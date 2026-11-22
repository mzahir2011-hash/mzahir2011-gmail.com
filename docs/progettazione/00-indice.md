# 00 – Sintesi esecutiva

**Progetto:** CRM IBRA
**Committente:** Frutta e Verdura di Ibrahim – Fontanellato (PR)
**Fase:** 1 – Analisi e progettazione (in attesa di approvazione)
**Data documento:** 22 novembre 2026
**Versione:** 0.1 (bozza per revisione)

---

## 1. In una frase

Un'applicazione web in italiano, utilizzabile da computer, tablet in cassa e smartphone, che riunisce in un unico sistema clienti, vendite, prodotti a peso, magazzino con lotti e scadenze, fornitori, ordini, WhatsApp, fedeltà, marketing e un assistente AI che **propone** azioni ma **non agisce mai senza conferma umana**.

## 2. Decisioni chiave proposte

| Ambito | Proposta | Motivo principale |
|---|---|---|
| Tipo di applicazione | Web app responsive + installabile (PWA) | Un solo prodotto per PC, tablet e smartphone; nessuna app store |
| Linguaggio | TypeScript su tutto lo stack | Un solo linguaggio, tipizzazione forte, meno errori |
| Frontend | Next.js + React + Tailwind CSS + shadcn/ui | Standard di mercato, ottimo supporto i18n e RTL (arabo) |
| Backend | NestJS (monolite modulare) | Moduli separati e ordinati, pronto per crescere |
| Database | PostgreSQL 16 + Prisma ORM | Affidabile, transazionale, isolamento multi-azienda con Row-Level Security |
| Code e automazioni | Redis + BullMQ | Invii WhatsApp, promemoria, automazioni programmate |
| WhatsApp | WhatsApp Business Platform (Cloud API ufficiale Meta) | Unico canale lecito e stabile per messaggi aziendali |
| AI | API Claude (Anthropic), modello `claude-opus-5-5`, con strumenti in sola lettura e azioni soggette ad approvazione | Qualità di ragionamento, controllo totale delle azioni |
| Hosting | Server in Unione Europea (Italia o Germania) | GDPR, latenza bassa |
| Fiscalità | **Il CRM non sostituisce il Registratore Telematico (RT)** | Obbligo di legge per scontrini; integrazione o registrazione parallela |

## 3. Cosa NON farà il sistema (per scelta e per legge)

- Non emetterà documenti commerciali fiscali al posto del Registratore Telematico, salvo integrazione certificata con un RT o con un servizio di "RT in cloud" autorizzato.
- Non eseguirà pagamenti o trasferimenti di denaro reali.
- Non invierà messaggi promozionali a clienti privi di consenso registrato, né senza approvazione umana della campagna.
- Non mostrerà mai dati dimostrativi confondibili con dati reali: l'ambiente demo è un'azienda separata, con un banner fisso **"DATI DIMOSTRATIVI"**.

## 4. Fasi di sviluppo (sintesi)

| Fase | Contenuto | Esito |
|---|---|---|
| 0 | Fondamenta: autenticazione, ruoli, registro attività, multi-azienda, i18n, CI/CD, backup | Piattaforma sicura vuota |
| 1 | **MVP operativo**: clienti, prodotti e listini, magazzino e lotti, vendite, dashboard base | Utilizzabile in negozio |
| 2 | Fornitori, ordini d'acquisto, ordini clienti/prenotazioni/consegne | Ciclo acquisti-vendite completo |
| 3 | WhatsApp, consensi, campagne, segmentazione, programma fedeltà | Comunicazione e fidelizzazione |
| 4 | Recupero clienti, recensioni e referral, automazioni | Crescita clienti |
| 5 | Assistente AI, analisi avanzate, report finanziari e operativi | Supporto decisionale |
| 6 | Multi-azienda completo, inglese e arabo, rifiniture | Prodotto riutilizzabile |

Dettaglio in [08 – Roadmap](08-roadmap.md).

## 5. Cosa serve dal committente

Prima dell'avvio dello sviluppo occorre:

1. **Approvazione** di architettura, stack e roadmap (o richiesta di modifiche).
2. **Risposte** alle domande in [11 – Domande aperte](11-domande-aperte.md), in particolare quelle marcate come *bloccanti* (registratore di cassa, bilancia, numero WhatsApp, budget di hosting).

## 6. Glossario essenziale

| Termine | Significato |
|---|---|
| RT | Registratore Telematico: cassa che trasmette i corrispettivi all'Agenzia delle Entrate |
| Corrispettivi | Incassi giornalieri da vendite al dettaglio |
| SDI | Sistema di Interscambio per la fattura elettronica |
| Lotto | Partita di merce con stessa origine, data di arrivo e fornitore (tracciabilità) |
| Calo / scarto | Merce persa per deperimento, danneggiamento, rottura |
| PLU | Codice articolo usato dalla bilancia |
| Opt-in | Consenso esplicito del cliente a ricevere comunicazioni |
| Tenant | Singola azienda ospitata nella piattaforma multi-azienda |
| PWA | Progressive Web App: sito installabile come un'app |
