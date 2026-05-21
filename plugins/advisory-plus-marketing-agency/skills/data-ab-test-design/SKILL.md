---
name: data-ab-test-design
description: Disegna esperimenti A/B statisticamente solidi per Advisory+ marketing. Copre: sample size calculation (formula classica con effect size + power + significance) Â· durata test (2-4 settimane tipico per social, 6-8 per email) Â· metrics architecture (primary + secondary + guardrail) Â· controlli operativi (no peeking, no early stop, segmentation, rollback plan). Use cases tipici: hook LinkedIn A vs B Â· subject line newsletter A vs B Â· voce editoriale A vs B su stesso pillar Â· thumbnail YouTube A vs B Â· CTA blog A vs B. Output Markdown con design plan + template tracking + criteri di chiusura. VINCOLO Brand Book v1.2 sez. 7: A/B test non possono usare claim ðŸ”´ vietati (rendimenti garantiti, comparazioni denigratorie, prezzi specifici).
---
# ðŸ§ª Skill data-ab-test-design â€” Design esperimenti A/B marketing Advisory+

> **Statistica solida. Compliance baseline. No claim ðŸ”´ nei test. Output: design plan + tracking template.**

---

## 1. Quando triggera

- Invocata dal MM quando vuole testare una variabile (hook, subject, voce, thumbnail, CTA, formato)
- Invocata da `advisory-plus:data-monthly-performance-report` come step F "Test da avviare"
- Invocata in fase di brief campagna per definire test da inserire nella pipeline (es. campaign-30-60-90)
- Invocata on-demand dal CEO se vuole "vedere se funziona meglio X o Y"
- Mai auto-trigger: brief MM obbligatorio (variabile da testare + ipotesi)

Tempo target di esecuzione: **15-30 minuti**.

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/data/[YYYY-MM-DD]_ab-test_[nome-test].md`:

```markdown
---
data: YYYY-MM-DD
nome_test: [es. "Subject line newsletter LTC - personale vs sistemico"]
canale: [LinkedIn pagina | LinkedIn personale | IG | FB | Newsletter | Blog | YouTube]
pillar: P[N]
variabile_testata: [es. "Tone of voice subject"]
ipotesi_h1: [versione A genera X% piÃ¹ [metrica primaria] di versione B perchÃ© [razionale]]
ipotesi_h0: [no differenza significativa]
data_start: YYYY-MM-DD
data_end_minima: YYYY-MM-DD
durata_minima: [N settimane]
sample_size_per_variante: N
metric_primaria: [es. "Open rate"]
metric_secondarie: [es. "CTR Â· click-to-open rate"]
metric_guardrail: [es. "Unsubscribe rate <0.3%"]
significance_level: 0.05
statistical_power: 0.80
effect_size_atteso: [es. "5pp di lift su open rate"]
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

## Sintesi (3-5 righe)

[Cosa testiamo + ipotesi + perchÃ© conta + criterio di chiusura]

## Versione A (controllo)

[Descrizione + esempio testuale completo]

## Versione B (variante)

[Descrizione + esempio testuale completo]

## Sample size & durata

- Formula: vedi sez. 3.1
- Sample size per variante: N
- Sample size totale: 2N
- Durata stimata: N settimane (dato il volume settimanale tipico del canale)
- Soglia minima per chiusura: sample size raggiunto + durata minima rispettata

## Metrics architecture

### Primary
- [Nome] â€” Definizione: [...] â€” Threshold significativitÃ : p<0.05 sul lift relativo

### Secondary (informative, no decisione)
- [Nome] â€” Definizione: [...]

### Guardrail (no peggioramento)
- [Nome] â€” Definizione: [...] â€” Threshold: [non oltre X% peggioramento]

## Setup operativo

### Randomization
[Come si assegnano gli utenti/contenuti a A vs B (es. split 50/50 random, alternato giorno, audience splitting Brevo)]

### Tracking
[Tool Â· UTM Â· evento conversion]

### Compliance check pre-launch
[Compliance Officer ha verificato: âœ… no claim ðŸ”´ Â· âœ… denominazione mandatarie Â· âœ… disclaimer Â· âœ… posizionamento nazionale]

## Controlli operativi (no peeking, no early stop)

- **NO peeking** prima di metÃ  sample size
- **NO early stop** anche se "sembra che A vinca" â€” termini il test secondo piano
- **Eccezione**: SOLO guardrail metric in zona rossa â†’ stop + analisi
- **Segmentation a posteriori**: sÃ¬ se sample size lo permette (per segmento target Brand Book v1.2 sez. 3)
- **Rollback plan**: se variante B perde â†’ torna a default A (stato pre-test) immediatamente

## Criteri di chiusura

1. âœ… Sample size raggiunto per entrambe le varianti
2. âœ… Durata minima rispettata
3. âœ… Guardrail metric NON in zona rossa
4. âœ… SignificativitÃ  statistica calcolata (z-test o chi-square a seconda della metrica)

## Decisione attesa

- **Se p<0.05 + lift >effect_size**: variante B vince â†’ adottata come nuovo default
- **Se p<0.05 + lift <effect_size**: variante B vince ma poco â†’ valuta costo-beneficio di adozione
- **Se pâ‰¥0.05**: no differenza significativa â†’ mantieni A (default)
- **Se guardrail rosso**: stop, analizza, eventualmente abort senza decisione

## Caveat

[Sample size piccolo? Power test sottile? Mid-campaign news che ha distorto? Annotare]
```

---

## 3. Statistica â€” formule operative

### 3.1 Sample size (per variante) â€” z-test proporzioni

Formula classica:
```
n = (z_Î±/2 + z_Î²)Â² Ã— [pâ‚(1-pâ‚) + pâ‚‚(1-pâ‚‚)] / (pâ‚ - pâ‚‚)Â²
```

Dove:
- z_Î±/2 = 1.96 (significance 0.05 two-tailed)
- z_Î² = 0.84 (power 0.80)
- pâ‚ = proporzione attesa controllo (baseline metric)
- pâ‚‚ = pâ‚ Ã— (1 + effect_size_relativo)

**Esempio pratico subject line newsletter:**
- Baseline open rate 25% â†’ pâ‚ = 0.25
- Effect size atteso lift +20% relativo â†’ pâ‚‚ = 0.30
- Sample size per variante: ~588 invii
- Sample size totale: ~1176 invii
- Se lista newsletter Ã¨ 1500: test fattibile in 1 invio
- Se lista Ã¨ 600: test richiede 2 invii (variante a settimane alternate)

### 3.2 Durata â€” basata su volume settimanale canale

| Canale | Volume settimanale tipico | Durata minima test |
|---|---|---|
| Newsletter | dipende da N iscritti Ã— frequenza | 1-3 invii o ~3 settimane |
| LinkedIn pagina | 2-3 post/sett | 4-6 settimane (sample size = impressions) |
| LinkedIn personale | 1 post/sett (Daniele) | 6-8 settimane |
| IG | 1-2 post/sett | 4-6 settimane |
| FB | 2 post/sett | 4-6 settimane |
| Blog | 1 articolo/sett | 6-8 settimane (lento per natura SEO) |
| YouTube | 1-2 video/mese | 8-12 settimane (volume basso fase calibrazione) |
| Thumbnail YouTube su singolo video | n/a, no A/B nativo YouTube basic | usare YouTube Studio Test Thumbnail (Premium) o split A/B su set di video |

### 3.3 Test statistico â€” quale usare

| Metrica | Test |
|---|---|
| Proporzione (open rate, CTR, conversion rate) | z-test proporzioni (o chi-square equivalente) |
| Media continua (dwell time, watch time, avg view duration) | t-test indipendente |
| Conteggi (numero commenti) | Poisson test o z-test approssimazione su volumi alti |

Il calcolo finale (p-value, lift relativo, intervallo di confidenza) viene fatto a fine test, non durante.

---

## 4. Use cases tipici per Advisory+

### 4.1 Subject line newsletter
- Variabile: tono subject (personale vs sistemico, domanda vs affermazione, curiositÃ  vs benefit)
- Primary: open rate
- Secondary: CTR
- Guardrail: unsub rate
- Durata: 1-3 invii

### 4.2 Hook LinkedIn (primo paragrafo post brand o Daniele)
- Variabile: tipo hook (provocatorio Â· domanda Â· numero Â· narrativo)
- Primary: engagement rate
- Secondary: dwell time, saves
- Guardrail: saldo polaritÃ  commenti
- Durata: 4-6 settimane

### 4.3 Voce editoriale A vs B su stesso pillar
- Variabile: Spiegato Facile vs Caso Reale su pillar 5 LTC, per esempio
- Primary: engagement rate
- Secondary: saves, CTR, dwell
- Guardrail: no spike unsub o sentiment negativo
- Durata: 6-8 settimane (piÃ¹ contenuti per variante)
- **Nota Brand Book**: tetto Badvisor 20% rispettato â€” Badvisor non si testa contro Spiegato Facile in modo che lo superi (gestire come variante esplorativa)

### 4.4 Thumbnail YouTube (post-lancio)
- Variabile: tipologia thumbnail (faccia visibile no/sÃ¬ avatar, testo grande/piccolo, colore brand vs accent)
- Primary: CTR
- Secondary: AVD
- Guardrail: dislike rate
- Tool: YouTube Studio Test Thumbnail (richiede YouTube Premium) o split a posteriori cambiando thumb su video stabile

### 4.5 CTA blog (in fondo articolo)
- Variabile: tipo CTA (newsletter signup Â· contatti Â· scarica guida)
- Primary: conversion rate sulla CTA
- Secondary: bounce post-CTA
- Durata: 6-8 settimane

---

## 5. Vincoli Brand Book v1.2 (Compliance check obbligatorio)

ðŸ”´ **Mai testare claim vietati**:
- Rendimenti garantiti su prodotti finanziario-assicurativi (es. "Garantisci 5% di rendimento" come variante)
- Comparazioni denigratorie con compagnie non mandatarie
- Prezzi specifici di prodotto senza contesto
- Testimonial reali senza consenso
- Dati inventati come hook

ðŸŸ¡ **Borderline che richiedono Compliance pre-launch**:
- Hook provocatorio Badvisor â†’ verifica regola "paradosso vs sistema, non vs lettore"
- A/B test su Tutela Legale â†’ verifica chiosa "consulenza individuale" per prodotti complessi (Reg. IVASS 40/2018 art. 56)
- A/B test pillar P9 D&O/RC professionale â†’ idem
- Subject line clickbait â†’ no "promesse" non sostanziate

âœ… **Sempre rispettati nelle varianti**:
- Disclaimer RUI nei canali che lo richiedono
- Denominazione mandatarie corretta
- Posizionamento nazionale (no Versilia/Apuana)
- AI disclosure se variante usa avatar HeyGen

---

## 6. Cosa NON fare mai

- âŒ **Early stop** anche se A "sembra vincere" (rischio falso positivo)
- âŒ **Peeking ripetuto** durante il test (gonfia Î± effettivo)
- âŒ **Modificare il test mid-flight** (cambiare variante B in corso = invalidazione)
- âŒ **Saltare guardrail** ("ma il primary va bene, ignoriamo unsub rate")
- âŒ **Test con sample size <30 per variante** â€” variance dominante, risultato non robusto
- âŒ **Test su claim ðŸ”´ vietati** (Brand Book v1.2 sez. 7)
- âŒ **Multi-armed bandit fai-da-te** senza framework statistico solido (lasciato a future iterazioni plugin v2.0)
- âŒ **Concludere "non ha funzionato"** senza analisi: power sottile? sample piccolo? confounding evento esterno?
- âŒ **Cherry-picking segment** post-hoc per "trovare un vincitore" (data dredging)

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di disegnare il test, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 5 strategia canali Â· sez. 7 Compliance â€” claim vietati)
2. `/01_Team/07_Data_Analyst.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (canali, frequenze, voci, claim ammessi/vietati)
4. KPI baseline corrente (`Output_approvati/data/data-kpi-channel-baseline.md`) per derivare baseline metric
5. Storico A/B test precedenti (per evitare riesumare test giÃ  conclusi)
6. Il brief operativo del MM (variabile + ipotesi)

---

## 8. Compliance hook (obbligatorio pre-launch)

Invoca SEMPRE `advisory-plus:compliance-gate-doppio` prima del go-live del test:
- Verifica claim entrambe varianti A e B
- Verifica disclaimer / denominazione mandatarie
- ðŸŸ¢ â†’ go Â· ðŸŸ¡ â†’ riformulazione Â· ðŸ”´ â†’ blocco

---

*SKILL v1.0 â€” advisory-plus:data-ab-test-design â€” Sessione 5 Plugin Build â€” 2026-05-20*

