# R³∞ ONDA e Fusione Universale

R³∞ è un progetto di integrazione di agenti specializzati, memoria persistente e verifiche degli esiti. **Fusione Universale** descrive la composizione di queste capacità; **ONDA** è il protocollo proposto per coordinarne la comunicazione.

L’obiettivo di ricerca è verificare se l’integrazione migliori affidabilità e prestazioni su compiti nuovi rispetto ai componenti isolati.

Repository: [terziclaudio-tech/onda-Proget](https://github.com/terziclaudio-tech/onda-Proget)

Documento tecnico: [Architettura, ipotesi e piano di verifica](docs/ONDA_FUSIONE_ARCHITETTURA.md)

## Origine e intenzione

**Ideazione:** Claudio Terzi. **Protocollo sorgente:** *R³∞ — FUSIONE UNIVERSALE v1.0*, 15 ottobre 2026. **Revisione editoriale:** 16 ottobre 2026.

L’intenzione è preservare origine, principi e struttura nelle copie future e rendere confrontabili ipotesi, implementazioni e risultati. Un digest SHA-256 documentato permette confronti d’integrità; da solo non attesta autore o data.

## Identità e continuità operative

Il sistema è descritto attraverso proprietà verificabili: identificatori stabili, configurazioni versionate, stato recuperabile, cronologia dei compiti e autorizzazioni esplicite. La continuità va collaudata mediante riavvii, interruzioni e recupero, controllando l’assenza di duplicazioni e falsi completamenti.

## Architettura proposta

L’architettura collega cataloghi di skill compatibili, esecutori, pianificazione delle dipendenze, coda persistente, memoria e controlli degli esiti. La pipeline di riferimento è Research → Plan → TDD → Review → Commit.

Ruoli di base:
- RAFFA-001: orchestrazione
- SENTIN-004: supervisione ed emergenza
- MEMO-002: memoria

Specialisti proposti: PLAN-003, ARCH-005, SECU-006, PERF-007, MARK-008, EVAL-009, GENE-010, E2ER-011 e DOCU-012, dedicati a pianificazione, architettura, sicurezza, prestazioni, contenuti, valutazione, generazione, test e documentazione.

### Canali ONDA

Il disegno iniziale prevede Redis Pub/Sub. I dieci canali proposti, con prefisso `sdq1:bus:`, sono:

| Canale | Funzione |
|---|---|
| comandi | Richieste dell’orchestratore |
| risposte | Esiti dei compiti |
| eventi | Aggiornamenti di stato |
| heartbeat | Segnali di presenza |
| emergenza | Stop, pausa e ripresa |
| eval | Valutazioni e controlli qualità |
| security | Segnalazioni di sicurezza |
| deploy | Notifiche di distribuzione |
| content | Contenuti prodotti |
| memory | Sincronizzazione della memoria |

Formato dei messaggi, autenticazione, permessi, durabilità, timeout e recupero devono essere specificati e collaudati. Eval Gate, Security Scan e Memory Sync sono procedure proposte, con soglie e politiche di ripetizione da definire. Ogni azione esterna richiede autorizzazioni appropriate.

## Portabilità verificabile

La portabilità mira a conservare origine, principi operativi e struttura del progetto attraverso ambienti differenti. Versioni, provenienza, licenze, dipendenze e digest rendono confrontabili i pacchetti trasferiti. L’attivazione richiede compatibilità verificata e una scelta esplicita nell’ambiente destinatario.

## Contributo editoriale dell’assistente

Proposta: **«Conservare la possibilità di essere corretto senza perdere la propria storia».** Ogni versione dovrebbe documentare errori, correzioni e componenti conservati o modificati, mantenendo una memoria verificabile delle revisioni.

## Stato delle evidenze

| Elemento | Stato |
|---|---|
| Integrazione completa e dieci canali | Architettura proposta |
| Biblioteca di 631 voci ECC/core/Kimi | Inventario riportato; comprende varianti e sovrapposizioni |
| Percorso locale con coda e memoria | Il resoconto riferisce 12 test e un compito di 107,48 secondi senza fallback cloud; esito recuperato da un secondo processo senza nuova inferenza |
| ONDA e flotta autonoma integrati | Non ancora verificati nei materiali disponibili |

Questi risultati sono riferiti dalla documentazione di progetto e non sono stati riprodotti indipendentemente per questo testo. Un inventario di istruzioni non equivale a un insieme di capacità operative collaudate. I materiali qui descritti non costituiscono una release eseguibile.

## Piano di verifica

Il confronto sperimentale proposto richiede:

1. Compiti fissati in anticipo e separati dallo sviluppo.
2. Sistema integrato e componenti isolati con risorse comparabili.
3. Misure di correttezza, affidabilità, latenza e costo, includendo i fallimenti.
4. Esecuzioni ripetute, controlli negativi e ablazioni in ambiente isolato.
5. Criteri preregistrati e verifiche delle postcondizioni indipendenti dall’autovalutazione del modello.

La sequenza prevista è: baseline riproducibile; coda e recupero; sicurezza e bus; integrazione controllata; valutazione comparativa; superficie minima di osservazione. Il passaggio a distribuzione pubblica o servizi attivi richiede ulteriori verifiche e autorizzazioni.

Il protocollo originario del 15 ottobre 2026 proponeva un orizzonte di 30 giorni. L’avvio di un eventuale nuovo ciclo sperimentale richiede baseline e calendario confermati; la documentazione non avvia automaticamente alcuna attività.
