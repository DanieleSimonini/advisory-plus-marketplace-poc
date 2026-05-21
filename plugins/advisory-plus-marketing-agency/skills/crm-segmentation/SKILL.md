---
name: crm-segmentation
description: Definisce, manutiene e applica la segmentazione della lista Brevo (newsletter Advisory+) lungo 3 dimensioni â€” (A) DEMOGRAFICA sui 8 segmenti target Brand Book v1.2 sez. 3 in 4 cluster (Privati & Famiglie Â· Patrimonio Â· Lavoro & Impresa Â· Terzo Settore & Specialty); (B) LIFECYCLE STAGE (welcome Â· engaged Â· power Â· at-risk Â· dormant Â· win-back Â· lost Â· customer); (C) BEHAVIOR TAGS (apri-regolari/casual/dormant newsletter Â· click-pillar P[N] Â· download lead-magnet Â· partecipa evento Â· risposte sondaggio). Output: schema tag/lista/folder Brevo + regole di auto-tagging + GDPR compliance + privacy by design. Implementazione via Brevo automation rules + script `crm-tag-update` (Sessione 7). Refresh schema annuale o post-evento strutturale (es. lancio nuovo segmento).
---
# ðŸ—‚ Skill crm-segmentation â€” Schema segmentazione Brevo (3 dimensioni)

> **8 segmenti Ã— 8 lifecycle stage Ã— N behavior tags. GDPR by design. Auto-tagging via Brevo automation rules.**

---

## 1. Quando triggera

- **Setup iniziale plugin v1.1** (questa sessione): definisce schema segmentazione completo
- **Refresh annuale** in chat 08 Performance & Analytics o chat 06 Email & CRM
- **Post-evento strutturale** (lancio nuovo cluster target, riposizionamento brand, nuovo pillar permanente)
- Invocata da `advisory-plus:crm-lifecycle` come dipendenza (lifecycle stage = sotto-insieme dei tag)
- Invocata da `advisory-plus:data-cohort-analysis` per cross-mapping coorti
- Invocata da `advisory-plus:crm-lead-nurture` per personalizzazione segment-based
- Mai auto-trigger continuo: brief MM o refresh schedulato

Tempo target di esecuzione: **30-60 minuti** in setup iniziale, **15-30 min** in refresh.

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/crm/[YYYY-MM-DD]_segmentation-schema_vN.md`:

```markdown
---
data: YYYY-MM-DD
versione: vN
piattaforma: Brevo (lista master "Advisory+ Newsletter")
dimensioni: 3 (demografica Â· lifecycle Â· behavior)
n_segmenti_demografici: 8
n_lifecycle_stage: 8
n_behavior_tag_base: ~15-20
gdpr_compliance: âœ… verificato
---

## A. Dimensione demografica (8 segmenti target Brand Book v1.2 sez. 3)

[Tag naming: SEG_[id]_[short_name] â€” es. SEG_01_famiglie_giovani]

| Tag | Segmento | Cluster | Pillar dominante mappato | Note GDPR |
|---|---|---|---|---|
| SEG_01_famiglie_giovani | Famiglie giovani genitori (30-45) | A Privati & Famiglie | P4 Famiglia & Vita | self-declared opt-in |
| SEG_02_adulti_genitori_anziani | Adulti 45-60 con genitori anziani | A | P5 AnzianitÃ  & LTC | self-declared opt-in |
| SEG_03_pre_pensionati | Pre-pensionati 55-65 | A | P6 Risparmio & Investimento | self-declared opt-in |
| SEG_04_patrimonializzati | Patrimonializzati | B Patrimonio | P6 + P8 | self-declared opt-in (delicato â€” solo opt-in volontario) |
| SEG_05_professionisti | Professionisti & P.IVA | C Lavoro & Impresa | P9 Imprese & Professionisti | self-declared opt-in |
| SEG_06_pmi_famigliari | PMI famigliari | C | P9 | self-declared opt-in |
| SEG_07_imprese_strutturate | Imprese strutturate | C | P9 + P7 | self-declared opt-in |
| SEG_08_terzo_settore | Enti del Terzo Settore | D Terzo Settore & Specialty | P12 Specialty | self-declared opt-in |
| SEG_09_specialty_yacht_arte_religiosi | Specialty | D | P10 Â· P11 Â· P12 | self-declared opt-in |

âš ï¸ **Self-declared only**: il segmento NON Ã¨ inferito automaticamente da analisi comportamentale (rischio profiling indebito GDPR). Il segmento Ã¨ dichiarato dal lead in fase di signup (campo dropdown opzionale) o aggiornato successivamente dal lead stesso via preference center.

## B. Dimensione lifecycle stage (8 stage)

[Tag naming: LCS_[id]_[short_name]]

| Tag | Stage | Definizione | Durata tipica | Trigger di passaggio |
|---|---|---|---|---|
| LCS_01_welcome | Welcome | Lead nuovo, sequenza welcome flow in corso | 21 giorni | Auto: 21gg da signup |
| LCS_02_engaged | Engaged | Apre regolarmente (â‰¥50% open rate ultimo 3 mesi) + ha cliccato almeno 1 CTA | rolling | Auto: comportamento |
| LCS_03_power | Power | Apre quasi sempre (â‰¥80%) + click â‰¥3 mesi consecutivi + interazione (form/contatto/risposta) | rolling | Auto: comportamento |
| LCS_04_at_risk | At-risk | Open rate scende sotto 30% per 2 mesi consecutivi | rolling | Auto: comportamento |
| LCS_05_dormant | Dormant | Non apre da 90gg | rolling | Auto: 90gg no-open |
| LCS_06_winback | Win-back | Sequenza riattivazione in corso (3 email graduate) | 21 giorni | Auto: trigger win-back da Dormant |
| LCS_07_lost | Lost | Win-back fallito (no engagement post-sequenza) | finale | Auto: post-winback no-engagement â†’ unsub automatico |
| LCS_08_customer | Customer | Diventato cliente Advisory+ (campo CRM dedicato `customer_status = active`) | rolling | Manuale CEO/MM |

## C. Dimensione behavior tags (~15-20 tag base)

[Tag naming: BHV_[area]_[detail]]

### Behavior â€” engagement newsletter
- BHV_open_regular (â‰¥50% open rate ultimo 3 mesi)
- BHV_open_dormant (no-open ultimi 90gg)
- BHV_click_active (â‰¥1 click ultimo mese)

### Behavior â€” pillar interest (auto-set su click CTA blog/newsletter)
- BHV_pillar_P1_educazione Â· BHV_pillar_P2_voce_ceo Â· BHV_pillar_P3_news
- BHV_pillar_P4_famiglia Â· BHV_pillar_P5_ltc Â· BHV_pillar_P6_risparmio
- BHV_pillar_P7_tutela_legale Â· BHV_pillar_P8_casa Â· BHV_pillar_P9_imprese
- BHV_pillar_P10_yacht Â· BHV_pillar_P11_arte Â· BHV_pillar_P12_terzo_settore

### Behavior â€” lead-magnet/event
- BHV_lead_magnet_downloaded Â· BHV_event_partecipato Â· BHV_survey_compilato

## D. Regole di auto-tagging Brevo

[Documentazione regole automation Brevo per ogni tag dinamico â€” implementazione tecnica Sessione 7 publish/brevo scripts]

## E. GDPR & privacy by design

[Verifica conformitÃ : consenso esplicito Â· base giuridica Â· diritto cancellazione Â· profilazione limitata a comportamento self-declared]

## F. Refresh schedule
- Refresh schema: annuale o post-evento strutturale
- Pulizia tag obsoleti: trimestrale
- Audit GDPR: annuale
```

---

## 3. Logica di auto-tagging (Brevo automation rules)

### 3.1 Tag demografici (SEG_*)
- **Solo self-declared** via campo dropdown form newsletter o preference center
- **Update**: lead puÃ² cambiare segmento via preference center
- **No inferenza** da comportamento (GDPR â€” no profilazione indebita)

### 3.2 Tag lifecycle (LCS_*)
- **Auto-set** via Brevo automation rules basate su comportamento aggregato:
  - LCS_welcome â†’ signup_date - 21 giorni
  - LCS_engaged â†’ open_rate_3m â‰¥ 50% AND click_count_3m â‰¥ 1
  - LCS_power â†’ open_rate_3m â‰¥ 80% AND click_count_3m â‰¥ 3 AND interaction_count_3m â‰¥ 1
  - LCS_at_risk â†’ open_rate_2m < 30%
  - LCS_dormant â†’ days_since_last_open > 90
  - LCS_winback â†’ triggered_winback_flow = true
  - LCS_lost â†’ winback_flow_completed = true AND no_engagement = true
  - LCS_customer â†’ customer_status = active (manuale)
- **Update mensile** via cron `crm-lifecycle-recompute.sh` (Sessione 7 publish/scripts)

### 3.3 Tag behavior (BHV_*)
- **Engagement**: auto-set via Brevo behavior tracking nativo
- **Pillar interest**: auto-set via UTM parameter su CTA blog/newsletter (es. `utm_campaign=P5_ltc_caso_reale_giugno` â†’ tag BHV_pillar_P5_ltc)
- **Lead-magnet/event**: auto-set su form submission specifici (lead magnet download form, event registration form)
- **Decay**: tag pillar interest decade dopo 6 mesi se nessun nuovo click su quel pillar (auto-cleanup mensile)

---

## 4. Naming convention tag

### Pattern obbligatorio
```
[DIMENSIONE]_[id]_[short_name]
```

### Esempi
- `SEG_05_professionisti` â€” demografica
- `LCS_03_power` â€” lifecycle stage
- `BHV_pillar_P7_tutela_legale` â€” behavior interest

### Vietati
- âŒ Spazi nel nome tag (rotture Brevo automation)
- âŒ Caratteri speciali (italics, accenti) â€” usare ASCII
- âŒ Maiuscolo misto (tutto lowercase tranne il prefisso 3-letter)
- âŒ Tag generici non-strutturati ("interessante", "prioritario", "vip") â€” sempre dimensione + id

---

## 5. Folder structure Brevo

```
ðŸ“ Lista master: "Advisory+ Newsletter"
   â”œâ”€ Tag demografici (SEG_*)
   â”œâ”€ Tag lifecycle (LCS_*)
   â”œâ”€ Tag behavior (BHV_*)
   â””â”€ Smart segments (combinazioni filtri AND/OR per campagne ad-hoc)

ðŸ“ Lista parallela: "Advisory+ Clienti attivi"
   â””â”€ Sync con CRM clienti (manuale, riservato)

ðŸ“ Lista parallela: "Advisory+ Eventi" (opt-in separato per inviti eventi)
   â””â”€ Opt-in indipendente dalla newsletter

ðŸ“ Lista soppressione: "Advisory+ Unsubscribed"
   â””â”€ Permanent suppression list (GDPR right-to-be-forgotten compliance)
```

---

## 6. GDPR by design â€” checklist obbligatoria

âœ… **Consenso esplicito** raccolto via form opt-in (no pre-check, no opt-in implicito)
âœ… **Base giuridica documentata**: consenso libero, specifico, informato, revocabile (Art. 6.1.a GDPR)
âœ… **Preference center accessibile** in ogni email (link footer)
âœ… **Diritto cancellazione** rispettato (unsubscribe immediato + persistenza in suppression list)
âœ… **Diritto portabilitÃ **: lead puÃ² richiedere export dei propri dati (via richiesta scritta a info@advisoryplus.it)
âœ… **Diritto rettifica**: lead puÃ² aggiornare segmento via preference center
âœ… **No profilazione indebita**: segmento demografico SOLO self-declared
âœ… **Minimizzazione dati**: raccogliamo solo campi necessari (email obbligatorio Â· nome opzionale Â· segmento opzionale Â· interessi opzionali)
âœ… **Retention policy**: dormant >24 mesi â†’ unsubscribe automatico + spostamento in suppression list
âœ… **Audit GDPR**: annuale, documentato in `99_Archivio/GDPR_audit_[anno].md`

---

## 7. Smart segments tipici (combinazioni)

| Smart segment | Filtro | Use case |
|---|---|---|
| Engaged Famiglie | SEG_01 AND LCS_engaged | Campagna pillar P4 Famiglia & Vita |
| Power readers | LCS_power (qualunque SEG) | Beta-test nuove voci editoriali Â· early access contenuti |
| At-risk con click recente | LCS_at_risk AND BHV_click_active | Win-back soft prima di sequenza piena |
| Dormant â‰¥90gg | LCS_dormant | Trigger win-back sequence |
| Interessati a LTC | BHV_pillar_P5_ltc (qualunque SEG) | Newsletter speciale pillar-of-month P5 |

---

## 8. Cosa NON fare mai

- âŒ **Profilare segmento demografico** da comportamento (no inferenza â€” solo self-declared)
- âŒ **Cross-referenziare** con altre liste senza consenso esplicito (GDPR)
- âŒ **Vendere/condividere** la lista con terze parti (mai)
- âŒ **Mantenere dormant >24 mesi** senza purge (GDPR retention)
- âŒ **Tag liberi** non strutturati (no naming convention = caos)
- âŒ **Cancellare definitivamente unsubscribed** dalla suppression list (mantenere per evitare re-add accidentale)
- âŒ **Refresh schema senza notifica MM** (cambi struttura tag impattano automation downstream)
- âŒ **Tag con dati personali sensibili** (no SEG_X_disabile, no SEG_X_malato â€” categorie particolari GDPR Art. 9)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di definire/aggiornare schema, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 3 segmenti target Â· sez. 6 Pillar Map Â· sez. 7 Compliance + GDPR)
2. `/01_Team/08_CRM_Lead_Manager.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (8 segmenti target dichiarati Â· 12 pillar)
4. `Output_approvati/crm/` schema precedenti (per evoluzione)
5. `Output_approvati/crm/` lifecycle + lead-nurture + win-back skill (per coerenza cross-skill)
6. `99_Archivio/GDPR_audit_*.md` se esistente
7. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:crm-segmentation â€” Sessione 6 Plugin Build â€” 2026-05-21*

