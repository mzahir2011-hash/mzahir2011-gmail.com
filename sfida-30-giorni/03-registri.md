# 03 · Registri

Tutti i registri sono nel **cruscotto** (`cruscotto.html`). Qui è descritta la loro struttura, così i dati restano consultabili anche fuori dal cruscotto (esportazione JSON in Impostazioni).

## 1. Registro centrale delle attività (una scheda per giorno)

| Campo | Contenuto |
|-------|-----------|
| 3 priorità | testo + stato: ✓ completata · ◐ parziale · ✗ non completata |
| Corano | memorizzazione (quantità + da/a), ripasso (pagine), lettura (pagine), adhkār mattina e sera |
| Formazione | ore + testo/capitolo |
| Specializzazione | ore + testo/capitolo |
| Lettura | pagine + libro |
| Ore istituzionali | Al-Tarbal (ore), Al-Jisr (ore) — separate dallo studio |
| Salute e famiglia | sport (min), sonno (ore), famiglia (min), figli (min) |
| Preghiere | Fajr, Dhuhr, Asr, Maghrib, Isha: a casa / in moschea |
| Ostacoli e note | testo libero |
| Priorità di domani | 3 righe (proposte in automatico: attività non completate + piano del giorno dopo) |

## 2. Registro Al-Tarbal (1.500 confezioni)

**Inventario per titolo** — compilato con il conteggio fisico dei giorni 1–3:

| Titolo / confezione | Quantità contata | Prezzo unitario (€) |
|---------------------|------------------|---------------------|

Controllo automatico: la somma delle quantità deve coincidere con 1.500; in caso contrario il cruscotto segnala la differenza.
Un modello stampabile per il conteggio è in [`registri/tarbal-inventario.csv`](registri/tarbal-inventario.csv).

**Registro vendite** — una riga per vendita:

| Data | Cliente | Nuovo cliente | Titolo | Quantità | Importo (€) | Incassato | Note |
|------|---------|---------------|--------|----------|-------------|-----------|------|

## 3. Inventario iniziale delle attività Al-Jisr

Elenco delle 28 attività dei 4 progetti (con scadenza): visibile e spuntabile nella scheda **Al-Jisr** del cruscotto.

| Progetto | Attività | Scadenza |
|----------|----------|----------|
| P1 Ricevute | modello · numerazione · collegamento studente/pagamento · archivio e storico · prova con 5 ricevute | 24–27/11 |
| P2 Contabilità e lezioni | studenti · insegnanti · calendario · presenze · contabilità · report · prova completa | 30/11–06/12, verifica 18/12 |
| P3 Campagna | pubblico · piano · contenuti AR · contenuti IT · immagini/video · canali · lancio · monitoraggio | 07–16/12 |
| P4 Iscritti | situazione iniziale · registro richieste · risposte · prove · conversione · richiami · misura settimanale | 28/11–19/12 |

Prima di costruire, la sessione di avvio deve chiarire **cosa esiste già** (vedi 04): sul tuo account c'è già una procedura per le ricevute «وصل أداء» e le richieste «طلب أداء» collegata a un registro Excel dell'istituto. Se è già in uso, il Progetto 1 parte da lì (numerazione e archivio) invece che da zero.

**Registro richieste / potenziali iscritti** — una riga per persona:

| Data | Nome | Canale | Corso / note | Stato | Prossimo contatto | Quota (€) |
|------|------|--------|--------------|-------|-------------------|-----------|

Stati: Nuova richiesta → Contattato → Lezione di prova → **Iscritto** / Non interessato. Il cruscotto evidenzia i richiami scaduti.
