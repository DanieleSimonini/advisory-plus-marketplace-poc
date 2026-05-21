---
name: stato
description: Stampa lo stato sintetico del sistema marketing Advisory+ negli ultimi 7 giorni — pubblicato, skippato, pending CEO, alert, scadenze token, KPI essenziali. Usalo ogni volta che vuoi un colpo d'occhio senza scrollare verbali.
argument-hint: [opzionale: numero giorni — default 7 | "mese" per ultimi 30gg]
---

# /stato — Dashboard sintetica sistema marketing

## Cosa fa

Esegue la skill `process/monitoring/stato` che aggrega dati da:

- Verbali di tutte le chat `/03_Aree_di_lavoro/*`
- Log di publish (Meta · LinkedIn · WordPress · YouTube)
- Analytics MCP (Supermetrics) — engagement, reach, click
- Scadenze token (Meta · Gemini · HeyGen · Brevo)
- Spunti_CEO.md (quanti nuovi · quanti già consumati)
- Compliance log (quanti 🟢🟡🔴 negli ultimi 7gg)

## Sintassi

```
/stato                  → ultimi 7 giorni (default)
/stato 14               → ultimi 14 giorni
/stato mese             → ultimi 30 giorni
/stato W21              → settimana 21
```

## Skill innescata

`skills/process/monitoring/stato/SKILL.md`

## Output formato fisso (mobile-friendly)

```
📊 ADVISORY+ STATO 7gg (11-18 mag 2026)
─────────────────────────────────────

📤 PUBBLICATO
- 5 LinkedIn (3 Daniele · 2 brand)
- 4 Instagram (3 post · 1 reel)
- 3 Facebook
- 1 Blog THE ADVISOR
Totale: 13 contenuti — target W21 era 9 ✅ +4 ahead

⏸️ SKIPPATO (CEO)
- 1 LinkedIn (STOP #4 ricevuto mar)

⏳ PENDING APPROVAZIONE CEO
- 0 (silent approval window 48h fluida)

🚨 ALERT
- Nessuno

🔑 SCADENZE TOKEN
- Meta: 60gg (17 lug)
- Gemini: stabile
- HeyGen: piano OK 13gg/15min

💡 SPUNTI CEO
- Nuovi non ancora consumati: 3
- Consumati settimana: 2

⚖️ COMPLIANCE
- 13 🟢 · 2 🟡 (anonimizzazioni applicate) · 0 🔴

📈 ENGAGEMENT TOP 3
1. LinkedIn Daniele "TCM e mutuo" — 47 reactions
2. IG Reel "Maria 62 anni" — 1240 views
3. Blog "LTC numero che cambia" — 380 reads · 4'12" avg

Ultimo aggiornamento: 18 mag 2026 18:00
```

## Comportamento

- **Sempre stesso formato** (CEO lo legge in 20 secondi)
- **Niente blabla introduttivo** — solo dati
- **Soglie alert configurate in `config/brand.json`**: drop engagement >40% vs avg → 🚨; token <7gg → 🚨; pending CEO >2 → 🚨
- **Mobile-first**: max 80 char per riga (legge sullo smartphone)

## Compliance

N/A — è solo report, no publish.

## Variante "scadenza"

```
/stato scadenze         → solo blocco token + reminder operativi
```

Output ultra-compatto:
```
🔑 TOKEN
Meta:     17 lug 2026 (60gg) ✅
Gemini:   stabile (rotazione 90gg)
HeyGen:   piano 13gg/15min
Brevo:    no exp
LinkedIn: pending MDP application
```

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
