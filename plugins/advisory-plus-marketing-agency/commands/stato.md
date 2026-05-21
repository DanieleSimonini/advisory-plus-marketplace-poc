---
name: stato
description: Stampa lo stato sintetico del sistema marketing Advisory+ negli ultimi 7 giorni — pubblicato, skippato, pending CEO, alert, scadenze token, KPI essenziali. Usalo ogni volta che vuoi un colpo d'occhio senza scrollare verbali.
argument-hint: (nessuno)
---

# /stato — Snapshot 7gg sistema marketing

Quando vieni invocato con `/stato`, esegui SUBITO le istruzioni qui sotto. **READ-ONLY** — non scrivere nulla.

## Step 1 — Leggi le 5 fonti di stato

Tutte le fonti vivono in:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\04_Risorse\Stato_Sistema\
```

File da leggere (usa Read tool per ciascuno, gestisci graziosamente se non esiste):

| File | Cosa contiene | Comportamento se manca |
|---|---|---|
| `modalita.json` | Stato modalità corrente (normale/ferie/crisi) | Considera `normale` di default |
| `tokens.json` | Scadenze token API (Meta/Brevo/HeyGen/LinkedIn/Buffer/WordPress) | Sezione "Token API" → "(nessun tracking attivo)" |
| `log_pubblicazioni.jsonl` | Append-only log pubblicazioni (1 JSON per riga: `{date, channel, status, item_id, pillar}`) | "(nessuna pubblicazione registrata)" |
| `piano_corrente.json` | Piano settimana corrente con array `items[]` (ognuno `{id, channel, date, status: pending|published|skipped|stopped, title, pillar}`) | "(nessun piano caricato)" |
| `pending_ceo.jsonl` | Azioni pending sul CEO (append-only `{date, action, severity, deadline}`) | "(nessuna pendenza)" |

## Step 2 — Calcola gli aggregati

Finestra temporale: **ultimi 7 giorni** dalla data odierna (env).

Per ogni metrica:

### Pubblicato 7gg
Conta entry in `log_pubblicazioni.jsonl` con `status=published` e `date >= oggi-7gg`. Raggruppa per canale (LinkedIn brand, LinkedIn Daniele, Instagram, Facebook, Blog, YouTube, Newsletter Brevo).

### Skippato 7gg
Conta entry con `status=skipped` o `status=stopped` negli ultimi 7gg.

### Pending CEO
Conta righe in `pending_ceo.jsonl` con `deadline >= oggi` OR `deadline` mancante. Mostra le 3 più urgenti (deadline crescente).

### Alert
Combina:
- Item in `piano_corrente.json` con `status=pending` e `date < oggi` → "Item in ritardo"
- Token in `tokens.json` con scadenza entro 7gg → "Token in scadenza"
- Modalità in `modalita.json` != normale → mostra modalità attiva

### Scadenze token
Per ogni voce in `tokens.json`, calcola giorni residui (`expires_at - oggi`). Se ≤ 7 → 🔴, ≤ 30 → 🟡, > 30 → 🟢.

### KPI essenziali
- Volume settimana: numero pubblicazioni 7gg vs target (default 7/sett)
- Compliance pass rate: % entry con `compliance=green` / totali (se campo presente)
- Pending CEO open: numero pendenze aperte

## Step 3 — Output formato dashboard

Mostra esattamente questo blocco (sostituisci i valori). Usa `—` per metriche senza dato.

```
═══════════════════════════════════════════════════
ADVISORY+ STATO SISTEMA · 7gg al [oggi formato IT]
[se modalita != normale: aggiungi "[🌴 FERIE LIGHT fino DD mmm]" o "[🚨 CRISI dal DD mmm]"]
═══════════════════════════════════════════════════

📤 PUBBLICATO 7gg ([totale] item)
  LinkedIn brand:    [N] · LinkedIn Daniele: [N]
  Instagram:         [N] · Facebook:         [N]
  Blog THE ADVISOR:  [N] · YouTube:          [N]
  Newsletter Brevo:  [N]

🚫 SKIPPATO/STOPPATO 7gg: [N]
  [se >0, lista breve: "- [item] (motivo)"]

⏳ PENDING CEO ([N] aperte, top 3)
  1. [action] · scade [deadline o "—"]
  2. ...
  3. ...

🚨 ALERT ([N])
  - [alert 1]
  - [alert 2]

🔑 SCADENZE TOKEN
  Meta:      [giorni] gg [🟢🟡🔴]
  Brevo:     [giorni] gg [🟢🟡🔴]
  HeyGen:    [giorni] gg [🟢🟡🔴]
  LinkedIn:  [giorni] gg [🟢🟡🔴]
  Buffer:    [giorni] gg [🟢🟡🔴]
  WordPress: [giorni] gg [🟢🟡🔴]

📊 KPI 7gg
  Volume:        [N]/7 ([%] vs target)
  Compliance:    [%] verde
  Pending CEO:   [N] aperte

═══════════════════════════════════════════════════
Per cambiare modalità: command modalita [normale|ferie|crisi]
```

## Vincoli di stile

- **NO scrittura su nessun file** — è solo READ
- **NO domande di follow-up** — output e basta
- **NO uso di tool Skill** — self-contained
- **Lunghezza output: ~30-40 righe massimo** (formato fisso)
- Se TUTTE le fonti mancano: mostra blocco con valori `(nessun dato)` invece di errore, e chiudi con "Sistema appena inizializzato — i dati popoleranno con le prime pubblicazioni."

## Edge case

Se i file JSON sono malformati: NON crashare, segnala in alert: "🟡 [nome_file] JSON malformato — riportare al MM".

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained, READ-ONLY.*
