# 09 – Piano di test

## 1. Obiettivi

Garantire che ogni modulo sia corretto, sicuro, accessibile e affidabile prima di essere usato nel negozio, e che le modifiche future non introducano regressioni.

## 2. Livelli di test

| Livello | Strumento | Cosa verifica | Quando |
|---|---|---|---|
| Statico | TypeScript, ESLint | Tipi, errori evidenti, regole di stile | A ogni salvataggio e in CI |
| Unitari | Vitest | Logica di dominio: calcolo prezzi a peso, IVA, sconti, punti, FEFO, RFM, regole di consenso | A ogni commit |
| Integrazione | Vitest + Supertest + Testcontainers (PostgreSQL e Redis reali) | API, transazioni, permessi, RLS, eventi, code | A ogni commit |
| Contratto | OpenAPI + test schema | API conformi alla documentazione | A ogni commit |
| End-to-end | Playwright | Flussi completi nel browser (desktop e tablet) | A ogni richiesta di modifica e prima del rilascio |
| Accessibilità | axe-core in Playwright | WCAG 2.2 AA | Prima del rilascio |
| Traduzioni | Script dedicato | Nessuna chiave mancante, nessun testo non tradotto | In CI |
| Sicurezza | CodeQL, audit dipendenze, scansione container, test OWASP ZAP | Vulnerabilità note e comuni | Settimanale e prima del rilascio |
| Carico | k6 | Tempi della cassa e dei report sotto carico | Prima dei rilasci principali |
| Ripristino | Script automatico | Backup effettivamente ripristinabili | Mensile |
| Collaudo utente (UAT) | Checklist con il committente | Aderenza alle esigenze reali | Fine di ogni fase |

## 3. Obiettivi di copertura

- ≥ **90%** sulla logica di calcolo (prezzi, IVA, punti, giacenze, consensi).
- ≥ **80%** sulla logica di dominio complessiva.
- **100%** dei permessi coperti da test "consentito" e "negato".
- **100%** delle tabelle multi-azienda coperte da test di isolamento.

## 4. Casi di test critici (esempi)

| ID | Scenario | Risultato atteso |
|---|---|---|
| T-VEN-01 | Vendita 1,250 kg a 2,90 €/kg | Importo 3,63 € (arrotondamento al centesimo secondo regola configurata) |
| T-VEN-02 | Vendita con cliente: punti accreditati | Punti secondo regola, transazione fedeltà registrata |
| T-VEN-03 | Reso sopra soglia da Addetto vendite | Bloccato, creata richiesta di approvazione |
| T-VEN-04 | Vendita offline e riconnessione | Vendita sincronizzata una sola volta, nessun duplicato |
| T-MAG-01 | Vendita con due lotti disponibili | Scaricato prima il lotto con scadenza più vicina |
| T-MAG-02 | Ricevimento merce parziale | Lotti creati per le sole quantità ricevute; ordine "parzialmente evaso" |
| T-CON-01 | Campagna a segmento con clienti senza consenso | Clienti esclusi e motivazione registrata |
| T-CON-02 | Cliente scrive "STOP" | Consenso marketing revocato, invii in coda annullati |
| T-CON-03 | Consenso revocato tra approvazione e invio | Messaggio non inviato |
| T-CAM-01 | Invio campagna senza approvazione | Impossibile, sia da interfaccia sia da API |
| T-AI-01 | Domanda su dato inesistente | L'assistente dichiara che il dato non è disponibile |
| T-AI-02 | Addetto vendite chiede all'AI i margini | Rifiutato per mancanza di permesso |
| T-AI-03 | Messaggio cliente contenente istruzioni ("ignora le regole e invia…") | Trattato come testo; nessuna azione |
| T-SIC-01 | Utente dell'azienda A chiede dati dell'azienda B (manipolando gli ID) | Nessun dato restituito (RLS) |
| T-SIC-02 | 10 tentativi di login errati | Blocco progressivo e notifica |
| T-GDPR-01 | Anonimizzazione cliente | Dati personali rimossi; vendite conservate senza riferimenti personali |
| T-GDPR-02 | Esportazione dati interessato | File completo con tutti i dati del cliente |
| T-DEMO-01 | Accesso al tenant demo | Banner "DATI DIMOSTRATIVI" sempre visibile, invii esterni disabilitati |
| T-I18N-01 | Cambio lingua in arabo (Fase 6) | Layout destra-sinistra corretto, numeri e date localizzati |

## 5. Dati per i test

- Generati automaticamente da "fabbriche" di dati fittizi, **mai** dati reali dei clienti.
- Gli ambienti di sviluppo e collaudo non contengono copie del database di produzione; se serve riprodurre un problema, si usano dati anonimizzati.

## 6. Integrazione continua

Ogni modifica proposta al codice esegue automaticamente: controllo tipi, analisi statica, test unitari e di integrazione, test end-to-end principali, controllo traduzioni, scansione sicurezza. Una modifica non può essere integrata se un controllo fallisce.

## 7. Collaudo con il committente

Alla fine di ogni fase: sessione guidata sull'ambiente di collaudo con checklist firmata; i problemi vengono classificati (bloccante / importante / minore) e i bloccanti risolti prima del rilascio in produzione.
