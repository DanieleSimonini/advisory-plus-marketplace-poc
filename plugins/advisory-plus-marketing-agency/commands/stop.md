---
name: stop
description: Kill switch del sistema marketing Advisory+. Ferma un singolo item del piano (/stop #N) o disattiva l'intera automazione (/stop tutto). Effetto immediato, irreversibile salvo riattivazione esplicita.
argument-hint: [#N per singolo item | "tutto" per kill switch globale]
---

# /stop — Kill switch CEO

## Cosa fa

Interrompe esecuzione di contenuti pianificati. Due modalità:

### Modalità 1 — `/stop #N`
Stoppa il singolo item numero `N` del piano settimanale corrente. NON tocca gli altri.

### Modalità 2 — `/stop tutto`
**Kill switch globale.** Flip `config/AUTOMAZIONE_ATTIVA=false`. Blocca:
- Ogni publish automatico
- Ogni scheduled-task (cron)
- Ogni hook automatico
- Friday Email automatica

NON blocca:
- Chat operative (il CEO può ancora chattare col MM)
- Lettura/scrittura file
- Compliance checks on-demand

## Sintassi

```
/stop #3                → stoppa item #3 del piano corrente
/stop #3,#5,#7          → stoppa multipli item
/stop tutto             → kill switch globale
/stop tutto motivo=crisi → kill switch con motivo loggato
```

## Skill innescata

`skills/process/safety/stop/SKILL.md`

## Output

### `/stop #N`
```
🛑 STOP #3 ricevuto.
Item: "mer 20 mag 18:00 Blog THE ADVISOR — LTC il numero che cambia"
Status: bloccato (non sarà pubblicato)
Loggato in: /03_Aree_di_lavoro/01_Strategia/Verbale.md → STATO ATTUALE
Effetto: immediato.
```

### `/stop tutto`
```
🛑🛑🛑 KILL SWITCH GLOBALE ATTIVATO
─────────────────────────────────
AUTOMAZIONE_ATTIVA = false (era: true)
Timestamp: 2026-05-18 19:32
Motivo: [se fornito]

Bloccati:
- 0 publish in coda nei prossimi 7gg
- 5 scheduled tasks (Friday Email · Monday inbox · daily check · token refresh · weekly report)
- 2 hook automatici

Per riattivare: /modalita normale
```

## Comportamento

- **Conferma sempre cosa è stato bloccato** (item title, scheduled tasks, hook)
- **Loga in Verbale** con timestamp e motivo (se fornito)
- **Backup snapshot piano** prima di stop (per eventuale rollback)
- **Notifica via email** (se SMTP attivo) al CEO con riepilogo
- **NON disattiva la chat** — il CEO può sempre intervenire

## Riattivazione

Solo via `/modalita normale` (slash command separato). Non c'è "/start tutto" — la scelta è esplicita per evitare riattivazioni accidentali.

## Email subject equivalent

In modalità email (rispondi con subject specifico al Friday Email):
- `STOP #3` → equivalente `/stop #3`
- `STOP TUTTO` → equivalente `/stop tutto`

(skill `process/strategia/week-mon` parsea l'inbox lun 06:00)

## Compliance

L'hook `pre-publish-compliance` NON è il kill switch. Quello blocca contenuti non conformi; questo è una scelta strategica del CEO.

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
