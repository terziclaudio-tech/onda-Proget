# Review tecnica R³∞ ONDA — analisi e completamenti proposti

**Data:** 16 ottobre 2026
**Base documentale:** `README.md` (SHA b46ce80) e `docs/ONDA_FUSIONE_ARCHITETTURA.md` (SHA d56b289)
**Natura del documento:** proposta di revisione. Ogni completamento è marcato **[PROPOSTA]** e richiede conferma dell'ideatore prima di entrare nel protocollo; nulla in questo documento modifica lo stato delle evidenze.

---

## 1. Sintesi della review

Il progetto descrive un'architettura di agenti specializzati con memoria persistente, bus di coordinamento ONDA e controlli degli esiti. La documentazione è metodologicamente rigorosa nella distinzione fra proposta, risultato riportato e risultato riprodotto. I punti aperti individuati sono cinque, trattati nelle sezioni 3–7 con proposte di completamento.

---

## 2. Stato delle evidenze (confermato)

| Elemento | Stato | Azione |
|---|---|---|
| Architettura completa e dieci canali | Proposta | Specificare contratti (sezione 4) |
| Biblioteca 631 voci (311 ECC + 46 core + 274 Kimi) | Riportato, non riprodotto | Riprodurre nei giorni 1–5; i 5 nomi senza sorgente vanno risolti o rimossi dall'inventario |
| Integrazione locale (12 test, 107,48 s) | Riportato, campione circoscritto | Estendere il campione prima di conclusioni generali |
| Suite CI da 429 test | Riportato, non riprodotto | Rendere la suite eseguibile da terzi |
| ONDA e flotta autonoma | Non verificati | Obiettivo dei giorni 6–10 |

---

## 3. Gap 1 — Soglie dei controlli (Eval Gate, Security Scan, Memory Sync)

Il protocollo rinvia la definizione di soglie e politiche di ripetizione. **[PROPOSTA]** di valori iniziali, da confermare e preregistrare prima della sperimentazione:

### 3.1 Eval Gate

| Parametro | Valore proposto | Note |
|---|---|---|
| Postcondizioni critiche | 100% verificate per dichiarare il compito completato | Una postcondizione critica fallita = compito fallito, mai "completato parziale" |
| Postcondizioni secondarie | ≥ 90% | Sotto soglia: esito "degradato", tracciato |
| Esito incerto (verifica impossibile) | Stato `quarantena` | Non autorizza alcun retry automatico di azioni esterne |
| Retry azioni interne idempotenti | Max 2, backoff 5 s / 30 s | Solo con identificatore compito stabile (deduplicazione) |
| Retry azioni esterne | 0 automatici | Richiedono sempre ri-autorizzazione |

### 3.2 Security Scan

| Severità | Definizione | Azione proposta |
|---|---|---|
| Critica | Messaggio senza firma valida, mittente non autorizzato sul canale, envelope malformato | Stop del canale + allarme SENTIN-004 su `sdq1:bus:emergenza` |
| Alta | Payload che viola lo schema del canale | Quarantena del messaggio, log, notifica SECU-006 |
| Media | Anomalie di frequenza (es. heartbeat irregolari) | Log + metrica |
| Bassa | Deviazioni non bloccanti | Log |

Ogni messaggio sul bus deve avere envelope con: `id` (UUID), `epoch`, `mittente`, `canale`, `timestamp`, `firma HMAC`, `payload`. La verifica della firma precede qualsiasi elaborazione.

### 3.3 Memory Sync

| Parametro | Valore proposto |
|---|---|
| Verifica integrità | SHA-256 su ogni blocco sincronizzato; mismatch = stop sync + allarme, mai sovrascrittura automatica |
| Direzione | Sync bidirezionale consentita solo all'interno della stessa `epoch`; fra epoch diverse serve procedura di merge esplicita |
| Conflitto | Vince la copia con digest documentato nel registro di provenienza; l'altra va in quarantena |

---

## 4. Gap 2 — Durabilità del bus: Redis Pub/Sub → Redis Streams

**Problema.** Redis Pub/Sub è fire-and-forget: un messaggio pubblicato senza sottoscrittori attivi viene perso. Il protocollo richiede invece durabilità della coda, recupero dopo riavvio e prevenzione dei duplicati — proprietà che Pub/Sub non fornisce.

**[PROPOSTA].** Adottare **Redis Streams** per i canali che richiedono durabilità, mantenendo Pub/Sub solo dove la perdita è accettabile:

| Canale | Meccanismo proposto | Motivo |
|---|---|---|
| comandi | Stream + consumer group per ruolo | Durabilità, deduplicazione via ID messaggio |
| risposte | Stream | Traccia verificabile degli esiti |
| eventi | Stream con TTL (trim `MAXLEN`) | Storia limitata ma recuperabile |
| heartbeat | **Pub/Sub** | Effimero per natura; la perdita è irrilevante |
| emergenza | Pub/Sub + Stream di audit | Consegna immediata + traccia |
| eval, security | Stream | Auditabilità dei controlli |
| deploy | Stream | Traccia delle distribuzioni |
| content | Stream | I contenuti prodotti non devono perdersi |
| memory | Stream | La sincronizzazione richiede durabilità |

Recupero dopo riavvio: ogni consumatore riprende dai *pending entries* del proprio consumer group; l'ID messaggio (`<epoch>-<seq>`) funge da chiave di deduplicazione.

---

## 5. Gap 3 — Corrispondenza 12 ruoli ↔ 9 nodi

**[PROPOSTA]** di mappatura su nove nodi (accorpamenti per affinità di dominio):

| Nodo | Ruoli ospitati | Razionale |
|---|---|---|
| 1 | RAFFA-001 | Orchestrazione dedicata |
| 2 | SENTIN-004 | Supervisione isolata: deve sopravvivere al fallimento degli altri nodi |
| 3 | MEMO-002 | Memoria dedicata, accoppiata al volume persistente |
| 4 | PLAN-003 + ARCH-005 | Pianificazione e architettura condividono il contesto decisionale |
| 5 | SECU-006 | Sicurezza isolata (separazione dei ruoli rispetto a SENTIN-004) |
| 6 | PERF-007 + EVAL-009 | Misurazione e valutazione condividono la telemetria |
| 7 | MARK-008 + DOCU-012 | Contenuti e documentazione sono lo stesso flusso editoriale |
| 8 | GENE-010 | Generazione dedicata |
| 9 | E2ER-011 | Test end-to-end dedicati |

Vincolo architetturale: SENTIN-004 e SECU-006 restano su nodi distinti, perché allarme sicurezza e comando d'emergenza richiedono ruoli separati anche fisicamente.

---

## 6. Gap 4 — Piano originario dei 30 giorni: completamento

Il piano del 15 ottobre 2026 presenta caselle vuote e manca dei giorni 29–30. **[PROPOSTA]** di completamento, subordinato alla decisione fra piano originario e piano sperimentale riveduto (raccomandato il secondo):

- **Giorni 29–30 (piano originario):** consolidamento dei risultati, revisione delle caselle di verifica, decisione go/no-go documentata per la fase successiva. Nessuna nuova attività: solo chiusura e retrospettiva.
- **Date settimanali:** il giorno 1 decorre solo da baseline confermata (ambiente, versioni, dati di prova, permessi, budget), come già stabilito dal piano riveduto.

---

## 7. Gap 5 — Dati anagrafici da confermare (non deducibili)

Questi dati **non sono completabili dall'esterno** senza rischio di fabbricazione; restano azioni per l'ideatore:

1. **Anno dei trenta heartbeat storici** (16 settembre–15 ottobre, «riportati senza anno»): presumibilmente 2026, ma va confermato e annotato nel documento.
2. **I cinque nomi dell'inventario senza sorgente originale**: vanno ricondotti alla fonte o marcati come non verificati e rimossi dal conteggio operativo.
3. **Intestazione "FUSIONE COMPLETATA"**: va corretta in "integrazione documentata, verifiche in corso" oppure accompagnata dall'elenco delle attività ancora aperte, per evitare che il titolo dichiari uno stato che la tabella delle evidenze smentisce.

---

## 8. Raccomandazioni conclusive

1. Adottare il piano sperimentale riveduto come unico piano attivo; archiviare quello originario come documento storico.
2. Preregistrare le soglie della sezione 3 prima dei giorni 1–5, in modo che le verifiche siano indipendenti dallo sviluppo.
3. Migrare il disegno del bus a Redis Streams (sezione 4) prima dei giorni 6–10, altrimenti i test di recupero misurerebbero un meccanismo che non garantisce durabilità.
4. Risolvere i dati anagrafici della sezione 7 nella prossima revisione editoriale.

---

*Documento prodotto con contributo dell'assistente, in coerenza con la proposta editoriale: «Conservare la possibilità di essere corretto senza perdere la propria storia».*
