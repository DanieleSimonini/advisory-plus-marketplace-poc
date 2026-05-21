---
name: piano-settimana
description: Genera ON DEMAND il Friday Email del piano editoriale settimanale di Advisory+. Usalo quando vuoi anticipare il piano (non aspettare venerdì 18:00) o quando devi rilanciare dopo un cambio strategico.
argument-hint: [opzionale: "+1 settimana" per piano della prossima | "questa" per settimana corrente | default: prossima]
---

# /piano-settimana — Friday Email piano editoriale on demand

Quando vieni invocato con `/piano-settimana $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. Generi un piano editoriale settimanale completo in formato Friday Email.

## Step 1 — Calcola la settimana target

Default: **prossima settimana** (lunedì-domenica successivi alla data odierna).

| `$ARGUMENTS` | Settimana target |
|---|---|
| (vuoto) o `+1 settimana` o `prossima` | Lunedì-Domenica della settimana successiva |
| `questa` o `corrente` | Lunedì-Domenica della settimana corrente |
| `+2 settimane` | Settimana dopo la prossima |
| Data `YYYY-MM-DD` | Settimana che contiene quella data |

Output: `Wxx [data lunedì] → [data domenica]` (es. `W22 25 mag → 31 mag 2026`).

## Step 2 — Leggi le fonti

Path base:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\
```

File da leggere (gestisci graziosamente se mancano):

| File | Cosa serve |
|---|---|
| `00_Brand_Book_v1.1.md` (o ultimo Brand Book disponibile) | Pillar map sez. 6 + 6bis · Voci sez. 4 · Pillar of month sez. 7 |
| `05_Calendario_editoriale/Spunti_CEO.md` | Sezione "📋 DA TRATTARE" → input grezzi del CEO da integrare |
| `05_Calendario_editoriale/2026-MM_*.md` (mese corrente o target) | Piano editoriale mensile esistente — eventuali item già pianificati |
| `04_Risorse/Stato_Sistema/modalita.json` | Se ferie → riduci -50% volume · Se crisi → solo utility · Se normale → volume pieno |
| `04_Risorse/Stato_Sistema/piano_corrente.json` | Item già esistenti per la settimana target (per evitare duplicati) |

## Step 3 — Pillar mix della settimana

Default mix per settimana (7-10 contenuti totali su 7 canali):

- **Pillar 1 La famiglia che protegge** (TCM + Tutela Legale privati) — 2 contenuti
- **Pillar 2 Il dopo di noi, il dopo di loro** (LTC) — 2 contenuti
- **Pillar 3 Risparmio sensato** (Previdenza) — 1 contenuto
- **Pillar 4 Tutela legale invisibile** (UCA + DAS) — 1 contenuto
- **Pillar 5 Territorio Advisory+** — 1 contenuto evergreen

Se `modalita.json` indica un `pillar_of_month` attivo (Brand Book sez. 7), DOMINA il mix di quella settimana: 3 contenuti su quel pillar.

Se il CEO ha lasciato `[push]` spunti che indicano pillar dominante → applica.

## Step 4 — Allocazione canale × giorno

Schema base (modificabile se piano corrente già pieno):

| Giorno | Canale principale | Canale secondario | Voce |
|---|---|---|---|
| Lunedì | LinkedIn brand | — | 🧠 Spiegato Facile |
| Martedì | Instagram + Facebook | — | 📖 Caso Reale |
| Mercoledì | Blog THE ADVISOR | LinkedIn brand (snippet) | 🧠 Spiegato Facile o 📊 Analisi |
| Giovedì | LinkedIn Daniele personale | — | Voce CEO (Brand Book sez. 4) |
| Venerdì | Newsletter Brevo | LinkedIn brand | mix |
| Sabato | Instagram Stories | — | breve |
| Domenica | — (silenzio) | — | — |

## Step 5 — Integra spunti CEO non trattati

Leggi `## 📋 DA TRATTARE` in `Spunti_CEO.md`. Per ogni spunto non ancora archiviato:
- Se compatibile con un contenuto pianificato → lo cita come ispirazione ("ispirato da spunto CEO [data]: ...")
- Se merita un contenuto dedicato → aggiungi item al piano
- Se è `[veto]` → marca relativi item come "VETO CEO" da ripianificare
- Se è `[push]` → modifica il mix pillar di conseguenza

## Step 6 — Big Bets (max 5/settimana)

Identifica i `Big Bets` della settimana (decisioni che richiedono OK esplicito CEO, vedi MM Decision Authority Framework Brand Book sez. 13):
- Nuova pillar / sotto-pillar
- Campagna budget >€300
- Crisis comms
- Post profilo Daniele Simonini (Voce CEO)
- Contenuti 🟡 borderline Compliance
- Modifica Brand Book
- Spostamento pillar-of-month
- Attivazione nuovo canale
- Partnership esterne

Massimo 5 per settimana. Se ce ne sono più di 5, scegli i 5 più rilevanti e segna gli altri come "Backlog".

## Step 7 — Punti di esitazione (solo Trust Calibration Window)

Se siamo nel periodo `16 mag 2026 → 16 giu 2026` (Trust Calibration Window, vedi Brand Book sez. 13): includi max **3 Punti di esitazione** — decisioni che il MM ha preso ma su cui vuole il check del CEO.

Formato: "ESITAZIONE #N: [decisione] — Motivazione: [perché esita]"

Dopo il 16 giu 2026: ometti questa sezione.

## Step 8 — Output: Friday Email completa

Formato esatto:

```
═══════════════════════════════════════════════════
📧 FRIDAY EMAIL · PIANO EDITORIALE [Wxx]
[data lunedì] → [data domenica]
[se modalità non normale: "[🌴 FERIE LIGHT — volume ridotto -50%]" o "[🚨 CRISI — solo utility]"]
═══════════════════════════════════════════════════

📅 PIANO SETTIMANA

Lun [DD/MM] · LinkedIn brand
  Titolo: [titolo]
  Pillar: [P1-P5] · Voce: [🧠📖🔥📊]
  Owner: Copywriter
  Status: [pending|draft|ready]

Mar [DD/MM] · Instagram + Facebook
  Titolo: [titolo]
  Pillar: [P1-P5] · Voce: [voce]
  Owner: Copywriter + Art Director
  Status: [...]

[ripeti per Mer, Gio, Ven, Sab, Dom]

📌 BIG BETS ([N] richiedono OK esplicito CEO)

1. [titolo bet] · scade [DD/MM]
   Perché Big Bet: [motivazione MM Decision Authority]
   Costo/Impatto: [stima]

[ripeti fino a max 5]

💡 SPUNTI CEO TRATTATI ([N])

- [data] [tag] [spunto sintetico] → integrato in [item del piano]
[ripeti]

[SE Trust Calibration Window attiva:]
🤔 PUNTI DI ESITAZIONE ([max 3])

1. ESITAZIONE: [decisione presa]
   Motivazione MM: [perché esita]
   Richiesta CEO: [Conferma | Veto | Modifica]

[ripeti fino a max 3]

═══════════════════════════════════════════════════
🟢 Silent Approval Window: 48h dal ricevimento (= [data+48h])
   Routine: via libera tacito
   Big Bets: richiedono OK esplicito anche dopo 48h
═══════════════════════════════════════════════════

[opzionale, se in NL evocato]
Vuoi aggiustare qualcosa? Rispondi "veto #N" o "modifica #N [come]".
```

## Vincoli di stile

- **READ-ONLY su file** — non salvare il piano in alcun file (è una proposta in attesa di OK CEO)
- **Voce: Marketing Manager** (sintetica, decisionale, operativa)
- **NO uso di tool Skill** — self-contained
- **Lunghezza output: 60-100 righe** (è il piano della settimana, non un riassunto)
- **NO domande aperte sul contenuto** — proponi e basta, il CEO decide via veto/modifica/silent approval

## Edge case

- Se `Spunti_CEO.md` ha 0 spunti DA TRATTARE: mostra sezione "💡 SPUNTI CEO TRATTATI" con "(nessuno spunto in coda — settimana basata su pillar mix standard)"
- Se modalità = crisi: il piano è SOLO utility (no contenuti promozionali) e tutti gli item sono marcati `BLOCCATO CRISI` con sola mention del backlog
- Se data fuori range plausibile (es. > 6 mesi avanti): mostra errore e fermati

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained.*
