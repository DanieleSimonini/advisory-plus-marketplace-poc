---
name: data-kpi-channel-baseline
description: Definisce e mantiene la baseline KPI per i 7 canali Advisory+ (LinkedIn pagina + profili personali Â· Instagram Â· Facebook Â· Blog THE ADVISOR Â· Newsletter Â· WhatsApp utility Â· YouTube nuovo canale Brand Book v1.2 sez. 14). Per ogni canale: KPI primari + secondari + guardrail Â· benchmark settore B2B/finanziario IT con fonti+anno Â· target prudente mese 1 lancio Â· target a regime 6 mesi. Output: tabella KPI consolidata + nota su come misurare ogni metrica + caveat fonti. Aggiornabile via Supermetrics MCP quando wirato (Sessione 8 MCP wiring). Trigger: una tantum a setup plugin + refresh trimestrale + post-launch nuovo canale (es. YouTube giugno 2026).
---
# ðŸ“Š Skill data-kpi-channel-baseline â€” Baseline KPI 7 canali Advisory+

> **Una tantum a setup + refresh trimestrale + post-launch nuovi canali. Alimenta Friday Email recap + Monthly report.**

---

## 1. Quando triggera

- **Setup iniziale plugin v1.1** (questa sessione): definisce baseline KPI per tutti i 7 canali
- **Refresh trimestrale** in chat 08 Performance & Analytics (riallineamento target dopo 3 mesi di dati)
- **Post-launch nuovo canale** (es. YouTube go-live giugno 2026 â†’ primo benchmark fase calibrazione + target a regime)
- Invocata da `advisory-plus:data-monthly-performance-report` come reference per calcolo delta target
- Invocata da `advisory-plus:data-ab-test-design` per definire effect size atteso e guardrail metrics
- Mai auto-trigger continuo: brief MM o scheduled task obbligatorio

Tempo target di esecuzione: **20-40 minuti** (piÃ¹ lungo in setup iniziale).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/data/[YYYY-MM-DD]_kpi-baseline_[scope].md`:

```markdown
---
data: YYYY-MM-DD
versione: vN
scope: [setup_iniziale | refresh_trimestrale | post_launch_canale]
fonte_benchmark: [es. "Statista Insurance Marketing IT 2025 Â· LinkedIn B2B Benchmark Report 2024 Â· Mailchimp Benchmarks Industry Finance/Insurance 2024"]
caveat: [es. "Benchmark settore B2B/finanziario IT, validare con dati storici nostri dopo 3 mesi"]
---

## Executive Summary (5 righe)

[Stato baseline + canali con target piÃ¹ sfidanti + canale di apertura YouTube e relative cautele]

## Tabella KPI consolidata per canale

[Vedi sezione 3 sotto]

## Note metodologiche per canale

[Per ogni canale: come si misura ogni KPI Â· quale tool Â· frequenza misurazione]

## Aggiornamento Supermetrics MCP

[Quando MCP wirato (Sessione 8): pull automatico dei KPI dai data source nativi. Frequenza pull: settimanale per Friday Email Â· mensile per Monthly report]

## Caveat fonti benchmark

[Tutte le fonti benchmark esterne hanno anno di riferimento. Settore "B2B Finance/Insurance Italy" non sempre ha dati granulari pubblici. Quando benchmark assente: target prudente basato su esperienza generale + revisione a 3 mesi su dati nostri.]
```

---

## 3. KPI per canale

### 3.1 LinkedIn Pagina Aziendale Advisory+

| KPI | Primario/Secondario/Guardrail | Benchmark settore (fonte+anno) | Target mese 1 | Target a regime (6 mesi) |
|---|---|---|---|---|
| Follower (count) | Primario | 100-500 follower-month per pagine B2B medio-piccole | +30-50/mese | +80-120/mese |
| Engagement Rate (likes+comm+share / impressions) | Primario | 2-4% B2B finance medio (LinkedIn B2B Benchmark) | 2-3% | 4-5% |
| CTR su link (clicks / impressions) | Secondario | 0.4-1.2% B2B | 0.5% | 1.0% |
| Reach mediano per post | Secondario | varia per audience size | 500-1500 imp | 2000-5000 imp |
| Saldo polaritÃ  sentiment commenti | Guardrail | >0 = positivo | >0 | >0 |

### 3.2 LinkedIn Profili Personali (Daniele 80% + altri soci 20%)

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Engagement rate post Daniele | Primario | 5-10% profili personali esperti | 4-6% | 7-10% |
| Saving rate (save / impressions) | Secondario | 0.5-2% per contenuti educativi | 0.5% | 1.5% |
| Dwell time (qualitativo via dwell sui Long-form Article) | Secondario | n/d puntuale | â€” | â€” |
| Tasso commenti significativi (>10 parole / commenti tot) | Guardrail | >40% | >30% | >50% |
| Coerenza voce 80/20 firma | Guardrail | 80/20 Â±5% | rispettato | rispettato |

### 3.3 Instagram (@advisoryplus_)

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Follower count | Primario | crescita 1-3%/mese B2B medio | +30-60/mese | +80-150/mese |
| Engagement Rate (likes+comm+saves+shares / reach) | Primario | 1-3% finance Italy 2024 | 2% | 3.5% |
| Reach mediano post | Secondario | 30-70% follower-base | 30% | 50% |
| Saves rate (saves / reach) | Secondario | 0.5-2% educational content | 0.5% | 1.5% |
| Stories completion rate | Secondario | 60-80% per set ben fatto | 60% | 75% |
| Reel reach mediano | Secondario | 2-5x reach post statico | 2x post | 4x post |

### 3.4 Facebook

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Engagement Rate (interazioni / reach) | Primario | 1-2% finance Italy | 1% | 2% |
| Reach organico mediano | Primario | 5-15% follower-base (FB organico molto compresso) | 5% | 10% |
| CTR link | Secondario | 0.3-0.8% | 0.4% | 0.7% |
| Saldo polaritÃ  sentiment | Guardrail | >0 | >0 | >0 |

### 3.5 Blog "THE ADVISOR" (advisoryplus.it/the-advisor)

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Visite mensili (GA4 sessions) | Primario | 200-1000 per blog corporate giovane | 300-500 | 2000-5000 |
| Sessioni organiche (GA4 traffic-source organic) | Primario | 40-60% del traffico totale blog maturo | 30% del tot | 60% del tot |
| Bounce rate articolo singolo | Secondario | 50-70% blog informativo Ã¨ normale | 70% | 55% |
| Dwell time medio (engaged sessions GA4) | Primario | 2-4 min per articoli 1000-2000p | 1.5min | 3min |
| Posizione media keyword (GSC) | Secondario | 20-40 al lancio, sotto 10 a regime per long-tail | 30-50 | 10-20 |
| CTR organico medio (GSC) | Secondario | 2-5% medio | 2% | 4% |
| Email signup da blog | Secondario | 0.5-2% conversion blogâ†’newsletter | 0.5% | 1.5% |

### 3.6 Newsletter (Brevo)

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Open rate | Primario | 20-25% finance/insurance IT (Mailchimp Benchmarks 2024 industry "Insurance") | 25% (audience opt-in fresca) | 30% |
| CTR (click / send) | Primario | 2-3% finance/insurance IT | 2% | 3.5% |
| CTOR (click / open) | Secondario | 8-15% | 10% | 14% |
| Unsubscribe rate | Guardrail | <0.5% sano | <0.3% | <0.3% |
| Spam complaint rate | Guardrail | <0.1% sano | <0.05% | <0.05% |
| Lista crescita netta | Secondario | +2-5%/mese sano | +5%/mese (lancio) | +3%/mese stabile |

### 3.7 YouTube (canale NUOVO Brand Book v1.2 sez. 14, go-live giugno 2026)

| KPI | Tipo | Benchmark | Mese 1-2 (calibrazione) | Mese 6+ (a regime) |
|---|---|---|---|---|
| Iscritti (count) | Primario | n/d settore IT specifico | 30-100 | 500-1500 |
| Visualizzazioni mediane per video | Primario | 50-200 canali giovani B2B | 50-150 | 500-2000 |
| Watch time mediano (Avg View Duration) | Primario | 40-50% video durata 5-10 min | 35% | 50% |
| CTR thumbnail (impressions â†’ clicks) | Secondario | 3-6% sano YouTube | 3% | 5-7% |
| Like/View ratio | Secondario | 2-5% | 2% | 4% |
| Iscritti per video | Secondario | 0.5-2 nuovi iscritti per video B2B | 0.5/video | 3-5/video |
| AI disclosure compliance | Guardrail | 100% video AI con disclosure | 100% | 100% |

### 3.8 WhatsApp Business (canale utility, no editoriale)

| KPI | Tipo | Benchmark | Mese 1 | A regime |
|---|---|---|---|---|
| Tasso di risposta in 24h (cliente â†’ noi) | Primario | n/d standard, target servizio | 95% | 98% |
| Numero messaggi proattivi/mese (scadenze polizze, auguri) | Operativo | dipende dal CRM trigger | misurato | misurato |
| Lamentele / reclami via WA | Guardrail | bassissimo | <1% messaggi | <1% messaggi |
| Opt-out rate | Guardrail | <0.5% | <0.3% | <0.3% |

---

## 4. Note metodologiche

### Come si misura ogni KPI (tool-by-tool)

| Canale | Tool nativo | Tool via Supermetrics MCP (Sessione 8) | Frequenza pull |
|---|---|---|---|
| LinkedIn Pagina | LinkedIn Analytics nativo | Supermetrics â†’ LinkedIn Pages | Settimanale |
| LinkedIn Profili | LinkedIn dashboard creator (Daniele) | Manuale (no Supermetrics su profili personali) | Settimanale |
| Instagram | Insights Meta Business Suite | Supermetrics â†’ Meta Insights | Settimanale |
| Facebook | Insights Meta Business Suite | Supermetrics â†’ Meta Insights | Settimanale |
| Blog | GA4 + Google Search Console | Supermetrics â†’ GA4 + GSC | Settimanale |
| Newsletter | Brevo dashboard nativo | Brevo API REST via shell library (Sessione 6) | Per ogni invio |
| YouTube | YouTube Studio Analytics | Supermetrics â†’ YouTube Channel | Mensile (volumi bassi mese 1-2) |
| WhatsApp | Twilio Console o WA Business app | n/d in v1.1 (fase 2) | Manuale |

### Caveat fonti benchmark

- **LinkedIn B2B Benchmark Report 2024**: dato aggregato globale, settore "Financial Services". Mercato Italy puÃ² deviare Â±20-30%.
- **Mailchimp Email Benchmarks Industry "Insurance" 2024**: aggiornati annualmente, dato globale aggregato.
- **YouTube**: NO benchmark settore "broker assicurativo IT" disponibile pubblicamente. Target su esperienza generale canali B2B finanziari italiani giovani. Revisione obbligatoria a mese 3.
- **Tutti i benchmark hanno anno+fonte esplicito** (Brand Book v1.2 sez. 7 voce Analisi richiede fonte+anno per ogni dato).

---

## 5. Trust calibration window (post-go-live plugin)

Primi 30 giorni dopo go-live plugin v1.1 (31 mag â†’ 30 giu 2026):
- Misurazione settimanale di tutti i KPI primari
- Confronto vs target mese 1
- Se gap >30% sul target mese 1: ricalibrazione target (non panic mode) + sezione "Esitazione MM" in Friday Email (Brand Book v1.2 sez. 13.5)
- Refresh formale a fine giugno + fine settembre (refresh trimestrale)

---

## 6. Cosa NON fare mai

- âŒ **Promettere target garantiti** ("a 6 mesi avremo 5000 follower IG") â€” i target sono guida, non garanzia
- âŒ **Inventare benchmark** senza fonte+anno (Brand Book v1.2 sez. 7)
- âŒ **Confronti denigratori** con competitor su KPI ("noi siamo meglio di X")
- âŒ **Ignorare i guardrail** (es. unsub rate >0.5% segnala problema lista, non KPI laterale)
- âŒ **Confondere reach e impressions** o engagement rate calcolato male (sempre esplicitare formula)
- âŒ **Bypassare il vincolo posizionamento nazionale**: KPI non differenziano per regione (Brand Book v1.2 sez. 2)
- âŒ **Pull dati senza consenso esplicito CEO** sui profili personali soci (privacy)

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di definire/aggiornare baseline, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia voce per canale Â· sez. 13.5 Friday Email Â· sez. 14 YouTube)
2. `/01_Team/07_Data_Analyst.md`
3. `config/brand.json` (canali attivi, frequenze, target)
4. `Output_approvati/data/` baseline precedenti (per evoluzione storica)
5. Dati storici a disposizione (esportazioni LinkedIn/Meta/GA4/GSC/Brevo se giÃ  esistenti)
6. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:data-kpi-channel-baseline â€” Sessione 5 Plugin Build â€” 2026-05-20*

