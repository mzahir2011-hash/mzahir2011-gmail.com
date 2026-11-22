# 01 – Analisi dei requisiti

## 1. Contesto operativo

Negozio di vendita al dettaglio di frutta e verdura a Fontanellato (PR). Caratteristiche tipiche del settore, da confermare con il committente (vedi [11 – Domande aperte](11-domande-aperte.md)):

- **Vendita prevalentemente a peso** (€/kg), con articoli anche a pezzo, a mazzo, a cassetta, a confezione.
- **Prezzi variabili** anche quotidianamente, in funzione degli acquisti al mercato ortofrutticolo o dai fornitori.
- **Merce deperibile**: rischio di cali, scarti e invenduto; necessità di rotazione (primo arrivato, primo venduto).
- **Obblighi di etichettatura**: per l'ortofrutta fresca vanno indicati origine, categoria e varietà (norme UE di commercializzazione, Reg. UE 1308/2013 e Reg. delegato UE 2023/2429). Il sistema deve conservare questi dati per ogni prodotto/lotto.
- **Tracciabilità alimentare** (Reg. CE 178/2002): sapere da quale fornitore proviene ogni lotto.
- **Clientela mista**: privati, possibili clienti professionali (ristoranti, bar, mense) con fattura elettronica, possibili ordini telefonici/WhatsApp e consegne a domicilio.
- **Personale ridotto**: l'interfaccia di cassa deve essere velocissima e utilizzabile su tablet touch.

## 2. Attori (utenti del sistema)

| Attore | Descrizione |
|---|---|
| Titolare | Ibrahim: accesso completo, approva operazioni sensibili |
| Responsabile di negozio | Gestione operativa quotidiana |
| Addetto vendite / cassa | Vendite, clienti, prenotazioni |
| Magazziniere | Carichi, scarichi, inventari, scarti |
| Addetto marketing | Campagne e comunicazioni (con approvazione) |
| Consulente / commercialista | Sola lettura su report finanziari ed esportazioni |
| Cliente finale | **Non accede** al gestionale nella prima versione; interagisce via WhatsApp. Un'area clienti potrà essere valutata in futuro |
| Amministratore di piattaforma | Gestione tecnica multi-azienda (non vede i dati aziendali senza autorizzazione) |

## 3. Requisiti funzionali (per modulo)

Il codice `RF-xx` serve per tracciare ogni requisito fino ai test.

### 3.1 Dashboard direzionale
- RF-01 Indicatori del giorno: incasso, numero scontrini, scontrino medio, clienti identificati, top prodotti.
- RF-02 Confronto con giorno/settimana/mese precedente e stesso periodo anno precedente (quando disponibile).
- RF-03 Avvisi: scorte sotto soglia, lotti in scadenza, ordini da ricevere, messaggi WhatsApp non letti, approvazioni in attesa.
- RF-04 Ogni indicatore mostra la sua fonte e l'orario di aggiornamento; se i dati sono incompleti, lo dichiara.

### 3.2 Gestione clienti (CRM)
- RF-05 Anagrafica cliente privato e azienda (ragione sociale, P.IVA, codice fiscale, codice SDI/PEC).
- RF-06 Contatti, indirizzi di consegna multipli, preferenze, allergie/esigenze dichiarate (dato da trattare con cautela).
- RF-07 Storico acquisti, ordini, messaggi, punti fedeltà, note interne con autore e data.
- RF-08 Registrazione dei consensi (privacy, marketing, profilazione) con data, canale e testo dell'informativa accettata.
- RF-09 Ricerca rapida per nome, telefono, tessera; rilevamento duplicati e unione schede.
- RF-10 Esercizio dei diritti GDPR: esportazione dati, rettifica, cancellazione/anonimizzazione.

### 3.3 Segmentazione
- RF-11 Segmenti dinamici basati su regole (es. "acquisto negli ultimi 30 giorni", "spesa media > X", "acquista biologico").
- RF-12 Segmenti statici (liste manuali) ed etichette.
- RF-13 Analisi RFM (Recenza, Frequenza, Valore) calcolata automaticamente.
- RF-14 Anteprima del numero di clienti e di quanti hanno consenso valido al canale scelto.

### 3.4 Gestione vendite
- RF-15 Schermata di vendita rapida da tablet: ricerca prodotto, peso (manuale o da bilancia), quantità, sconti.
- RF-16 Associazione facoltativa del cliente (telefono o tessera) per punti e storico.
- RF-17 Metodi di pagamento registrati (contanti, carta, buono, altro) – **solo registrazione**, nessun incasso elettronico gestito dal sistema.
- RF-18 Collegamento allo scontrino del RT (numero e data del documento commerciale) o importazione dei corrispettivi.
- RF-19 Resi e annullamenti con motivazione, soggetti a permesso.
- RF-20 Chiusura giornaliera di cassa con quadratura.

### 3.5 Catalogo prodotti
- RF-21 Prodotti con categoria, varietà, origine, categoria commerciale (Extra, I, II), unità di misura, codice PLU/EAN, aliquota IVA, foto.
- RF-22 Listini multipli (al banco, clienti professionali, promozioni) con validità temporale.
- RF-23 Storico dei prezzi di vendita e di acquisto; calcolo del margine.
- RF-24 Stagionalità e disponibilità; prodotti attivi/inattivi.
- RF-25 Stampa/esportazione cartellini prezzo con origine e categoria.

### 3.6 Magazzino
- RF-26 Lotti con fornitore, data arrivo, quantità, costo, origine, eventuale data limite consigliata di vendita.
- RF-27 Movimenti: carico, vendita, reso, scarto/calo, rettifica inventario, trasferimento (futuro multi-sede).
- RF-28 Giacenza in tempo reale per prodotto e lotto; logica FEFO/FIFO.
- RF-29 Soglie di riordino e avvisi.
- RF-30 Inventario guidato da tablet.
- RF-31 Analisi degli scarti per prodotto, fornitore, motivo.

### 3.7 Ordini
- RF-32 Ordini clienti: prenotazioni, cesti, ordini per ristoranti, consegne a domicilio, ritiro in negozio.
- RF-33 Stati dell'ordine (bozza, confermato, in preparazione, pronto, consegnato, annullato) con notifiche.
- RF-34 Ordini d'acquisto ai fornitori, ricezione parziale/totale con generazione lotti.
- RF-35 Proposta di riordino basata su vendite e giacenze (con conferma umana).

### 3.8 Fornitori
- RF-36 Anagrafica fornitori, contatti, condizioni, prodotti forniti, listini d'acquisto.
- RF-37 Valutazione fornitori (qualità, puntualità, scarti).
- RF-38 Registrazione documenti di trasporto (DDT) e fatture d'acquisto (riferimenti e allegati).

### 3.9 Integrazione WhatsApp
- RF-39 Casella unica dei messaggi WhatsApp associati alla scheda cliente.
- RF-40 Risposte manuali da parte degli operatori; risposte rapide predefinite.
- RF-41 Modelli di messaggio approvati da Meta per comunicazioni fuori dalla finestra di 24 ore.
- RF-42 Gestione consenso e richiesta di disiscrizione ("STOP") automatica.
- RF-43 Notifiche transazionali (ordine pronto, conferma prenotazione) solo con consenso al servizio.

### 3.10 Campagne marketing
- RF-44 Creazione campagna: segmento, canale, messaggio, programmazione.
- RF-45 **Flusso di approvazione obbligatorio** prima dell'invio.
- RF-46 Esclusione automatica di chi non ha consenso valido.
- RF-47 Statistiche: inviati, consegnati, letti, risposte, vendite attribuite (con metodo dichiarato).
- RF-48 Limiti di frequenza per cliente (es. max N messaggi promozionali al mese).

### 3.11 Programma fedeltà
- RF-49 Regole di accumulo (es. punti per euro, bonus su categorie) configurabili.
- RF-50 Premi e soglie; riscatto in cassa.
- RF-51 Tessera digitale (QR o numero di telefono).
- RF-52 Scadenza punti e regolamento del programma conforme alla normativa sulle manifestazioni a premio (DPR 430/2001) – da verificare con consulente.

### 3.12 Fidelizzazione e recupero clienti
- RF-53 Individuazione clienti a rischio abbandono (assenza oltre soglia rispetto alla loro frequenza abituale).
- RF-54 Suggerimento di azioni di recupero (messaggio, offerta) da approvare.
- RF-55 Messaggi di compleanno/ricorrenza solo con consenso.

### 3.13 Recensioni e referral
- RF-56 Richiesta di recensione (es. Google) dopo l'acquisto, solo con consenso e senza incentivi vietati alle recensioni positive.
- RF-57 Raccolta feedback interni (voto + commento).
- RF-58 Programma "presenta un amico" con codice referral e premio a entrambi, con regole antiabuso.

### 3.14 Analisi delle performance
- RF-59 Vendite per prodotto, categoria, fascia oraria, giorno della settimana, operatore.
- RF-60 Margini, rotazione, scarti, valore di magazzino.
- RF-61 Analisi clienti: nuovi, ricorrenti, persi, valore nel tempo.
- RF-62 Efficacia campagne e programma fedeltà.

### 3.15 Assistente aziendale AI
- RF-63 Domande in linguaggio naturale sui dati aziendali ("quanto ho venduto di fragole a maggio?").
- RF-64 Risposte con indicazione delle fonti (quali dati sono stati letti) e dichiarazione esplicita di incertezza.
- RF-65 Bozze: testi di messaggi, descrizioni prodotti, proposte di riordino, riepiloghi.
- RF-66 **Nessuna azione automatica**: ogni azione proposta dall'AI crea una richiesta che un utente autorizzato deve approvare.
- RF-67 L'AI non inventa numeri: se un dato non esiste nel database, lo dice.

### 3.16 Automazioni
- RF-68 Regole "quando… se… allora…" (es. quando un lotto supera N giorni → avviso al responsabile).
- RF-69 Pianificazioni (giornaliere, settimanali).
- RF-70 Azioni verso l'esterno (messaggi ai clienti) sempre soggette a consenso e, se configurato, ad approvazione.
- RF-71 Registro di ogni esecuzione con esito.

### 3.17 Report finanziari e operativi
- RF-72 Report incassi giornalieri/mensili per aliquota IVA e metodo di pagamento.
- RF-73 Report acquisti per fornitore; costo del venduto stimato; margine lordo.
- RF-74 Report magazzino e scarti.
- RF-75 Esportazione in PDF, Excel/CSV per il commercialista.
- RF-76 Ogni report indica il periodo, la data di generazione e se contiene dati incompleti. **I report del CRM sono gestionali e non sostituiscono la contabilità ufficiale.**

## 4. Requisiti non funzionali

| Codice | Requisito | Obiettivo misurabile |
|---|---|---|
| RNF-01 | Lingua | 100% dei testi in italiano tramite file di traduzione; nessun testo "cablato" nel codice |
| RNF-02 | Multilingua futuro | Aggiunta di inglese e arabo (con layout destra-sinistra) senza modifiche al codice |
| RNF-03 | Prestazioni cassa | Registrazione di una riga di vendita < 300 ms; apertura schermata < 1,5 s su tablet medio |
| RNF-04 | Disponibilità | ≥ 99,5% mensile in orario di apertura |
| RNF-05 | Continuità | Vendita possibile anche con connessione instabile (coda locale e sincronizzazione) – da valutare in Fase 1 |
| RNF-06 | Backup | RPO ≤ 15 minuti, RTO ≤ 4 ore |
| RNF-07 | Sicurezza | Conformità OWASP ASVS livello 2 |
| RNF-08 | Accessibilità | WCAG 2.2 livello AA |
| RNF-09 | Responsive | Smartphone, tablet (cassa), desktop |
| RNF-10 | Tracciabilità | Ogni modifica a dati rilevanti registrata nel registro attività |
| RNF-11 | Multi-azienda | Isolamento totale dei dati tra aziende, verificato da test automatici |
| RNF-12 | Manutenibilità | Copertura test ≥ 80% sulla logica di dominio |
| RNF-13 | Distinzione dati | Dati demo solo in un'azienda dimostrativa separata e segnalata |

## 5. Vincoli normativi da rispettare

| Norma | Impatto sul sistema |
|---|---|
| GDPR (Reg. UE 2016/679) e Codice Privacy (D.Lgs. 196/2003 mod. D.Lgs. 101/2018) | Consensi, informative, diritti, registro trattamenti, sicurezza, DPA con fornitori |
| Provvedimenti del Garante su marketing e fidelity card | Consensi separati marketing/profilazione; tempi di conservazione limitati per profilazione |
| Codice del Consumo (D.Lgs. 206/2005) | Trasparenza su prezzi e promozioni |
| Normativa corrispettivi telematici (art. 2 D.Lgs. 127/2015) | Il CRM non emette scontrini fiscali; si integra con l'RT |
| Fatturazione elettronica (SDI) | Eventuale integrazione per clienti professionali tramite intermediario |
| Tracciabilità alimentare (Reg. CE 178/2002) | Lotti e fornitori conservati |
| Norme di commercializzazione ortofrutta (UE) | Origine, categoria, varietà su prodotti e cartellini |
| Manifestazioni a premio (DPR 430/2001) | Programma fedeltà: regolamento e verifica di eventuali adempimenti |
| Policy WhatsApp Business / Meta | Opt-in, modelli approvati, finestra 24 ore |
| AI Act (Reg. UE 2024/1689) | Trasparenza sull'uso dell'AI; supervisione umana |

> Nota: le indicazioni normative sono un quadro progettuale e non costituiscono consulenza legale o fiscale. Le scelte finali vanno validate con il commercialista e, per la privacy, con un consulente.

## 6. Fuori ambito nella prima versione

- Contabilità generale e bilancio (si esportano i dati verso il commercialista).
- Gestione paghe e presenze del personale.
- E-commerce pubblico con pagamento online (valutabile in futuro).
- App nativa per iOS/Android (la PWA copre l'esigenza).
