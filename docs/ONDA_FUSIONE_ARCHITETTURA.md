# R³∞ ONDA e Fusione Universale

## Architettura ipotesi e piano di verifica

## Origine e intenzione

**Ideazione:** Claudio Terzi. **Protocollo sorgente:** *R³∞ — FUSIONE UNIVERSALE v1.0*, 15 ottobre 2026. **Revisione editoriale:** 16 ottobre 2026.

L’intenzione è preservare origine, principi e struttura nelle copie future e rendere confrontabili ipotesi, implementazioni e risultati. Un digest SHA-256 documentato permette confronti d’integrità; da solo non attesta autore o data.

## Scopo e definizioni operative

R³∞ propone un sistema di agenti specializzati capace di conservare stato, coordinare attività e verificare risultati attraverso sessioni differenti.

**Fusione Universale** integra raccolte Kimi/ECC, memoria, strumenti, controlli e orchestrazione. **ONDA** coordina la comunicazione. **ClaudioRaffaelloCore** resta distinto: il nucleo tecnico da specificare come configurazione versionata, principi operativi e cronologia.

L’“esistenza” del sistema viene qui definita operativamente: identità identificabile, configurazione recuperabile, stato persistente, continuità dei compiti e storia verificabile delle esecuzioni. La Scacchiera Quantica descrive nell’originale otto direzioni di esplorazione e branching; il suo contributo algoritmico richiede una specifica valutabile.

## Architettura proposta

L’integrazione comprende catalogo delle skill con provenienza e prerequisiti, esecutori compatibili, orchestratore di dipendenze, coda persistente, stato recuperabile, bus ONDA e controlli indipendenti degli esiti.

Pipeline originaria: Research → Plan → TDD → Review → Commit. Ciascun passaggio deve conservare autorizzazioni, identificatore del compito, input, versione degli strumenti ed evidenze dell’esito. Le attività esterne richiedono permessi specifici.

Ruoli di base e specialisti proposti:

- RAFFA-001: orchestrazione; SENTIN-004: supervisione; MEMO-002: memoria.
- PLAN-003: pianificazione; ARCH-005: architettura; SECU-006: sicurezza; PERF-007: prestazioni.
- MARK-008: contenuti; EVAL-009: valutazione; GENE-010: generazione; E2ER-011: test; DOCU-012: documentazione.

Resta da chiarire la corrispondenza fra dodici ruoli e “nove nodi”.

### Canali ONDA

Tutti i canali proposti usano il prefisso `sdq1:bus:`.

| Canale | Funzione | Mittente previsto |
|---|---|---|
| comandi | Richieste di esecuzione | RAFFA-001 |
| risposte | Esiti | Tutti |
| eventi | Aggiornamenti di stato | Tutti |
| heartbeat | Segnali di presenza | Tutti |
| emergenza | Stop, pausa, ripresa | SENTIN-004 |
| eval | Valutazioni e controlli qualità | EVAL-009 |
| security | Segnalazioni di sicurezza | SECU-006 |
| deploy | Notifiche di distribuzione | ARCH-005 |
| content | Contenuti prodotti | MARK-008 |
| memory | Sincronizzazione della memoria | MEMO-002 |

Il disegno iniziale usa Redis Pub/Sub, envelope comuni e stato su Redis. Durabilità della coda, recupero, autenticazione e gestione delle versioni di coordinamento, chiamate epoch, richiedono contratti espliciti.

### Controlli e recupero

L’originale propone **Eval Gate**, **Security Scan** e **Memory Sync**: valutazione degli esiti, controllo dei messaggi e sincronizzazione con CK/unified-memory verificata tramite hash.

La specifica deve fissare soglie, limiti dei tentativi e gestione degli esiti incerti. Un’interruzione non autorizza a ripetere automaticamente un’azione esterna. Identificatori stabili e verifica delle postcondizioni devono prevenire duplicazioni e completamenti dichiarati erroneamente.

Vanno inoltre definiti isolamento dei dati, permessi per canale, revoca, arresto e recupero autenticato. Un allarme SECU-006 e un comando d’emergenza SENTIN-004 richiedono ruoli distinti e una procedura coerente.

## Portabilità verificabile

La portabilità mira a conservare origine, principi operativi e struttura del progetto in ambienti differenti. Una descrizione del pacchetto può associare versione, sorgenti, licenze, dipendenze e digest dei file. Ogni importazione deve documentare provenienza e compatibilità, mantenere i confini dei permessi e prevedere un’attivazione esplicita nell’ambiente destinatario.

## Contributo editoriale dell’assistente

Proposta: **«Conservare la possibilità di essere corretto senza perdere la propria storia».** Ogni versione dovrebbe documentare errori, correzioni e componenti conservati o modificati, mantenendo una memoria verificabile delle revisioni.

## Stato delle evidenze

La tabella distingue specifiche e risultati riferiti, non riprodotti indipendentemente per questa sintesi.

| Elemento | Evidenza disponibile | Stato |
|---|---|---|
| Architettura completa e dieci canali | Protocollo del 15 ottobre 2026 | Proposta |
| Biblioteca recuperata | 311 voci ECC, 46 varianti core, 274 skill principali Kimi: 631 voci, più indice | Riportato, non riprodotto |
| Profili e regole | 71 profili agente; 121 file di regole in 22 gruppi | Riportato, non riprodotto |
| Integrazione locale | Coda R3, OmniRoute, ECC Memory Vault; 12 test; un compito locale in 107,48 secondi; rilettura senza nuova inferenza | Riportato, non riprodotto |
| Verifiche delle issue | Suite CI da 429 test; controllo preregistrato con cinque discrepanze rilevate su cinque | Riportato, non riprodotto |
| ONDA e flotta autonoma | Il resoconto locale li indica ancora da implementare e collaudare | Non verificati |

Le 631 voci comprendono varianti e sovrapposizioni. Cinque nomi rimangono riferimenti senza sorgente originale recuperato. Questi inventari correggono i conteggi preliminari del protocollo; la disponibilità di istruzioni non dimostra altrettante capacità operative.

L’intestazione “FUSIONE COMPLETATA” convive con attività ancora aperte. Suite, patch pronte, merge e runtime attivi devono restare distinguibili.

## Ipotesi e metodo sperimentale

L’ipotesi è che memoria persistente, coordinamento e verifica integrati migliorino l’affidabilità e il trasferimento a compiti nuovi rispetto ai componenti isolati. L’intuizione “1+1=3” va resa misurabile.

Il confronto deve prevedere:

- compiti fissati prima della valutazione, separati dallo sviluppo;
- componenti isolati e sistema integrato con risorse comparabili;
- correttezza delle postcondizioni, affidabilità, latenza e costo complessivo;
- esecuzioni ripetute, variabilità, fallimenti e controlli negativi;
- ablazioni in ambiente isolato per misurare il contributo delle componenti;
- criteri preregistrati e verificatori indipendenti dall’autovalutazione del modello.

I test locali riferiti documentano un campione circoscritto. Miglioramenti generali, sicurezza complessiva e crescita delle prestazioni richiedono ulteriori evidenze.

## Piano originario dei 30 giorni

Il documento del **15 ottobre 2026** presenta quattro settimane, con tutte le caselle vuote:

1. **Fondazione:** installare ECC; configurare CK; mappare regole a Python/TypeScript/Rust; predisporre autonomous-agent-harness.
2. **Orchestrazione:** orch-pipeline; dmux per nove nodi; team-agent-orchestration/Kanban; continuous-agent-loop con heartbeat ONDA.
3. **Sviluppo:** portale Three.js; backend tRPC/Drizzle/MySQL; bus Redis; Docker/Kubernetes.
4. **Lancio:** pitch deck; contenuti social; ricerca competitor; canary-watch.

Mancano avvio confermato, date settimanali e attività dei giorni 29–30. Sono distinti dai trenta heartbeat storici del 16 settembre–15 ottobre, riportati senza anno.

## Piano sperimentale riveduto

**Nuova proposta.** Il giorno 1 decorre soltanto da una baseline confermata: ambiente, versioni, dati di prova, permessi e budget di risorse definiti. Il piano non attiva servizi né impegna spese o pubblicazioni.

| Giorni | Attività e risultato da verificare |
|---|---|
| 1–5 | Riprodurre il campione locale; verificare inventario, coda persistente, checkpoint e recupero dopo riavvio. |
| 6–10 | Specificare e collaudare ONDA: permessi, duplicati, interruzioni, heartbeat, pausa e recupero autenticato. |
| 11–17 | Integrare pianificazione, memoria e valutazione su compiti circoscritti; verificare postcondizioni e tracce. |
| 18–24 | Eseguire confronti, ripetizioni, ablazioni e analisi dei fallimenti sui compiti separati dallo sviluppo. |
| 25–28 | Solo dopo i controlli precedenti, preparare una superficie minima di osservazione e collaudo. Kubernetes resta opzionale, subordinato a necessità misurate. |
| 29–30 | Consolidare risultati riproducibili, limiti e decisioni per la fase successiva. |

Dipendenze: persistenza prima della sincronizzazione; hardening prima dell’interoperabilità; identità completa prima del giudizio automatizzato; postcondizioni prima delle azioni fisiche. Distribuzione pubblica e lancio richiedono decisioni separate.

## Riferimenti documentali

- *R³∞ — FUSIONE UNIVERSALE v1.0*, 15 ottobre 2026: architettura primaria e piano originario.
- *R3 Skill globali e prima integrazione locale*: inventario corretto e campione locale riferito.
- Mappa delle issue R3 dalle fondamenta al prodotto: dipendenze e verifiche riferite.
- *ClaudioRaffaelloCore 1.0*: riferimento originario al nucleo del progetto.
