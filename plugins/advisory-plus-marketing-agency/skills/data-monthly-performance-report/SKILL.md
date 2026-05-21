---
name: data-monthly-performance-report
description: Compone il report mensile di performance marketing Advisory+ secondo template standard MM in 6 sezioni â€” A) Sintesi esecutiva 5 righe Â· B) Numeri chiave per canale (7 canali Â· KPI primari + variazione MoM) Â· C) Top 3 e Bottom 3 contenuti per performance Â· D) Pattern osservati (formato, orario, voce, pillar) Â· E) Raccomandazioni mese successivo (3 azioni concrete + perchÃ©) Â· F) Test da avviare (2-3 ipotesi). Orchestra: invoca data-kpi-channel-baseline (reference target) Â· data-attribution-model (mix canali) Â· data-cohort-analysis (sezione D pattern) Â· data-ab-test-design (sezione F). Trigger: ULTIMO VENERDÃŒ DEL MESE schedulato, alimenta il Friday Email di quel venerdÃ¬ (Brand Book v1.2 sez. 13.5). Input: dati Supermetrics MCP (Sessione 8) + Brevo stats + export LinkedIn/Meta/GA4. Output: file Markdown completo + sezione "Recap mese" pronta per Friday Email.
---
# ðŸ“ˆ Skill data-monthly-performance-report â€” Report mensile performance marketing

> **Schedulato ultimo venerdÃ¬ del mese. Alimenta Friday Email Brand Book v1.2 sez. 13.5. 6 sezioni standard. Orchestra 4 skill data via Task tool.**

---

## 1. Quando triggera

- **Schedulato ULTIMO VENERDÃŒ DEL MESE** (cron schedule via scheduled-tasks MCP, Sessione 8)
- Output alimenta automaticamente il Friday Email di quel venerdÃ¬ stesso (sezione "A. Recap settimana" estesa a "Recap settimana + Recap mese")
- Invocata on-demand dal MM/CEO per report ad-hoc (es. fine campagna, fine pillar-of-month)
- Mai auto-trigger continuo: schedulazione o brief MM obbligatori

Tempo target di esecuzione: **45-90 minuti** (orchestrazione di 4 skill data + composizione finale).

---

## 2. Output finale atteso

### A) File Markdown completo
In `Output_approvati/data/[YYYY-MM]_monthly-performance-report.md`:

```markdown
---
mese_riferimento: [YYYY-MM]
data_compilazione: YYYY-MM-DD (ultimo venerdÃ¬ del mese)
pillar_dominante_mese: P[N] [Nome]
specialty_attiva: [P10/P11/P12 o "nessuna"]
versione: vN
fonti_dati: [Supermetrics MCP Â· Brevo API Â· GA4 export Â· LinkedIn dashboard Â· YouTube Studio]
caveat: [se applicabili]
---

## A. Sintesi esecutiva (5 righe)

[Cosa Ã¨ successo Â· cosa ha funzionato Â· cosa no Â· take-away chiave Â· raccomandazione headline]

## B. Numeri chiave per canale (7 canali)

### LinkedIn Pagina Aziendale Advisory+
| KPI | Mese corrente | Mese precedente | Variazione % | Target mese | Status |
|---|---|---|---|---|---|
| Follower (count) | N | N | Â±X% | T | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Engagement Rate | X% | X% | Â±X pp | T | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| CTR su link | X% | X% | Â±X pp | T | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Reach mediano | N | N | Â±X% | T | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |

### LinkedIn Profili Personali (Daniele 80% + altri 20%)
[Idem tabella]

### Instagram (@advisoryplus_)
[Idem]

### Facebook
[Idem]

### Blog "THE ADVISOR"
[Idem]

### Newsletter (Brevo)
[Idem]

### YouTube
[Idem â€” solo da giugno 2026 in poi, prima "non ancora attivo"]

### Mix canali (da skill attribution-model)
[Distribuzione credito % per canale (time-decay 30gg) + trend MoM]

## C. Top 3 e Bottom 3 contenuti

### Top 3 contenuti per engagement
1. [Titolo] Â· [Canale] Â· [Pillar] Â· [Voce] Â· [Metrica chiave es. 8.5% ER Â· 1200 reach] Â· [Pubblicato il YYYY-MM-DD]
2. [...]
3. [...]

### Bottom 3 contenuti
1. [Titolo] Â· [Canale] Â· [Pillar] Â· [Voce] Â· [Metrica chiave] Â· [Pubblicato il YYYY-MM-DD]
2. [...]
3. [...]

### Best long-form del mese
- Articolo blog top per dwell-time + posizione media GSC
- Newsletter top per open rate

### Best video del mese (post-launch YouTube)
- Video top per AVD + iscritti acquisiti

## D. Pattern osservati

### D.1 Formato vincente
[Es. "Caroselli Spiegato Facile su IG sovraperformano post statici 1.8x" + dato]

### D.2 Orario ottimale
[Es. "LinkedIn pagina mar-mer 09:00 sovraperforma ven 14:00 di +35%"]

### D.3 Voce performante
[Es. "Voce Caso Reale sul Pillar 5 LTC = top engagement del mese"]

### D.4 Pillar in salute / in sofferenza
[Es. "Pillar 7 Tutela Legale ha generato 25% engagement totale brand, vs 12% mese precedente"]

### D.5 Coorti (handoff da cohort-analysis)
[Sintesi 2-3 righe dai principali pattern coorte]

### D.6 AI disclosure compliance (post-YouTube launch)
[Tasso 100% video AI con disclosure â†’ ðŸŸ¢]

## E. Raccomandazioni per il mese successivo (3 azioni concrete)

1. **[Azione 1]** â€” Razionale: [...] â€” Canale: [...] â€” Pillar: P[N] â€” Effort: [basso/medio/alto] â€” Stima impatto: [qualitativa]
2. **[Azione 2]** â€” [...]
3. **[Azione 3]** â€” [...]

## F. Test da avviare (2-3 ipotesi)

1. **Test 1 â€” [Variabile]** â€” Canale: [...] â€” Ipotesi: [...] â€” Sample size stimato: N â€” Durata: N sett. (handoff a `advisory-plus:data-ab-test-design` per design completo)
2. **Test 2 â€” [Variabile]** â€” [...]
3. **Test 3 â€” [Variabile]** (opzionale) â€” [...]

## G. Punti di esitazione MM (se Trust Calibration Window 30gg ancora aperta)

[Max 3 punti, formato:
- Punto: [...]
- Proposta MM: [...]
- Alternativa scartata e perchÃ©: [...]
Riconciliato in chiusura mese successivo se CEO ha vetato.]

## H. Caveat metodologici

[Eventuali limiti dati: pre-Supermetrics wiring, soglie statistiche, dati YouTube ancora bassi in fase calibrazione, ecc.]
```

### B) Sezione "Recap mese" per Friday Email
Estratto della sezione A (5 righe) + Top 3 contenuti + Top 3 raccomandazioni â†’ handoff a `advisory-plus:strategia-week-fri` che integra nella Friday Email di quel venerdÃ¬ stesso.

---

## 3. Le 6 sezioni â€” dettaglio operativo

### A. Sintesi esecutiva (5 righe)
- Cosa Ã¨ successo nel mese (1 riga)
- Cosa ha funzionato (1 riga)
- Cosa no (1 riga)
- Take-away chiave (1 riga)
- Raccomandazione headline (1 riga)

Tono: asciutto, fattuale, non promozionale.

### B. Numeri chiave per canale (7 canali)
Per ogni canale, tabella con: KPI primario Â· valore mese corrente Â· valore mese precedente Â· variazione % o pp Â· target Â· status ðŸŸ¢/ðŸŸ¡/ðŸ”´.

**Pre-Supermetrics MCP wiring (Sessione 8):** export manuale + MM compila tabella.
**Post-Supermetrics wiring:** pull automatico settimanale aggregato a fine mese.

### C. Top 3 e Bottom 3
- Top 3 = contenuti con engagement rate (o metrica primaria del canale) piÃ¹ alto
- Bottom 3 = contenuti con engagement rate piÃ¹ basso (no zero per outlier)
- Esplicitare canale + pillar + voce per ogni contenuto â†’ pattern emergono dalla composizione
- Aggiungere "best long-form" (1 blog post + 1 newsletter) e "best video" (post-YouTube launch)

### D. Pattern osservati
**Almeno 4 dimensioni:**
- Formato vincente (carosello vs post statico vs reel Â· long-form vs short-form)
- Orario ottimale (giorno settimana + ora)
- Voce performante (quale delle 4 voci editoriali ha generato piÃ¹ engagement)
- Pillar in salute / in sofferenza (allocazione attenzione vs ROI engagement)

**Sezione D.5 = handoff da cohort-analysis** (skill richiamata automaticamente).
**Sezione D.6 = compliance check AI disclosure** (post-YouTube launch).

### E. Raccomandazioni (3 azioni)
Ogni raccomandazione deve essere **azionabile** (non "fare meglio") con:
- Cosa fare (verbo + oggetto)
- Razionale (perchÃ©, in base ai pattern sezione D)
- Canale di applicazione
- Pillar di riferimento (1-12)
- Effort stimato
- Impatto qualitativo atteso

### F. Test da avviare (2-3)
Identificare ipotesi sperimentali emerse dai pattern. Per ogni test:
- Variabile da testare
- Canale
- Ipotesi (lift atteso + razionale)
- Sample size stimato
- Durata stimata
- Handoff a `advisory-plus:data-ab-test-design` per design completo nella settimana successiva

### G. Punti di esitazione MM (Trust Calibration Window)
Solo nei primi 30 giorni post-go-live plugin (16 mag â†’ 16 giu 2026 e iterazioni). Max 3 punti di MM Decision Authority dove ha esitato + proposta + alternativa scartata.
Dopo 16 giu 2026: sezione opzionale, solo se MM dichiara esitazione.

### H. Caveat metodologici
Trasparenza su limiti dati: tool non ancora wirati, soglie statistiche, etc.

---

## 4. Orchestrazione skill (Task tool)

La skill invoca in sequenza:

```
Step 1: Task(subagent_type: "advisory-plus:data-kpi-channel-baseline",
             prompt: "Recupera baseline KPI corrente per 7 canali Â· scope: mese [YYYY-MM]")
        â†’ riceve tabella KPI baseline + target

Step 2: Pull dati mese corrente:
        - Brevo API â†’ newsletter stats
        - Export GA4 / GSC â†’ blog stats
        - LinkedIn dashboard / Supermetrics â†’ social stats
        - YouTube Studio Analytics â†’ video stats (post-launch)
        - CRM Brevo â†’ lead stats

Step 3: Calcola variazione MoM per ogni KPI + status ðŸŸ¢/ðŸŸ¡/ðŸ”´ vs target

Step 4: Task(subagent_type: "advisory-plus:data-attribution-model",
             prompt: "Calcola mix canali con time-decay 30gg per il mese [YYYY-MM]")
        â†’ riceve distribuzione credito %

Step 5: Identifica Top 3 + Bottom 3 contenuti per canale (engagement rate)

Step 6: Task(subagent_type: "advisory-plus:data-cohort-analysis",
             prompt: "Sezione D5 - pattern coorti del mese [YYYY-MM] in formato 2-3 righe")
        â†’ riceve sintesi pattern

Step 7: Identifica pattern formato/orario/voce/pillar dalla matrice contenuti

Step 8: Genera 3 raccomandazioni azionabili + 2-3 test ipotetici

Step 9: Task(subagent_type: "advisory-plus:data-ab-test-design",
             prompt: "Pre-design per 2-3 test: [variabile1, variabile2, variabile3]")
        â†’ riceve sample size + durata stimate per ogni test

Step 10: Compila il report Markdown completo (sezioni A-H)

Step 11: Genera estratto "Recap mese" per Friday Email

Step 12: Handoff a Marketing Manager per integrazione Friday Email
```

---

## 5. Casi particolari

### Mese 1 post-launch plugin (giugno 2026)
- Dati ancora sotto soglia statistica per molti KPI
- Sezione H caveat esteso
- Raccomandazioni piÃ¹ cautelative
- Sezione G punti esitazione attivata (Trust Calibration Window)

### Mese 1 post-launch YouTube (giugno 2026)
- Solo 1-2 video pubblicati â†’ KPI YouTube preliminari
- Caveat su volume basso
- Pattern emergenti = ipotesi, non conclusioni

### Mese specialty attiva (P10/P11/P12)
- Sezione D dedica spazio a performance specialty
- Confronto con altri mesi specialty (se esistono)

### Crisis mode mese
- Report condensato (sezioni A + B + critico H)
- Pattern e raccomandazioni rinviati a mese successivo

### Vacation mode mese
- Report parziale (settimane attive)
- Caveat esplicito su rappresentativitÃ  dati

---

## 6. Compliance & Brand baseline

Ogni report passa:
- âœ… Compliance check finale (`advisory-plus:compliance-gate-doppio`) â€” verifica no claim ðŸ”´ nelle raccomandazioni e test ipotetici
- âœ… Brand Strategist check coerenza con Brand Book v1.2 (pillar attivi, voci, posizionamento nazionale)
- âœ… Privacy GDPR: nessun dato personale di utenti nel report (anonimizzato per default)
- âœ… Denominazione mandatarie corretta (se citate)

---

## 7. Cosa NON fare mai

- âŒ **Inventare numeri** se i dati non sono disponibili (Brand Book v1.2 sez. 7)
- âŒ **Cherry-pick metriche** che fanno bella figura ignorando sotto-target
- âŒ **Bottom 3 con outlier estremi** (es. post pubblicato 2 giorni prima fine mese con zero impressions per tempistica, non per qualitÃ )
- âŒ **Raccomandazioni vaghe** ("fare meglio", "spingere su LinkedIn") â€” sempre azionabili
- âŒ **Test ipotetici senza ipotesi misurabile** â€” sempre lift atteso + criterio chiusura
- âŒ **Confronti denigratori** con competitor nel report
- âŒ **Sentiment analysis automatica** senza review umano (rischio errore semantico italiano)
- âŒ **Dati personali utenti** nel report (GDPR)
- âŒ **Bypass del Trust Calibration Window** nei primi 30gg (sezione G obbligatoria)
- âŒ **Pubblicare il report senza approvazione MM/CEO** se contiene proposte di budget o decisioni strategiche

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di compilare il report, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia canali Â· sez. 6 Pillar Map Â· sez. 13.5 Friday Email Â· sez. 14 YouTube)
2. `/01_Team/00_Marketing_Manager.md` + `/01_Team/07_Data_Analyst.md`
3. `config/brand.json` (canali, pillar, voci, target dichiarati)
4. `Output_approvati/data/` baseline KPI + report mensili precedenti (per trend)
5. `Output_approvati/` di tutte le chat operative del mese (per identificazione contenuti pubblicati e Top/Bottom)
6. Dati grezzi disponibili (export Brevo, GA4, LinkedIn, Meta, YouTube Studio)
7. Il brief operativo del MM (se on-demand) o schedulazione

---

*SKILL v1.0 â€” advisory-plus:data-monthly-performance-report â€” Sessione 5 Plugin Build â€” 2026-05-20*

