# 07 – Piano di sicurezza e conformità GDPR

## 1. Ruoli privacy

| Soggetto | Ruolo GDPR |
|---|---|
| Frutta e Verdura di Ibrahim | **Titolare del trattamento** dei dati dei propri clienti |
| Fornitore della piattaforma CRM IBRA (sviluppo/gestione) | **Responsabile del trattamento** (art. 28) – serve un contratto/DPA |
| Hosting, WhatsApp/Meta, Anthropic (AI), email, backup | **Sub-responsabili** – elenco pubblicato e DPA con ciascuno |
| Personale del negozio | Persone autorizzate al trattamento (art. 29), con istruzioni scritte |

## 2. Adempimenti GDPR previsti

| Adempimento | Come lo supporta il sistema |
|---|---|
| Informativa (artt. 13-14) | Versioni archiviate; collegamento a ogni consenso; testo breve per WhatsApp e cassa |
| Base giuridica e consensi | Consensi **separati e facoltativi** per marketing e profilazione; il servizio (es. ordine) non richiede consenso marketing |
| Prova del consenso | Data, ora, canale, operatore, versione informativa, eventuale messaggio originale |
| Revoca semplice | "STOP" su WhatsApp, pulsante in scheda cliente, effetto immediato |
| Diritti dell'interessato (artt. 15-22) | Procedura guidata: accesso/esportazione, rettifica, cancellazione (anonimizzazione), limitazione, opposizione, portabilità; scadenza a 30 giorni monitorata |
| Minimizzazione | Campi facoltativi chiaramente distinti; data di nascita solo se serve per auguri con consenso |
| Limitazione della conservazione | Regole automatiche di cancellazione/aggregazione (vedi doc. 03 §6) |
| Registro dei trattamenti (art. 30) | Modello precompilato fornito con la documentazione |
| Valutazione d'impatto (DPIA, art. 35) | Da valutare per profilazione + AI; bozza fornita |
| Privacy by design / by default | Marketing disattivato per impostazione predefinita, RLS, cifratura, pseudonimizzazione per AI |
| Violazione dei dati (artt. 33-34) | Procedura di notifica entro 72 ore, registro incidenti |
| Trasferimenti extra UE | Hosting in UE; per Meta e Anthropic verifica di clausole contrattuali standard / Data Privacy Framework e opzioni di localizzazione dati |

> Questa sezione è un supporto tecnico-organizzativo e non sostituisce una consulenza legale. Si consiglia di validare informative e registro con un consulente privacy.

## 3. Sicurezza tecnica

### 3.1 Applicazione
- Conformità **OWASP ASVS livello 2** e controllo **OWASP Top 10** a ogni rilascio.
- Validazione di tutti gli input (Zod) e query parametrizzate (Prisma).
- Protezione CSRF, intestazioni di sicurezza (CSP, HSTS, X-Frame-Options), limitazione delle richieste.
- Controllo autorizzazioni centralizzato su ogni endpoint, con test automatici per ogni permesso.
- Isolamento aziende con **Row-Level Security** e test che tentano accessi incrociati.
- Caricamento file: controllo tipo, dimensione, scansione antivirus.
- Webhook WhatsApp verificati tramite firma.
- Protezione dall'iniezione di istruzioni nell'AI: i contenuti dei clienti (es. messaggi WhatsApp) sono trattati come dati, mai come comandi; l'AI non ha strumenti di scrittura diretta.

### 3.2 Dati
- Cifratura **in transito** (TLS 1.2+, preferibilmente 1.3) e **a riposo** (dischi e backup cifrati).
- Cifratura a livello di colonna per dati delicati (note su allergie/esigenze, documenti).
- Segreti (token WhatsApp, chiavi API) in un gestore di segreti, mai nel codice o nel repository.
- Esportazioni di dati personali con scadenza del link e registro.

### 3.3 Infrastruttura
- Server in **UE**; accesso amministrativo solo con chiavi SSH/VPN e 2FA.
- Principio del minimo privilegio per servizi e persone.
- Aggiornamenti di sicurezza automatici del sistema operativo; immagini container minimali.
- Firewall: esposti solo HTTPS e (se necessario) il webhook WhatsApp.
- Monitoraggio: disponibilità, errori, tentativi di accesso anomali, con avvisi.

## 4. Registro delle attività

Registrate automaticamente, con chi/cosa/quando/da dove e valori prima/dopo:

- Accessi riusciti e falliti, cambi password, attivazione 2FA.
- Creazione/modifica/cancellazione di clienti, prodotti, prezzi, ordini, fornitori.
- Vendite, resi, annullamenti, chiusure di cassa.
- Movimenti e rettifiche di magazzino.
- Consensi rilasciati e revocati.
- Campagne create, approvate, inviate.
- Approvazioni e rifiuti.
- Esportazioni di dati.
- Proposte e consultazioni dell'assistente AI.
- Modifiche a ruoli, permessi e impostazioni.

Il registro è **a sola aggiunta** (nessuno può modificarlo o cancellarlo dall'applicazione), con hash concatenati per rilevare manomissioni.

## 5. Backup e ripristino

| Elemento | Strategia |
|---|---|
| Database | Backup continuo (WAL) con **ripristino a un punto nel tempo**; backup completo giornaliero |
| File | Replica giornaliera con versionamento |
| Regola 3-2-1 | 3 copie, 2 supporti diversi, 1 fuori sede (altro data center UE) |
| Cifratura | Tutti i backup cifrati con chiavi separate |
| Conservazione | Giornalieri 35 giorni, mensili 12 mesi |
| Obiettivi | RPO ≤ 15 minuti, RTO ≤ 4 ore |
| Verifica | **Prova di ripristino automatica mensile** su ambiente isolato, con rapporto |
| Esportazione per il Titolare | Possibilità di scaricare in qualsiasi momento tutti i propri dati (CSV/Excel) – nessun vincolo verso il fornitore |

## 6. Misure organizzative

- Istruzioni scritte per il personale (uso password, dispositivi, privacy al banco).
- Account personali: **vietato** condividere credenziali.
- Disattivazione immediata degli utenti che lasciano l'azienda.
- Revisione trimestrale degli accessi.
- Formazione iniziale sull'uso corretto di consensi e WhatsApp.

## 7. Regole per WhatsApp

- Solo **WhatsApp Business Platform** ufficiale; vietati strumenti non ufficiali di invio massivo (rischio blocco numero e violazioni).
- Opt-in esplicito raccolto prima dei messaggi promozionali.
- Modelli di messaggio approvati da Meta per i messaggi fuori dalla finestra di 24 ore.
- Ogni messaggio promozionale include l'istruzione per disiscriversi.
- Limiti di frequenza per non disturbare i clienti.

## 8. Regole per l'AI

- Supervisione umana obbligatoria su ogni proposta (art. 14 AI Act come buona pratica).
- Nessuna decisione automatizzata con effetti significativi sui clienti (art. 22 GDPR).
- Dati inviati al modello ridotti al minimo e, dove possibile, pseudonimizzati.
- Interruttore per disattivare il modulo AI per azienda.
- Informazione agli utenti interni sull'uso di un sistema di AI.
