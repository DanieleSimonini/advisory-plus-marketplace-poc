---
name: data-cohort-analysis
description: Segmenta utenti/follower/lead in coorti per analisi retention ed engagement nel tempo. Tre tipologie di coorte coperte: (a) ACQUISIZIONE per mese di iscrizione (newsletter signup, follower social, lead CRM Brevo); (b) COMPORTAMENTALI (lettori blog regolari vs occasionali, open-rate newsletter, engagement social click-vs-save-vs-comment); (c) DEMOGRAFICHE (8 segmenti target Brand Book v1.2 sez. 3 in 4 cluster â€” Privati & Famiglie, Patrimonio, Lavoro & Impresa, Terzo Settore & Specialty). Output insight retention + raccomandazioni iterazione. Richiamata mensilmente da data-monthly-performance-report come sezione D "Pattern osservati". Aggrega dati Brevo + Supermetrics (Sessione 8) + export GA4.
---
# ðŸ“Š Skill data-cohort-analysis â€” Segmentazione coorti retention/engagement

> **Tre tipologie coorte: acquisizione Â· comportamentali Â· demografiche. Output: insight + iterazione. Richiamata da monthly report.**

---

## 1. Quando triggera

- **Mensile** da `advisory-plus:data-monthly-performance-report` come sezione D
- **Trimestrale** standalone in chat 08 Performance & Analytics per deep-dive
- Invocata on-demand dal MM quando emerge dubbio su retention ("perchÃ© stiamo perdendo follower IG?" "perchÃ© open-rate newsletter scende?")
- Invocata da `advisory-plus:data-ab-test-design` per identificare la coorte target di un test
- Mai auto-trigger continuo: brief MM o monthly report schedulato

Tempo target di esecuzione: **20-45 minuti** (dipende da volume dati e tipologie coorti richieste).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/data/[YYYY-MM-DD]_cohort-analysis_[scope].md`:

```markdown
---
data: YYYY-MM-DD
scope: [mensile | trimestrale | deep-dive_canale | demografico]
periodo_analizzato: [es. Gen-Mar 2026]
coorti_analizzate: [acquisizione | comportamentali | demografiche]
caveat: [es. "Pre-Supermetrics wiring: alcune coorti su dati Brevo + manual export GA4. Demografiche basate su mapping segmenti dichiarati"]
---

## Executive Summary (5 righe)

[Cosa emerge Â· top 3 insight retention/engagement Â· 2 raccomandazioni per iterazione]

## A. Coorti di acquisizione (mese di iscrizione)

### Newsletter Brevo
| Coorte (mese signup) | Iscritti iniziali | Open Rate M+1 | Open Rate M+3 | Open Rate M+6 | Unsub M+6 |
|---|---|---|---|---|---|
| Gen 2026 | N | X% | Y% | Z% | W% |
| Feb 2026 | N | X% | Y% | â€” | W% |
| Mar 2026 | N | X% | â€” | â€” | â€” |

**Insight:** [es. "Coorti piÃ¹ giovani hanno open-rate iniziale migliore (welcome flow funziona). Decadimento ~5pp dopo 3 mesi Ã¨ fisiologico, sotto i 10pp Ã¨ sano."]

### Follower social (proxy: nuovi follower per mese)
| Canale | Coorte (mese) | Follower aggiunti | Stima retention M+3 |
|---|---|---|---|
| LinkedIn pagina | Gen 2026 | +N | n/d puntuale (Pagina LinkedIn non distingue, proxy via engagement coorte) |
| IG | Gen 2026 | +N | n/d puntuale |
| YouTube | Giu 2026 (lancio) | +N | calcolare a M+3 |

### Lead CRM Brevo
| Coorte (mese lead) | Lead acquisiti | Lead in nurture M+3 | Lead convertiti cliente M+6 |
|---|---|---|---|
| Gen 2026 | N | X% | Y% |
| ... | ... | ... | ... |

## B. Coorti comportamentali

### B.1 Lettori blog (GA4)
| Segmento | Definizione | Volume | Retention M+1 | Conversione newsletter |
|---|---|---|---|---|
| Lettore regolare | â‰¥3 sessioni/mese su blog | N | X% | Y% |
| Lettore occasionale | 1-2 sessioni/mese | N | X% | Y% |
| One-time | 1 sessione singola | N | X% (basso) | Y% |

### B.2 Newsletter
| Segmento | Definizione | Volume | CTR |
|---|---|---|---|
| Power reader | Apre â‰¥80% delle newsletter | N | X% |
| Casual | Apre 30-80% | N | X% |
| Dormant | Apre <30% (ultimi 3 mesi) | N | basso |
| Inactive | Non apre da 90gg | N | 0% |

**Azione raccomandata:** dormant + inactive â†’ re-engagement campaign mese successivo (handoff a skill CRM Brevo Sessione 6 + email-sequence-* da plugin).

### B.3 Engagement LinkedIn pagina
| Segmento | Definizione | Volume |
|---|---|---|
| Engager attivo | Like+commento+share â‰¥1 ogni 2 settimane | N |
| Reactor | Solo like sporadico | N |
| Lurker | Visualizza ma non interagisce | N (stimato via reach) |

## C. Coorti demografiche (8 segmenti target Brand Book v1.2 sez. 3)

### Cluster A â€” Privati & Famiglie
| Segmento | Match attivo nei dati? | Volume stimato | Engagement medio |
|---|---|---|---|
| 1. Famiglie giovani genitori (30-45) | sÃ¬/no/parziale | N | X |
| 2. Adulti 45-60 con genitori anziani | sÃ¬/no/parziale | N | X |
| 3. Pre-pensionati 55-65 | sÃ¬/no/parziale | N | X |

### Cluster B â€” Patrimonio
| 4. Patrimonializzati | parziale (audience nascosta) | n/d | n/d |

### Cluster C â€” Lavoro & Impresa
| 5. Professionisti & P.IVA | sÃ¬ | N | X |
| 6. PMI famigliari | sÃ¬ | N | X |
| 7. Imprese strutturate | parziale | N | X |

### Cluster D â€” Terzo Settore & Specialty
| 8. Enti del Terzo Settore | da costruire (lancio luglio 2026) | n/d | n/d |
| 9. Specialty yacht/arte/religiosi | sotto-coperto | N | X |

**Caveat demografico:** segmentazione perfetta richiederebbe dati clienti CRM cross-referenziati con audience digitale. In assenza, mapping Ã¨ euristico (analisi commenti, profili LinkedIn engager, contenuti su cui rispondono).

## D. Insight chiave (3-5)

1. [Insight retention] â€” [implicazione]
2. [Insight engagement] â€” [implicazione]
3. [Insight demografico] â€” [implicazione]
4. [...]
5. [...]

## E. Raccomandazioni per iterazione (2-4)

1. **[Azione]** â€” Razionale: [...] â€” Canale: [...] â€” Effort: [basso/medio/alto] â€” Stima impatto: [qualitativa]
2. [...]

## F. Caveat metodologico

[Pre-Supermetrics MCP wiring (Sessione 8): coorti su Brevo + manual export GA4. Volume sotto soglia statistica per alcuni segmenti specialty. Demografiche euristiche. Revisione metodologica trimestrale.]
```

---

## 3. Le 3 tipologie di coorte â€” definizioni operative

### 3.1 Acquisizione (cohort by signup month)
Raggruppare utenti per **mese di prima azione tracciabile**:
- Newsletter: mese signup Brevo (campo `created_at`)
- Lead: mese creazione record CRM
- Follower: proxy "follower aggiunti per mese" (no precisione per-user su pagine, stima)

Misurare retention (es. open rate newsletter) a M+1, M+3, M+6 dalla coorte.

Pattern atteso: decadimento naturale ~5-10pp dopo 3 mesi Ã¨ fisiologico. Decadimento >15pp = segnale onboarding/nurture rotto.

### 3.2 Comportamentali (behavior-based)
Raggruppare utenti per **pattern di interazione**:
- Lettore regolare vs occasionale vs one-time (blog GA4)
- Power reader vs casual vs dormant vs inactive (newsletter)
- Engager attivo vs reactor vs lurker (social)
- Lead nurture engaged vs cold (CRM Brevo)

Misurare conversion rate (es. % lettore regolare che si iscrive newsletter; % power reader che diventa lead).

### 3.3 Demografiche (8 segmenti target Brand Book v1.2 sez. 3)
Mappare audience digitale sui 8 segmenti target dichiarati:
- 1. Famiglie giovani genitori 30-45
- 2. Adulti 45-60 con genitori anziani
- 3. Pre-pensionati 55-65
- 4. Patrimonializzati
- 5. Professionisti & P.IVA
- 6. PMI famigliari
- 7. Imprese strutturate
- 8. Enti del Terzo Settore
- 9. Specialty (yacht/arte/religiosi)

Misurare: a quali segmenti stiamo arrivando? quali sono sotto-rappresentati? quali pillar generano engagement nei diversi segmenti?

âš ï¸ Caveat: segmentazione demografica precisa richiederebbe cross-referencing dati clienti reali con audience digitale. Senza, mapping Ã¨ euristico (analisi profili LinkedIn engager, contenuti su cui rispondono, segnali contestuali commenti).

---

## 4. Logica di esecuzione â€” 5 fasi

### Fase 1 â€” Brief + scope
- Scope (mensile Â· trimestrale Â· deep-dive canale Â· demografico)
- Periodo analizzato
- Tipologie coorti da analizzare (A, B, C, o combinazione)

### Fase 2 â€” Pull dati
**Pre-Supermetrics MCP wiring (Sessione 8):**
- Brevo: export CSV iscritti + campagne (manuale)
- GA4: export comportamenti sessioni
- Meta/LinkedIn: insights dashboard manuale
- CRM Brevo lead: export

**Post-Supermetrics wiring:**
- Pull automatico via Supermetrics MCP
- Brevo API REST via shell library

### Fase 3 â€” Costruzione coorti
Aggregazione per tipologia (acquisizione/comportamentale/demografica) secondo definizioni sez. 3.

### Fase 4 â€” Calcolo retention & engagement
- Retention rate M+N = (N attivi M+N) / (N coorte iniziale)
- Engagement rate medio per coorte
- Conversion funnel coorte â†’ next stage

### Fase 5 â€” Insight + raccomandazioni
- 3-5 insight chiave (no piÃ¹, focus)
- 2-4 raccomandazioni iterazione (azionabili, con effort + stima impatto)

---

## 5. Pattern tipici e cosa significano

### Decadimento open-rate newsletter coorte recente
- M+1 80% â†’ M+3 70% â†’ M+6 60% = decadimento sano
- M+1 80% â†’ M+3 50% â†’ M+6 25% = decadimento patologico (welcome flow rotto, frequenza eccessiva, contenuti off-target)

### Volume "one-time" blog molto alto
- Normale per blog SEO-driven (utenti organici cercano risposta puntuale)
- Patologico se >85% del traffico (no costruzione audience nurture)
- Azione: lead magnet su articoli evergreen + CTA newsletter

### Dormant newsletter alta (>30% lista)
- Azione: re-engagement campaign (email-sequence dormant â†’ un'email "ci sei ancora?" â†’ 30gg â†’ unsub automatico se no apertura)

### Segmento "Patrimonializzati" sotto-rappresentato
- Audience B4 Patrimonio Ã¨ naturalmente piÃ¹ nascosta (privacy, no engagement pubblico)
- Misurare via lead CRM, non solo digital
- Possibile gap di posizionamento P6 + P9 nel mix editoriale

---

## 6. Cosa NON fare mai

- âŒ **Inventare segmentazione** (Brand Book v1.2 sez. 7 â€” no dati inventati)
- âŒ **Trattare ipotesi euristiche demografiche come fatti** â€” sempre "stimato qualitativamente"
- âŒ **Promettere conversion rate target garantiti** â€” dipendenza dal contenuto + offerta + mercato
- âŒ **Profilare in violazione GDPR** â€” segmentazione sempre su dati legalmente raccolti con consenso (Brand Book v1.2 sez. 7 Compliance + GDPR)
- âŒ **Esposizione dati personali** nei report (anonimizzare sempre, mai email + nomi nel report)
- âŒ **Aggregare coorti troppo piccole** (<30 unitÃ  â†’ variance alta, leggibilitÃ  nulla)
- âŒ **Ignorare il caveat statistico** â€” sotto soglia, analisi qualitativa, non quantitativa

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire la cohort analysis, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 3 segmenti target Â· sez. 5 strategia canali Â· sez. 7 Compliance + GDPR)
2. `/01_Team/07_Data_Analyst.md` + `/01_Team/08_CRM_Lead_Manager.md`
3. `config/brand.json` (segmenti target, canali, pillar)
4. `Output_approvati/data/` cohort-analysis precedenti (per evoluzione storica)
5. Dati grezzi disponibili (export Brevo, GA4, Meta/LinkedIn insights)
6. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:data-cohort-analysis â€” Sessione 5 Plugin Build â€” 2026-05-20*

