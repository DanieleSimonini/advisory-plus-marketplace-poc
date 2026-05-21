---
name: data-attribution-model
description: Definisce e applica il modello di attribuzione cross-channel per Advisory+ (consulenza assicurativa high-consideration multi-touchpoint: blog â†’ newsletter â†’ LinkedIn â†’ call â†’ lead). Confronta 5 modelli (first-touch Â· last-touch Â· linear Â· time-decay Â· position-based U-shaped) e raccomanda il migliore per il nostro funnel. Mio suggerimento iniziale: time-decay con 30 gg di lookback. Output: documento modello attivato + razionale + esempi applicati su 3-5 conversion path reali (o simulati con caveat). Read-only sul dataset (no scrittura dati grezzi), solo logic + report. Trigger: setup iniziale plugin + revisione semestrale + on-demand quando emerge dubbio interpretativo nei monthly report.
---
# ðŸŽ¯ Skill data-attribution-model â€” Modello attribuzione cross-channel Advisory+

> **Funnel high-consideration multi-touchpoint. Raccomandazione default: time-decay 30gg lookback. Output: logic + razionale, no scrittura dati.**

---

## 1. Quando triggera

- **Setup iniziale plugin v1.1** (questa sessione): definisce modello attivo e logica di applicazione
- **Revisione semestrale** in chat 08 Performance & Analytics
- Invocata da `advisory-plus:data-monthly-performance-report` come reference per interpretare conversion path
- Invocata on-demand dal MM quando emerge dubbio interpretativo ("ma chi ha generato davvero questo lead?")
- Invocata da `advisory-plus:data-cohort-analysis` per fonti di acquisizione di una coorte
- Mai auto-trigger continuo: brief MM obbligatorio

Tempo target di esecuzione: **15-30 minuti** (piÃ¹ lungo in setup iniziale).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/data/[YYYY-MM-DD]_attribution-model_[versione].md`:

```markdown
---
data: YYYY-MM-DD
versione: vN
modello_attivo: time-decay
lookback_window: 30 giorni
fall_back_window: 7 giorni (per email/social organic flash)
caveat: [es. "Senza GA4 Data API wirato, attribuzione manuale o tramite Supermetrics MCP â€” Sessione 8"]
---

## Executive Summary (3-5 righe)

[Modello attivo + perchÃ© + come si applica in pratica + caveat]

## Confronto 5 modelli

| Modello | Logica | Vantaggi per Advisory+ | Svantaggi per Advisory+ | Quando usarlo |
|---|---|---|---|---|
| First-touch | 100% credito al primo touchpoint | Identifica top of funnel awareness | Ignora nurture lungo (blog, newsletter) | Brand awareness campaign |
| Last-touch | 100% credito all'ultimo touchpoint | Semplice, default GA | Sovrastima call-to-action finali, ignora nurture | Conversion ottimization tattica |
| Linear | Credito equo su tutti i touchpoint | Riconosce nurture | Diluisce touchpoint chiave | Funnel breve uniforme |
| Time-decay (RACCOMANDATO) | Credito decresce esponenzialmente all'indietro nel tempo, half-life tipica 7-14gg | Premia il finale ma riconosce il nurture, adatto a high-consideration | Sottostima awareness lontana | Funnel lungo (Advisory+) |
| Position-based (U-shaped 40/20/40) | 40% first + 40% last + 20% middle | Riconosce inizio E fine, comprime middle | Arbitrario sul middle | Funnel definito con awareness e closing chiari |

## Modello raccomandato per Advisory+: TIME-DECAY con 30gg lookback

### Razionale (5-7 righe)

Consulenza assicurativa Ã¨ high-consideration con funnel lungo (settimane/mesi). Touchpoint tipico:
1. Articolo blog (awareness Â· educazione)
2. Newsletter signup (lead capture)
3. 2-3 newsletter ricevute (nurture)
4. Post LinkedIn rivisto (top of mind)
5. Modulo contatti compilato (lead qualificato)
6. Call con consulente (conversione cliente)

Time-decay (half-life 7-14 giorni) premia touchpoint vicini alla conversione (call, contact form) MA mantiene credito a nurture recente (newsletter, LinkedIn) MA non azzera awareness primaria (blog letto 3 settimane prima). Fit migliore di first/last/linear/position-based per il nostro funnel.

Lookback window 30 giorni: la maggior parte dei lead convertiti ha touchpoint significativi negli ultimi 30gg. Touchpoint >30gg residuano come "soft brand presence" non quantificata.

### Esempi applicati (conversion path reali o simulati)

**Esempio 1 â€” Lead retail "famiglia giovane genitori"** (Pillar 4)
- Touchpoint #1 (giorno -28): Articolo blog "TCM giovani genitori cosa coprire" (organic search)
- Touchpoint #2 (giorno -25): Newsletter signup
- Touchpoint #3 (giorno -18): Newsletter #1 ricevuta + click
- Touchpoint #4 (giorno -12): Post LinkedIn Daniele rivisto + save
- Touchpoint #5 (giorno -5): Modulo contatti compilato
- Touchpoint #6 (giorno 0): Call â†’ lead qualificato

Attribuzione time-decay (half-life 10gg):
- TP6 (call): ~25%
- TP5 (form, -5gg): ~22%
- TP4 (LinkedIn, -12gg): ~17%
- TP3 (newsletter, -18gg): ~13%
- TP2 (signup, -25gg): ~10%
- TP1 (blog, -28gg): ~8%

Interpretazione: blog ha aperto, newsletter ha nutrito, LinkedIn ha tenuto top of mind, form/call ha chiuso. Nessun singolo canale "ha generato il lead", il merito Ã¨ distribuito.

**Esempio 2 â€” Lead B2B "PMI famigliare"** (Pillar 9)
[...]

**Esempio 3 â€” Lead specialty "yacht"** (Pillar 10)
[...]

## Caveat metodologico

- Senza GA4 Data API wirato direttamente, attribuzione cross-channel completa richiede Supermetrics MCP (Sessione 8 wiring) o calcolo manuale su export
- Touchpoint WhatsApp e telefono diretti non sono tracciati in GA4 â†’ integrazione manuale via CRM Brevo + report MM
- LinkedIn profili personali (Daniele) non danno tracking dettagliato â†’ contributo stimato qualitativamente
- Soglia minima per attribuzione robusta: â‰¥30 lead/mese. Sotto, attribuzione qualitativa
```

---

## 3. I 5 modelli â€” formule operative

### 3.1 First-touch
```
credito(touchpoint_i) = 100% se i == 1, altrimenti 0%
```
Semplice. Premia awareness puro. Ignora nurture.

### 3.2 Last-touch (default GA4 storico)
```
credito(touchpoint_i) = 100% se i == n (ultimo), altrimenti 0%
```
Semplice. Premia closer. Ignora awareness e nurture.

### 3.3 Linear
```
credito(touchpoint_i) = 1/n per ogni touchpoint
```
Equo. Diluisce. Va bene per funnel breve uniforme.

### 3.4 Time-decay (RACCOMANDATO)
```
credito(touchpoint_i) = 2^(-Î”t_i / halflife)
poi normalizzazione: credito(i) = credito(i) / Î£ credito(j)
```
Dove:
- Î”t_i = giorni tra touchpoint_i e conversione
- halflife = 7-14 giorni (raccomandato 10gg per Advisory+)

Premia touchpoint vicini, mantiene credito ai lontani in modo decrescente.

### 3.5 Position-based U-shaped (40/20/40)
```
credito(primo) = 40%
credito(ultimo) = 40%
credito(middle) = 20% distribuito linearmente
```
Compromesso first + last. Buono per funnel con awareness e closing chiari.

---

## 4. Applicazione pratica nel plugin v1.1

### 4.1 Fonti dati (quando MCP wirati Sessione 8)
- **GA4** (Google Analytics 4) â†’ touchpoint web (blog, sito)
- **Brevo API** â†’ email open/click events
- **LinkedIn Pages Analytics** â†’ impressions/clicks pagina aziendale (via Supermetrics)
- **Meta Insights** â†’ impressions/clicks IG+FB (via Supermetrics)
- **YouTube Analytics** â†’ views/clicks (via Supermetrics)
- **CRM Brevo** â†’ lead qualificati con timestamp
- **Form analytics sito** â†’ submission con UTM source

### 4.2 Calcolo (logic, non scrittura)
Dato un set di conversion event (lead qualificato), per ogni evento:
1. Identifica conversion timestamp
2. Recupera touchpoint dell'utente nei 30gg precedenti (lookback)
3. Calcola Î”t per ogni touchpoint
4. Applica formula time-decay con halflife=10gg
5. Normalizza i crediti a somma 1
6. Aggrega per canale â†’ distribuzione credito per canale

### 4.3 Output Monthly report
- % credito per canale (es. blog 22%, newsletter 18%, LinkedIn 25%, IG 8%, FB 5%, YouTube 4%, direct/other 18%)
- Top 3 canali per credito
- Trend rispetto mese precedente

---

## 5. Limiti del modello (caveat trasparenti)

### 5.1 Touchpoint non tracciati
- Conversazioni dirette su WhatsApp non tracciate in attribution se non ricondotte manualmente
- Telefonate dirette non tracciate
- Word-of-mouth offline (passaparola tra clienti)
- PubblicitÃ  out-of-home (se mai attivata) â€” di solito non tracciabile

### 5.2 Profili personali LinkedIn
LinkedIn API limitata su profili personali rispetto a pagine. Contributo Daniele/altri soci stimato qualitativamente, non con precisione.

### 5.3 Cross-device
Utente legge blog da mobile, riceve newsletter su desktop, compila form su tablet â†’ tracking cross-device GA4 limitato. Approssimazione inevitabile.

### 5.4 Soglia statistica
Sotto i 30 lead/mese, attribuzione % per canale Ã¨ instabile (variance alta). In fase calibrazione (mese 1-3) usare attribution come indicazione qualitativa, non quantitativa.

---

## 6. Cosa NON fare mai

- âŒ **Promettere precisione assoluta** dell'attribution â€” Ã¨ approssimazione, sempre
- âŒ **Confondere correlazione con causalitÃ ** â€” "il canale X ha generato 30% lead" â‰  "se eliminiamo X perdiamo 30% lead"
- âŒ **Usare last-touch come default** per Advisory+ â€” sovrastima conversione tattica, ignora nurture
- âŒ **Cambiare modello continuamente** â€” coerenza serve per trend. Revisione semestrale (sez. 5), non ogni mese
- âŒ **Affidare decisioni di budget grandi** su attribution sotto soglia statistica (<30 lead/mese)
- âŒ **Modificare dati grezzi** â€” la skill Ã¨ read-only, applica logic e produce report
- âŒ **Includere prezzi specifici** dei prodotti nei conversion path documentati (compliance)

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di applicare il modello, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 3 segmenti target Â· sez. 5 strategia voce per canale Â· sez. 13.5 Friday Email)
2. `/01_Team/07_Data_Analyst.md` + `/01_Team/08_CRM_Lead_Manager.md`
3. `config/brand.json` (canali attivi)
4. `Output_approvati/data/` baseline KPI + attribution precedenti
5. Il brief operativo del MM o skill chiamante

---

*SKILL v1.0 â€” advisory-plus:data-attribution-model â€” Sessione 5 Plugin Build â€” 2026-05-20*

