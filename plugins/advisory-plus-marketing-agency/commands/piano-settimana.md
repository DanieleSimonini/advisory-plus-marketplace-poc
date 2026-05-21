---
name: piano-settimana
description: Genera ON DEMAND il Friday Email del piano editoriale settimanale di Advisory+. Usalo quando vuoi anticipare il piano (non aspettare venerdì 18:00) o quando devi rilanciare dopo un cambio strategico.
argument-hint: [opzionale: "+1 settimana" per piano della prossima | "questa" per settimana corrente | default: prossima]
---

# /piano-settimana — Friday Email on demand

## Cosa fa

Esegue la skill `process/strategia/week-fri` fuori cadenza (cron automatico = ven 18:00). Genera il piano editoriale completo della settimana target con:

- 7-12 contenuti pianificati (multi-canale: LinkedIn personale Daniele · LinkedIn brand · IG · FB · Blog · YouTube se attivo)
- Per ogni contenuto: pillar · voce · canale · giorno · ora · ToV · brief sintetico (50-80 parole)
- Numerazione `#1`-`#N` per permettere comandi successivi (`/stop #3`, `MODIFICA #5`)
- Compliance pre-check 🟢🟡🔴 su ogni item
- Footer con summary: capitale tempo CEO richiesto · capitale tempo MM automatizzato

## Sintassi

```
/piano-settimana                  → piano settimana prossima (default)
/piano-settimana +1               → piano settimana W+1 (avanti di 1)
/piano-settimana questa           → piano settimana corrente (rare: in caso di emergenza)
/piano-settimana W22              → piano settimana 22 (numero ISO)
```

## Skill innescata

`skills/process/strategia/week-fri/SKILL.md`

## Output

Email completo HTML + plain text in `/05_Calendario_editoriale/draft_piano_W[N]_[YYYY-MM-DD].md`, con preview in chat:

```
✅ Piano W22 (25-31 mag) generato.
File: draft_piano_W22_2026-05-25.md

Sintesi:
- 9 contenuti pianificati
- Pillar mix: 3 Famiglia · 2 Risparmio · 2 LegalTech · 2 Tutela
- Compliance: 7 🟢 · 2 🟡 (anonimizzazione case study) · 0 🔴
- Capitale CEO richiesto: 0h (silent approval window 48h aperta)
- Pronto per inviare via Friday Email? [SÌ/MODIFICA]
```

## Comportamento

- **Sempre 3 varianti per content critici** (Spiegato Facile · Badvisor · Caso Reale · Analisi)
- **Distribuzione bilanciata pillar** (no monocoltura su 1 pillar)
- **Rispetta calendar conflicts** (no overlap con eventi calendarizzati Google Calendar MCP)
- **Anti-fatigue cap**: max 1 post/giorno per canale, max 5 post/settimana per pillar
- **Spunti CEO**: pesca da `Spunti_CEO.md` prima di generare nuovi contenuti — gli spunti CEO hanno priorità

## Compliance

L'hook `pre-publish-compliance` NON scatta qui (è generazione draft, non publish). Però viene fatto un **pre-check soft** che colora ogni item 🟢🟡🔴 per anticipare problemi.

## Esempio reale

```
CEO: /piano-settimana

Output:
✅ Piano W21 (18-24 mag) generato.
File: draft_piano_W21_2026-05-18.md

#1 lun 18 mag 09:00 LinkedIn Daniele — Spiegato Facile — "Le 3 cose che TCM e LTC hanno in comune e nessuno te le dice"
#2 mar 19 mag 11:30 Instagram Reel — Caso Reale — "Maria, 62 anni" (anonimo)
#3 mer 20 mag 18:00 Blog THE ADVISOR — Analisi — "Long Term Care: il numero che cambia tutto"
... [9 totali]

Compliance: 7🟢 1🟡 1🔴
🔴 #7: claim "rendimento sicuro" su prodotto unit linked — bloccato, riformulare
🟡 #4: caso reale ma nome non anonimizzato

Vuoi che invii la Friday Email anticipata o aspetti ven 18:00? [INVIA/ATTENDI]
```

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
