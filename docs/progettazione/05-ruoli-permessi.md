# 05 – Ruoli e autorizzazioni

## 1. Modello

- **RBAC** (controllo accessi basato su ruoli) con **permessi granulari** nel formato `modulo.azione` (es. `clienti.esporta`, `vendite.reso`, `campagne.approva`).
- Ruoli predefiniti modificabili; possibilità di creare ruoli personalizzati per azienda.
- Restrizioni aggiuntive per **sede** (un operatore può essere abilitato solo a un punto vendita).
- Regola dei **"quattro occhi"** configurabile: chi crea una campagna o un reso sopra soglia non può approvarlo da solo (salvo il Titolare se unico utente).
- I permessi sono controllati **sempre sul server**; l'interfaccia nasconde solo ciò che non è consentito.

## 2. Ruoli predefiniti

| Ruolo | Descrizione |
|---|---|
| **Titolare** | Accesso completo all'azienda; unico che può gestire utenti, impostazioni fiscali, esportazioni massive e cancellazioni GDPR |
| **Responsabile** | Gestione operativa completa, approvazioni ordinarie, nessuna gestione utenti né impostazioni critiche |
| **Addetto vendite** | Cassa, clienti (consultazione e inserimento), ordini clienti, WhatsApp in risposta |
| **Magazziniere** | Prodotti (consultazione), magazzino, ricevimento merce, inventari, scarti |
| **Marketing** | Segmenti, campagne (bozze), modelli messaggi, fedeltà; nessun invio senza approvazione |
| **Consulente contabile** | Sola lettura di report finanziari ed esportazioni contabili; nessun dato di marketing |
| **Amministratore piattaforma** | Gestione tecnica dei tenant; accesso ai dati aziendali solo con autorizzazione temporanea e tracciata del Titolare |

## 3. Matrice dei permessi (sintesi)

Legenda: **C** completo · **M** modifica · **L** lettura · **P** proposta (richiede approvazione) · **A** approvazione · — nessun accesso

| Area | Titolare | Responsabile | Addetto vendite | Magazziniere | Marketing | Consulente |
|---|---|---|---|---|---|---|
| Dashboard | C | C | L (propria cassa) | L (magazzino) | L (marketing) | L (finanziaria) |
| Clienti – consultazione | C | C | L | — | L | — |
| Clienti – modifica | C | M | M | — | M (etichette) | — |
| Clienti – esportazione | C | P | — | — | P | — |
| Clienti – cancellazione/anonimizzazione GDPR | C | P | — | — | — | — |
| Consensi – registrazione | C | M | M | — | L | — |
| Segmenti | C | M | — | — | M | — |
| Vendite – registrazione | C | M | M | — | — | — |
| Vendite – sconto oltre soglia | A | A | P | — | — | — |
| Vendite – reso/annullamento | A | A (sotto soglia) | P | — | — | — |
| Chiusura cassa | C | M | M (propria) | — | — | L |
| Prodotti e categorie | C | M | L | L | L | — |
| Prezzi e listini | C | M | L | L | P (promozioni) | — |
| Magazzino – movimenti | C | M | — | M | — | — |
| Magazzino – rettifiche inventario | A | A | — | P | — | — |
| Scarti | C | M | P | M | — | L |
| Ordini clienti | C | M | M | L | — | — |
| Ordini fornitori | A | M / A (sotto soglia) | — | P | — | L |
| Fornitori | C | M | — | L | — | L |
| WhatsApp – leggere/rispondere | C | M | M | — | M | — |
| WhatsApp – modelli | C | M | — | — | P | — |
| Campagne – creare | C | M | — | — | M | — |
| Campagne – approvare e inviare | A | A (se abilitato) | — | — | — | — |
| Fedeltà – regole | C | P | — | — | P | — |
| Fedeltà – rettifica punti | A | P | — | — | — | — |
| Recensioni e referral | C | M | L | — | M | — |
| Automazioni – creare/attivare | A | P | — | — | P | — |
| Assistente AI | C | C | L (dati di cassa) | L (magazzino) | L (marketing) | L (report) |
| Report finanziari | C | L | — | — | — | L |
| Esportazioni contabili | C | L | — | — | — | C |
| Utenti e ruoli | C | — | — | — | — | — |
| Impostazioni azienda/fiscali | C | L | — | — | — | — |
| Registro attività | L | L (proprio reparto) | — | — | — | — |

> L'assistente AI eredita **esattamente** i permessi dell'utente che lo interroga e non può mai superarli.

## 4. Operazioni sensibili (richiedono conferma umana)

Ogni voce passa dal modulo Approvazioni oppure da una conferma esplicita con riautenticazione.

| Operazione | Tipo di controllo |
|---|---|
| Invio di una campagna o di qualsiasi messaggio promozionale | Approvazione del Titolare/Responsabile abilitato |
| Attivazione di un'automazione che contatta clienti | Approvazione |
| Modifica massiva dei prezzi (es. > 10 prodotti o variazione > soglia %) | Approvazione |
| Reso o annullamento vendita sopra soglia | Approvazione |
| Sconto oltre soglia | Approvazione |
| Rettifica inventario oltre soglia | Approvazione |
| Ordine a fornitore oltre importo soglia | Approvazione |
| Esportazione di dati personali | Approvazione + riautenticazione + registro |
| Cancellazione/anonimizzazione cliente | Riautenticazione + doppia conferma |
| Rettifica manuale punti fedeltà | Approvazione |
| Modifica ruoli e permessi | Riautenticazione + 2FA |
| Modifica impostazioni fiscali (IVA, RT) | Riautenticazione + 2FA |
| Qualsiasi proposta dell'assistente AI | Approvazione |
| Accesso dell'assistenza tecnica ai dati | Autorizzazione temporanea del Titolare |

Le soglie sono configurabili dal Titolare nelle impostazioni.

## 5. Autenticazione

- Password con requisiti di lunghezza (min. 12 caratteri) e verifica contro elenchi di password compromesse; hash **Argon2id**.
- **Autenticazione a due fattori obbligatoria** per Titolare, Responsabile e Consulente; consigliata per gli altri (TOTP o passkey).
- **Accesso rapido in cassa**: sul tablet registrato come "dispositivo di cassa", gli addetti possono cambiare operatore con PIN personale, valido solo su quel dispositivo e solo per le funzioni di cassa.
- Sessioni con cookie sicuri (`HttpOnly`, `Secure`, `SameSite`), scadenza per inattività, revoca da remoto.
- Blocco progressivo dopo tentativi falliti; avviso al Titolare di accessi anomali.
