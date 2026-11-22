# 06 – Proposta grafica e struttura della navigazione

## 1. Principi di design

1. **Velocità prima dell'estetica in cassa**: pulsanti grandi (min. 48 px), massimo 3 tocchi per una vendita semplice.
2. **Chiarezza**: un'azione principale per schermata, linguaggio commerciale italiano semplice.
3. **Trasparenza sui dati**: ogni numero ha periodo e fonte; i dati dimostrativi hanno un banner arancione fisso **"DATI DIMOSTRATIVI – non reali"**.
4. **Accessibilità** WCAG 2.2 AA: contrasto, navigazione da tastiera, testi alternativi.
5. **Predisposizione RTL**: layout costruito con proprietà logiche CSS (inizio/fine anziché sinistra/destra) per l'arabo.
6. **Coerenza**: un unico sistema di componenti per tutti i moduli.

## 2. Identità visiva proposta (da validare con il committente)

| Elemento | Proposta |
|---|---|
| Colore primario | Verde foglia `#2E7D32` (freschezza, ortofrutta) |
| Colore secondario | Arancio agrume `#F57C00` (azioni promozionali, evidenze) |
| Neutri | Grigi caldi per sfondi e testi; sfondo chiaro predefinito |
| Stati | Successo verde, avviso ambra, errore rosso `#C62828`, informazione blu |
| Tema scuro | Disponibile, utile per il retro negozio |
| Caratteri | **Inter** (interfaccia), cifre tabellari per importi; **Noto Sans Arabic** per l'arabo |
| Icone | Set lineare coerente (Lucide) |
| Logo | Da fornire dal committente (vedi domande aperte) |

I colori sono gestiti come variabili: ogni azienda futura potrà avere il proprio marchio.

## 3. Struttura della navigazione

Barra laterale su desktop/tablet orizzontale, menu inferiore su smartphone con le 4 voci più usate + "Altro".

```
CRM IBRA                                   [🔍 Cerca ovunque]  [🔔]  [Approvazioni (3)]  [Profilo ▾]
│
├── 🏠 Cruscotto
│
├── VENDITA
│   ├── 🛒 Cassa
│   ├── 🧾 Vendite e resi
│   └── 💶 Chiusura cassa
│
├── CLIENTI
│   ├── 👥 Clienti
│   ├── 🎯 Segmenti
│   ├── ⭐ Fedeltà
│   ├── ↩️ Recupero clienti
│   └── 💬 Recensioni e referral
│
├── COMUNICAZIONE
│   ├── 🟢 WhatsApp
│   └── 📣 Campagne
│
├── MERCE
│   ├── 🥕 Prodotti e listini
│   ├── 📦 Magazzino
│   ├── 📋 Ordini clienti
│   ├── 🚚 Ordini fornitori
│   └── 🏭 Fornitori
│
├── ANALISI
│   ├── 📈 Performance
│   ├── 📊 Report
│   └── ✨ Assistente AI
│
└── SISTEMA
    ├── ⚙️ Automazioni
    ├── ✅ Approvazioni
    ├── 🔐 Utenti e ruoli
    ├── 📜 Registro attività
    ├── 🛡️ Privacy e consensi
    └── 🏪 Impostazioni azienda
```

Le voci visibili dipendono dal ruolo: l'Addetto vendite vede principalmente Cassa, Clienti, Ordini clienti e WhatsApp.

## 4. Schermate chiave

### 4.1 Cruscotto (Titolare)

```
┌───────────────────────────────────────────────────────────────────────┐
│ Oggi, sabato 22 novembre · aggiornato alle 11:42                      │
├──────────────┬──────────────┬──────────────┬──────────────────────────┤
│ Incasso      │ Scontrini    │ Scontrino    │ Clienti identificati     │
│ € —          │ —            │ medio € —    │ — %                      │
│ vs sab. scorso│             │              │                          │
├──────────────┴──────────────┴──────────────┴──────────────────────────┤
│ ⚠ Avvisi: 4 lotti da vendere entro domani · 2 prodotti sotto scorta  │
│           1 ordine fornitore in arrivo · 5 messaggi WhatsApp non letti│
├───────────────────────────────────┬───────────────────────────────────┤
│ Vendite per ora (grafico)         │ Prodotti più venduti (oggi)       │
├───────────────────────────────────┼───────────────────────────────────┤
│ Approvazioni in attesa (3)        │ Suggerimenti dell'assistente AI   │
└───────────────────────────────────┴───────────────────────────────────┘
```

I valori "—" indicano l'assenza di dati: il sistema non mostra mai numeri inventati.

### 4.2 Cassa (tablet orizzontale)

```
┌──────────────────────────────────────────────┬────────────────────────┐
│ [🔍 Cerca prodotto o PLU]   [📷 Codice]      │ Cliente: [+ Associa]   │
├──────────────────────────────────────────────┤────────────────────────│
│ Preferiti / Categorie                        │ Pomodori ramati        │
│ ┌──────┐┌──────┐┌──────┐┌──────┐┌──────┐     │ 1,250 kg × 2,90 = 3,63 │
│ │Mele  ││Banane││Pomod.││Patate││Insal.│     │ Banane                 │
│ └──────┘└──────┘└──────┘└──────┘└──────┘     │ 0,980 kg × 1,80 = 1,76 │
│ ┌──────┐┌──────┐┌──────┐┌──────┐┌──────┐     │                        │
│ │Arance││Limoni││Zucch.││Carote││Funghi│     │ ───────────────────    │
│ └──────┘└──────┘└──────┘└──────┘└──────┘     │ Totale         € 5,39  │
├──────────────────────────────────────────────┤ [Sconto] [Sospendi]    │
│ Peso: 0,000 kg  [Tara]  [Inserisci a mano]   │ [   PAGAMENTO   ]      │
└──────────────────────────────────────────────┴────────────────────────┘
```
(Prezzi nell'esempio puramente illustrativi.)

### 4.3 Scheda cliente

Intestazione con nome, telefono, stato consensi (icone verdi/grigie per servizio, marketing, profilazione), saldo punti, segmento RFM. Schede: **Panoramica · Acquisti · Ordini · Messaggi · Fedeltà · Note · Privacy**.

### 4.4 Approvazioni

Elenco con tipo, richiedente (persona o "Assistente AI"), riepilogo, impatto (es. "invio a 142 clienti con consenso, 18 esclusi"), pulsanti **Approva** / **Rifiuta con motivazione** / **Dettagli**.

### 4.5 Assistente AI

Pannello di conversazione con: domanda, risposta, sezione "**Dati consultati**", eventuali proposte con pulsante "**Invia per approvazione**". Avviso permanente: *"Le risposte dell'assistente possono contenere errori. Nessuna azione viene eseguita senza la tua conferma."*

## 5. Messaggi e testi dell'interfaccia (esempi di tono)

| Situazione | Testo |
|---|---|
| Salvataggio riuscito | "Cliente salvato correttamente." |
| Errore di validazione | "Il numero di telefono non è valido. Inserisci il prefisso internazionale, ad esempio +39." |
| Permesso mancante | "Non hai l'autorizzazione per questa operazione. Contatta il titolare." |
| Consenso mancante | "Questo cliente non ha dato il consenso a ricevere offerte su WhatsApp." |
| Approvazione richiesta | "Operazione inviata per approvazione. Riceverai una notifica appena sarà valutata." |
| Connessione assente | "Connessione assente. Le vendite vengono salvate sul dispositivo e inviate appena possibile." |
| Dati insufficienti | "Dati non sufficienti per calcolare questo indicatore nel periodo selezionato." |

## 6. Responsive

| Dispositivo | Adattamento |
|---|---|
| Smartphone | Menu inferiore, schede a lista, azioni rapide (consultare cliente, rispondere su WhatsApp, vedere incasso) |
| Tablet | Cassa a due colonne, inventario guidato, ricevimento merce |
| Desktop | Tabelle complete, report, configurazioni |
