---
name: modalita
description: Switch della modalità operativa del sistema marketing Advisory+ — normale, ferie (riduzione/stop pianificato), crisi (blocco contenuti promozionali). Usalo prima di partire per ferie, durante eventi critici, o per riprendere dopo uno stop.
argument-hint: [normale | ferie | crisi] [opzionale: start_date end_date per ferie]
---

# /modalita — Switch modalità operativa

## Cosa fa

Cambia lo stato globale del sistema marketing. 3 modalità:

### 🟢 Modalità NORMALE
Default. Tutto attivo: publish · scheduled tasks · hook · Friday Email · Monday inbox check.

### 🌴 Modalità FERIE
Riduce o ferma temporaneamente con riattivazione automatica a end_date. Il CEO è OOO ma il sistema continua a respirare:
- **Light** (default): -50% volume contenuti · solo evergreen · no case study fresh · no commenti automatici
- **Full stop**: 0 publish · solo monitoring · email out-of-office on `marketing@advisoryplus.it`

### 🚨 Modalità CRISI
Blocca **tutti i contenuti promozionali**. Lascia attivi solo:
- Utility (es. comunicazioni clienti via email)
- Risposte/commenti già pianificati a brand mentions
- Monitoring e alert

Usata in caso di: incidente compliance · ispezione IVASS · crisi reputazionale · emergenza CEO.

## Sintassi

```
/modalita normale                                → torna a NORMALE
/modalita ferie 2026-08-08 2026-08-22            → ferie 8-22 agosto (default light)
/modalita ferie 2026-08-08 2026-08-22 full       → ferie full stop
/modalita crisi                                  → CRISI subito (no end_date, richiede ritorno esplicito)
/modalita crisi motivo="ispezione IVASS"         → CRISI con motivo loggato
```

## Skill innescata

`skills/process/safety/modalita/SKILL.md`

## Output

### Modalità FERIE light
```
🌴 MODALITÀ FERIE LIGHT ATTIVATA
─────────────────────────────────
Periodo: 8 ago - 22 ago 2026 (14gg)
Volume: -50% (da ~10/sett a ~5/sett)
Contenuti permessi: evergreen + already-scheduled
Contenuti bloccati: case study fresh · spunti CEO nuovi · annunci · commenti automatici
Auto-revert: 23 ago 2026 00:00 → MODALITÀ NORMALE

Email OOO: ✅ attivato su marketing@advisoryplus.it
Friday Email durante ferie: ✅ inviata regolarmente (CEO può rispondere o silent approval)
Monday inbox check: ✅ continua
```

### Modalità CRISI
```
🚨 MODALITÀ CRISI ATTIVATA
─────────────────────────────────
Motivo: [se fornito]
Timestamp: 2026-05-18 21:00
Auto-revert: NO (richiede /modalita normale esplicita)

Bloccati IMMEDIATAMENTE:
- 7 contenuti in coda settimana corrente
- 2 contenuti scheduled W22
- Friday Email piano automatico

Permessi:
- Risposte già programmate a brand mentions
- Email utility a clienti
- Monitoring

Compliance Officer in modalità HIGH ALERT (semaforo solo 🟢 passa, 🟡 → 🔴 implicito).
```

## Comportamento

- **Auto-revert ferie**: scheduled-task MCP imposta cron alla `end_date+1` per flip back a NORMALE
- **Crisi NO auto-revert**: scelta esplicita del CEO (cautela)
- **Loga in Verbale** sessione + email notifica
- **Backup piano**: snapshot prima del switch, per eventuale ripristino
- **Compliance Officer alert level**: cambia con la modalità

## Email subject equivalent

- `MODALITÀ FERIE 2026-08-08 2026-08-22` → equivalente `/modalita ferie 2026-08-08 2026-08-22`
- `MODALITÀ CRISI` → equivalente `/modalita crisi`
- `MODALITÀ NORMALE` → equivalente `/modalita normale`

## Visibilità

Lo stato corrente è sempre visibile in `/stato` (prima riga):
```
📊 ADVISORY+ STATO 7gg [🌴 FERIE LIGHT fino 22 ago]
```

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
