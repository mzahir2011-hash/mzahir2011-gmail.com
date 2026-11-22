# 11 – Informazioni aziendali mancanti e domande aperte

Le domande marcate con **[B]** sono **bloccanti**: senza risposta non è possibile completare la progettazione della fase indicata.
Dove non si conosce la risposta, va bene indicarlo: proporremo una soluzione predefinita.

## A. Dati dell'azienda

1. **[B – Fase 0]** Ragione sociale esatta, forma giuridica, Partita IVA, indirizzo della sede.
2. Ci sono (o sono previsti) altri punti vendita, banchi al mercato o un magazzino separato?
3. Orari di apertura e giorni di chiusura.
4. Esiste un logo e dei colori aziendali? Esiste un sito web o una scheda Google dell'attività?
5. Quante persone lavorano nel negozio e con quali mansioni? Quante useranno il sistema?

## B. Cassa, fiscalità, hardware

6. **[B – Fase 1]** Marca e modello del **Registratore Telematico** in uso. È collegabile in rete? Chi è il fornitore/assistenza?
7. **[B – Fase 1]** Marca e modello della **bilancia**. Stampa etichette con codice a barre? È collegata alla cassa?
8. Quali metodi di pagamento accettate (contanti, carte, POS collegato alla cassa, buoni pasto, altro)?
9. Emettete **fatture** a clienti professionali (ristoranti, bar, mense)? Con quale programma o intermediario oggi?
10. Chi è il **commercialista**? È disponibile a validare aliquote IVA, esportazioni e regolamento fedeltà?
11. Quali aliquote IVA applicate oggi e su quali tipologie di prodotto? (non le assumiamo: vanno confermate)
12. Che dispositivi avete oggi (PC, tablet, smartphone, stampanti) e com'è la **connessione internet** in negozio (fibra, ADSL, 4G, stabile o no)?

## C. Prodotti e magazzino

13. Quanti prodotti indicativamente avete in assortimento? Vendete anche prodotti confezionati (con codice EAN), secchi, conserve, altro oltre all'ortofrutta?
14. Come e con che frequenza cambiano i prezzi? Chi li decide?
15. Da chi acquistate (mercato ortofrutticolo, grossisti, produttori locali)? Quanti fornitori abituali?
16. Come ordinate oggi ai fornitori (telefono, WhatsApp, email, di persona)?
17. Registrate oggi scarti/cali? Fate inventari?
18. Esiste già un elenco prodotti/prezzi in formato digitale (Excel, gestionale della cassa)?

## D. Clienti e vendite

19. Avete già un elenco clienti (rubrica, Excel, gruppo WhatsApp, quaderno)? Con quali consensi raccolti?
20. Fate **consegne a domicilio** o prenotazioni (cesti, ordini per ristoranti)? In quali zone e con quali giorni/orari?
21. Clientela principale: famiglie, anziani, ristoranti, stranieri? Lingue parlate dai clienti (utile per arabo/inglese)?
22. Indicativamente, quanti scontrini al giorno? (serve solo per dimensionare il sistema; non verrà usato come dato commerciale)

## E. WhatsApp e comunicazione

23. **[B – Fase 3]** Usate oggi WhatsApp normale o **WhatsApp Business**? Con quale numero? Siete disposti a usare un numero dedicato per la piattaforma ufficiale (WhatsApp Business Platform)?
24. Avete un account **Meta Business** (Facebook/Instagram aziendale)?
25. Che tipo di messaggi vorreste inviare (offerte del giorno, prodotti arrivati, ordine pronto, auguri)? Con che frequenza massima?
26. Chi deve approvare le campagne: solo il Titolare o anche un responsabile?

## F. Fedeltà, recensioni, referral

27. Avete già una tessera o un programma fedeltà? Che tipo di premio immaginate (sconto, prodotto omaggio, buono)?
28. Volete raccogliere recensioni su Google? Avete accesso al profilo dell'attività?
29. Interessa il programma "presenta un amico"? Con quale premio?

## G. AI, automazioni, report

30. Quali sono le 3 domande che vorreste porre più spesso all'assistente AI?
31. Quali report vi servono ogni giorno, settimana, mese? Cosa chiede oggi il commercialista?
32. Siete d'accordo con l'uso di un servizio AI esterno (Anthropic) con dati ridotti al minimo, oppure preferite disattivare l'AI all'inizio?

## H. Ruoli, sicurezza, privacy

33. Chi oltre al Titolare deve poter fare resi, sconti, modifiche prezzi, approvazioni? Con quali soglie (importi, percentuali)?
34. Avete un consulente privacy o un DPO? Avete già un'informativa privacy?
35. Lingua preferita di ciascun utente interno (in vista dell'arabo/inglese).

## I. Budget, tempi, pubblicazione

36. **[B – Fase 0]** Budget mensile indicativo per i costi ricorrenti (hosting, WhatsApp, AI, email, backup).
37. C'è una data obiettivo per iniziare a usare il sistema in negozio?
38. Dominio internet disponibile o da registrare?
39. Preferenza tra server in Italia o in altro paese UE?
40. In futuro chi gestirà la piattaforma per altre aziende (il committente stesso, un partner, una nuova società)? Questo influenza licenze, contratti e modello multi-azienda.

## L. Decisioni da approvare

Oltre alle risposte, chiediamo conferma esplicita su:

| # | Decisione | Proposta |
|---|---|---|
| D1 | Stack tecnologico | Next.js + NestJS + PostgreSQL (doc. 02) |
| D2 | Hosting | Opzione C in UE (doc. 10) |
| D3 | WhatsApp | Solo piattaforma ufficiale Meta |
| D4 | Integrazione cassa | RT integrato se possibile, altrimenti importazione corrispettivi |
| D5 | AI | Claude (Anthropic), solo lettura + proposte con approvazione, disattivabile |
| D6 | Ordine delle fasi | Come da roadmap (doc. 08), MVP negozio per primo |
| D7 | Modalità offline della cassa | Inclusa nella Fase 1 se la connessione non è affidabile |
| D8 | Lingua tecnica del codice | Codice in inglese tecnico, tutto ciò che vede l'utente in italiano |
