---
name: crm-lifecycle
description: Definisce e governa il customer journey dei lead/clienti Advisory+ lungo gli 8 lifecycle stage (welcome Â· engaged Â· power Â· at-risk Â· dormant Â· win-back Â· lost Â· customer). Orchestra: definizione regole di transizione (basate su comportamento + tempo + interazione) Â· trigger automatici Brevo per cambio stage Â· azioni associate (sequenza lead-nurture per welcome Â· contenuti premium per power Â· sequenza win-back per dormant Â· ecc.) Â· cron mensile di ricalcolo lifecycle stage per tutti i contatti. Output: mappa lifecycle stage completa + regole di transizione + KPI per stage + dashboard report mensile (alimenta data-monthly-performance-report sez. D coorti). Implementazione tecnica via Brevo automation + script `crm-lifecycle-recompute.sh` (Sessione 7).
---
# â™»ï¸ Skill crm-lifecycle â€” Customer journey 8 stage Advisory+

> **Lead â†’ welcome â†’ engaged â†’ power â†’ at-risk â†’ dormant â†’ win-back â†’ lost / customer. Cron mensile + Brevo automation.**

---

## 1. Quando triggera

- **Setup iniziale plugin v1.1** (questa sessione): definisce mappa lifecycle + regole transizione + KPI
- **Cron mensile** schedulato (1Â° del mese) via `scheduled-tasks` MCP (Sessione 8): ricalcolo lifecycle stage per tutti i contatti Brevo
- **Refresh annuale** in chat 06 Email & CRM
- Invocata da `advisory-plus:crm-lead-nurture` come componente del Welcome stage
- Invocata da `advisory-plus:crm-win-back` come componente del Win-back stage
- Invocata da `advisory-plus:data-cohort-analysis` come reference per analisi retention
- Mai auto-trigger continuo: brief MM o cron mensile

Tempo target: **30-45 min** setup iniziale, **10-15 min** refresh.

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/crm/[YYYY-MM-DD]_lifecycle-map_vN.md`:

```markdown
---
data: YYYY-MM-DD
versione: vN
n_lifecycle_stage: 8
cron_schedule: ricalcolo 1Â° del mese 03:00 (script crm-lifecycle-recompute.sh)
fonte_dati: Brevo events (open/click/form) + CRM (customer_status)
---

## Mappa lifecycle (diagramma testuale)

```
[NEW SIGNUP]
    â†“
[01 WELCOME] (21gg)
    â†“
[02 ENGAGED] â†â”€â†’ [04 AT-RISK]
    â†“                â†“
[03 POWER]      [05 DORMANT] (>90gg no-open)
                     â†“
                [06 WIN-BACK] (21gg)
                     â†“
                 [07 LOST] (no-engagement post-winback)
                     â†“ (auto-unsub)
                  [SUPPRESSED]

[ANY STAGE] â”€â”€â†’ [08 CUSTOMER] (manuale)
```

## Regole di transizione

[Tabella stage A â†’ stage B con condizione Â· timing Â· azione associata Â· responsabile]

## KPI per stage

[Tabella: distribuzione % contatti per stage Â· transition rate Â· target a regime]

## Cron mensile crm-lifecycle-recompute.sh

[Logica: per ogni contatto Brevo, calcolare stage attuale in base a regole, aggiornare tag LCS_*, trigger eventuali automation di passaggio stage]

## Dashboard report mensile

[Alimenta data-monthly-performance-report sez. D5 coorti â€” pattern emergenti lifecycle]
```

---

## 3. Gli 8 lifecycle stage â€” definizione operativa

### 01 â€” WELCOME (giorni 1-21 da signup)
- **Definizione**: lead nuovo, sequenza welcome flow in corso
- **Tag Brevo**: `LCS_01_welcome`
- **Azione associata**: sequenza `crm-lead-nurture` 5 email su 21gg
- **Transizione**:
  - â†’ ENGAGED se completa welcome flow + â‰¥1 click CTA
  - â†’ DORMANT se non apre â‰¥3 email su 5
  - â†’ CUSTOMER se diventa cliente prima della fine flow (manuale CEO)

### 02 â€” ENGAGED (rolling)
- **Definizione**: open rate ultimo 3 mesi â‰¥50% + click count â‰¥1
- **Tag Brevo**: `LCS_02_engaged`
- **Azione associata**: riceve newsletter mensile + drop pillar-of-month
- **Transizione**:
  - â†’ POWER se open rate â‰¥80% per 3 mesi + click â‰¥3 + interazione (form/contatto)
  - â†’ AT-RISK se open rate scende <30% per 2 mesi consecutivi

### 03 â€” POWER (rolling)
- **Definizione**: open rate â‰¥80% ultimo 3 mesi + click â‰¥3 + â‰¥1 interazione (form/contatto/risposta)
- **Tag Brevo**: `LCS_03_power`
- **Azione associata**: accesso a contenuti premium / beta-test nuove voci editoriali / inviti eventi prioritari / direct outreach soft 1-2x/anno
- **Transizione**:
  - â†’ ENGAGED se metriche scendono (downgrade graceful)
  - â†’ CUSTOMER se diventa cliente (manuale)
  - â†’ AT-RISK se open rate <30% per 2 mesi

### 04 â€” AT-RISK (rolling)
- **Definizione**: open rate <30% per 2 mesi consecutivi (ma ancora "vivo")
- **Tag Brevo**: `LCS_04_at_risk`
- **Azione associata**: riduzione frequenza email + email "ti stiamo perdendo?" soft (1 colpo) + preference center promosso
- **Transizione**:
  - â†’ ENGAGED se open rate risale â‰¥50% nei 2 mesi successivi
  - â†’ DORMANT se no-open per 90gg

### 05 â€” DORMANT (>90gg no-open)
- **Definizione**: no-open da 90gg
- **Tag Brevo**: `LCS_05_dormant`
- **Azione associata**: nessuna newsletter regolare Â· trigger sequenza win-back
- **Transizione**:
  - â†’ WIN-BACK automatico (trigger sequenza win-back 3 email su 21gg)

### 06 â€” WIN-BACK (giorni 1-21 da trigger)
- **Definizione**: sequenza riattivazione in corso
- **Tag Brevo**: `LCS_06_winback`
- **Azione associata**: skill `crm-win-back` (3 email graduate)
- **Transizione**:
  - â†’ ENGAGED se apre â‰¥1 email + click â‰¥1 CTA nei 21gg
  - â†’ LOST se completa sequenza senza engagement

### 07 â€” LOST (post-winback fallito)
- **Definizione**: win-back completato senza engagement
- **Tag Brevo**: `LCS_07_lost`
- **Azione associata**: **unsubscribe automatico** (lista pulita) + spostamento in suppression list permanente (GDPR right-to-be-forgotten compliance + sanitÃ  lista)
- **Transizione**: finale (no ritorno automatico â€” solo re-signup volontario)

### 08 â€” CUSTOMER (manuale CEO/MM)
- **Definizione**: lead diventato cliente Advisory+ (campo CRM dedicato `customer_status = active`)
- **Tag Brevo**: `LCS_08_customer`
- **Azione associata**: spostato in lista parallela "Advisory+ Clienti attivi" + frequenza email ridotta + comunicazioni utility prevalenti (rinnovi, sinistri, novitÃ  contrattuali)
- **Transizione**: rolling (puÃ² tornare a engaged se attivo, puÃ² andare in dormant clienti se inattivo dal canale email)

---

## 4. Regole di transizione (tabella completa)

| Da | A | Condizione | Timing | Azione automatica |
|---|---|---|---|---|
| NEW | WELCOME | signup_date set | 0 | Brevo trigger welcome flow |
| WELCOME | ENGAGED | welcome_completed + click_count â‰¥1 | giorno 22 | Tag LCS_engaged + newsletter regolare |
| WELCOME | DORMANT | open_count â‰¤2 su 5 email | giorno 22 | Tag LCS_dormant + pausa email |
| ENGAGED | POWER | open_rate_3m â‰¥80% AND click_count_3m â‰¥3 AND interaction_count_3m â‰¥1 | rolling mensile | Tag LCS_power + accesso premium |
| ENGAGED | AT-RISK | open_rate_2m <30% | rolling mensile | Tag LCS_at_risk + riduzione frequenza |
| POWER | ENGAGED | metriche scendono sotto soglia | rolling mensile | Downgrade graceful |
| AT-RISK | ENGAGED | open_rate_2m â‰¥50% | rolling mensile | Recovery |
| AT-RISK | DORMANT | no_open >90gg | rolling mensile | Trigger pausa |
| DORMANT | WIN-BACK | trigger manuale o cron mensile | rolling mensile | Brevo trigger win-back flow |
| WIN-BACK | ENGAGED | open â‰¥1 + click â‰¥1 in 21gg | giorno 22 da trigger | Ritorno engaged |
| WIN-BACK | LOST | no_engagement post 21gg | giorno 22 da trigger | Auto-unsubscribe + suppression |
| LOST | (suppressed) | finale | immediato | Nessuna ricostruzione automatica |
| ANY | CUSTOMER | customer_status = active | manuale | Spostamento lista clienti |
| CUSTOMER | (any) | customer_status = inactive (rinuncia contratto) | manuale | Decisione MM caso-per-caso |

---

## 5. KPI per stage (riferimento data-monthly-performance-report sez. D)

| Stage | % lista (target a regime) | Transition rate atteso |
|---|---|---|
| WELCOME | 5-10% | â†’ENGAGED 70-80% |
| ENGAGED | 40-50% | â†’POWER 5-10% / â†’AT-RISK 10-15% |
| POWER | 5-10% | stable rolling |
| AT-RISK | 5-10% | â†’ENGAGED 30-40% / â†’DORMANT 60-70% |
| DORMANT | 15-25% | â†’WIN-BACK 100% (automatico) |
| WIN-BACK | 5-10% | â†’ENGAGED 20-30% / â†’LOST 70-80% |
| LOST | (purged) | 0% (suppressed) |
| CUSTOMER | 5-15% | rolling |

**Soglia di allarme**: se DORMANT + AT-RISK >40% della lista per 2 mesi consecutivi â†’ revisione strategia editoriale (frequenza? voce? rilevanza?).

---

## 6. Cron mensile `crm-lifecycle-recompute.sh` (logica)

Schedulato 1Â° del mese 03:00. Per ogni contatto attivo in Brevo:
1. Pull metriche ultimi 3 mesi (open_rate, click_count, interaction_count, days_since_last_open)
2. Calcola stage attuale secondo regole transizione (sez. 4)
3. Se diverso da stage corrente: update tag LCS_* + trigger automation se applicabile (es. WIN-BACK flow)
4. Log nuovo stage in `/Log_pubblicati/lifecycle_recompute_[YYYY-MM]_log.md`
5. Aggrega report distribuzione % stage â†’ handoff a `data-monthly-performance-report` sez. D5

Eccezioni:
- Stage CUSTOMER: mai modificato automaticamente (solo manuale)
- Stage LOST: terminale (no re-elaborazione)
- Stage WELCOME: gestito dal trigger welcome flow, non da cron (anti-doppia automation)

---

## 7. Compliance & privacy

âœ… **No profilazione sensibile**: lifecycle stage Ã¨ basato SOLO su comportamento aggregato (open/click/days_since), non su categorie particolari GDPR Art. 9
âœ… **Diritto cancellazione**: utente puÃ² richiedere unsubscribe in qualsiasi stage â†’ spostamento immediato in suppression list
âœ… **Diritto rettifica**: utente puÃ² aggiornare preferenze via preference center
âœ… **Audit log**: ogni transizione stage loggata (data + condizione che ha triggerato)
âœ… **Retention**: stage LOST mantiene lo storico per audit GDPR ma non riceve comunicazioni
âœ… **Customer stage**: solo manuale CEO/MM (no inferenza automatica da comportamento email â€” il customer Ã¨ quello con contratto firmato)

---

## 8. Cosa NON fare mai

- âŒ **Inferire stage CUSTOMER** da comportamento email (Ã¨ un fatto, non un comportamento)
- âŒ **Saltare il cron mensile** (lifecycle si fossilizza, decisioni downstream errate)
- âŒ **Modificare regole transizione senza notifica MM** (impatto downstream su lead-nurture Â· win-back Â· monthly-report)
- âŒ **Trigger WIN-BACK piÃ¹ volte** allo stesso utente in <12 mesi (rischio fatigue)
- âŒ **Mantenere LOST in lista attiva** (anti-spam Â· pulizia lista Â· sanitÃ  deliverability)
- âŒ **Profilazione con dati sensibili** (no etnia, religione, salute â€” GDPR Art. 9)
- âŒ **Combinare lifecycle stage con segmenti demografici inferiti** (segmenti demografici sono SOLO self-declared, vedi crm-segmentation)
- âŒ **Email post-LOST** (utente Ã¨ suppressed, GDPR rispettato)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di applicare/aggiornare lifecycle, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia canali Â· sez. 7 Compliance + GDPR)
2. `/01_Team/08_CRM_Lead_Manager.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json`
4. `Output_approvati/crm/` lifecycle precedente + segmentation schema + lead-nurture flow
5. Brevo current data (export comportamento ultimi 3 mesi)
6. Il brief operativo del MM o cron schedulato

---

*SKILL v1.0 â€” advisory-plus:crm-lifecycle â€” Sessione 6 Plugin Build â€” 2026-05-21*

