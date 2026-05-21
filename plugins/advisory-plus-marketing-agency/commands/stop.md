---
name: stop
description: Kill switch del sistema marketing Advisory+. Ferma un singolo item del piano (/stop #N) o disattiva l'intera automazione (/stop tutto). Effetto immediato, irreversibile salvo riattivazione esplicita.
argument-hint: [#N per singolo item | "tutto" per kill switch globale | "riattiva" per riattivare]
---

# /stop — Kill switch sistema marketing

Quando vieni invocato con `/stop $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. **WRITE su filesystem** — effetto immediato.

## Step 1 — Parse argomenti

`$ARGUMENTS` deve essere uno tra:

| Pattern | Azione |
|---|---|
| `#N` (es. `#3`, `#42`) | Stop singolo item con id N nel `piano_corrente.json` |
| `tutto` | Kill switch globale: disattiva intera automazione (flag `automation_active=false`) |
| `riattiva` | Riattiva sistema dopo `/stop tutto` (flag `automation_active=true`) |
| (vuoto) o altro | Mostra errore + sintassi e fermati |

Se errore:

```
❌ Sintassi non valida.

Sintassi:
/stop #N          → stoppa singolo item piano (es. /stop #3)
/stop tutto       → kill switch globale, disattiva automazione
/stop riattiva    → riattiva sistema dopo kill switch globale

Per stato corrente: /stato
Per cambiare modalità (ferie/crisi): command modalita
```

## Step 2 — Localizza i file di stato

Path base:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\04_Risorse\Stato_Sistema\
```

File coinvolti:
- `piano_corrente.json` (per stop item singolo)
- `automation_state.json` (per kill switch globale)

Crea cartella o file vuoti se mancano.

## Step 3a — CASO "stop #N" (singolo item)

1. Read `piano_corrente.json`. Schema atteso:
   ```json
   {
     "settimana": "Wxx YYYY-MM-DD/YYYY-MM-DD",
     "items": [
       {"id": 1, "channel": "...", "date": "ISO", "status": "pending|published|skipped|stopped", "title": "...", "pillar": "..."}
     ]
   }
   ```
2. Cerca item con `id == N`.
3. Se NON trovato → mostra errore:
   ```
   ❌ Item #N non trovato nel piano corrente.
   Verifica con: command stato
   ```
4. Se trovato:
   - Aggiorna `status` a `stopped`
   - Aggiungi campo `stopped_at` (timestamp ISO)
   - Aggiungi campo `stopped_by` = `CEO via /stop`
   - Write `piano_corrente.json`
5. Append entry a `pending_ceo.jsonl`:
   ```json
   {"date": "ISO", "action": "Item #N stoppato — valutare se ripianificare", "severity": "info"}
   ```

Output:

```
🛑 ITEM #N STOPPATO

Titolo: [title]
Canale: [channel]
Data prevista: [date]
Pillar: [pillar]

✅ Status aggiornato a `stopped` in piano_corrente.json
✅ Pending CEO: "ripianificare?" registrato per Friday Email

Per riattivarlo: chiedi al MM "riattiva item #N" oppure modifica manuale piano.
```

## Step 3b — CASO "stop tutto" (kill switch globale)

1. Read `automation_state.json` (o crea con default se manca):
   ```json
   {
     "automation_active": true,
     "stopped_at": null,
     "stopped_by": null,
     "stopped_reason": null
   }
   ```
2. Aggiorna:
   - `automation_active` = `false`
   - `stopped_at` = timestamp ISO corrente
   - `stopped_by` = `CEO via /stop tutto`
   - `stopped_reason` = `"(non specificato)"` (CEO può aggiornare a mano)
3. Write `automation_state.json`
4. Append entry critica a `pending_ceo.jsonl`:
   ```json
   {"date": "ISO", "action": "SISTEMA SPENTO — richiesta riattivazione esplicita", "severity": "critical"}
   ```

Output:

```
🚨🚨🚨 KILL SWITCH GLOBALE ATTIVATO

Sistema marketing Advisory+ DISATTIVATO dal: [timestamp IT]

Effetto immediato:
- Tutti gli item `pending` nel piano corrente: SOSPESI (status invariato ma non eseguiti)
- Scheduled task automatici: NON eseguiti dal prossimo trigger
- Hook pre-publish: BLOCCO
- Friday Email automatica: NON inviata
- Monitoring (oncall) e Compliance Officer alert: rimangono ATTIVI

Per riattivare: command stop riattiva

⚠️ Questa è azione critica — registrata in pending_ceo.jsonl con severity=critical.
```

## Step 3c — CASO "stop riattiva" (uscita dal kill switch)

1. Read `automation_state.json`.
2. Se `automation_active` è già `true`:
   ```
   ℹ️ Sistema già attivo. Nessuna azione.
   ```
3. Se `automation_active` è `false`:
   - `automation_active` = `true`
   - `restarted_at` = timestamp ISO corrente
   - `restarted_by` = `CEO via /stop riattiva`
   - (Lascia campi `stopped_*` come storico, non azzerare)
4. Write `automation_state.json`
5. Append entry a `pending_ceo.jsonl`:
   ```json
   {"date": "ISO", "action": "Sistema riattivato — verifica piano corrente prima di pubblicare", "severity": "info"}
   ```

Output:

```
✅ SISTEMA RIATTIVATO

Marketing Advisory+ tornato in modalità attiva dal: [timestamp IT]
(Era spento da: [stopped_at IT] · Motivo: [stopped_reason])

Prima del prossimo publish ti consiglio:
1. command stato → verifica scheduled task e item pending
2. command modalita → conferma sia normale (non ferie/crisi)
3. command piano-settimana → verifica piano corrente
```

## Vincoli di stile

- **Effetto immediato** — write subito, nessuna conferma
- **NO domande di follow-up** — write e basta, output asciutto
- **NO uso di tool Skill** — self-contained
- **Output adattivo per caso**: stop singolo ~10 righe, stop tutto ~15 righe, riattiva ~8 righe
- **Mai dimenticare** di scrivere su `pending_ceo.jsonl` per audit trail

## Edge case

- Piano corrente JSON malformato → NON modificare, mostra "🟡 piano_corrente.json malformato, intervieni a mano"
- `/stop tutto` quando sistema già spento → mostra "ℹ️ Sistema già spento dal [data]. Per riattivare: command stop riattiva"
- File `Stato_Sistema/` non writable (permessi) → mostra errore con percorso file e fermati

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained, WRITE-CRITICAL.*
