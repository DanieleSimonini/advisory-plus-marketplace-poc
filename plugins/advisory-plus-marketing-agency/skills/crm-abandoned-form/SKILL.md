---
name: crm-abandoned-form
description: Sequenza recupero form abbandonato (es. lead ha iniziato il form "richiedi consulenza" o "prenota call" sul sito advisoryplus.it ma non ha completato il submit). 2 email graduate su 7 giorni (giorno +1 Â· giorno +5) con tono UTILITY e accessibilitÃ  rapida â€” link che riporta al form pre-compilato (Brevo dynamic fields), no push, no senso di colpa. Voce dominante Spiegato Facile, NO Caso Reale nÃ© Analisi (registro mismatch â€” utility prevale). Auto-exit se utente completa il form o se sceglie esplicitamente di non procedere. Implementazione Brevo automation + integrazione form analytics sito (UTM parameter + form ID + completion percentage). Anti-fatigue cap: stesso form non triggera sequenza piÃ¹ di 1 volta in 30 giorni.
---
# ðŸ“ Skill crm-abandoned-form â€” Recupero form abbandonato (2 email Â· 7gg Â· tono utility)

> **Form parzialmente compilato â†’ ripresa rapida. No push. Compliance gate-doppio. Cap 1 trigger/30gg.**

---

## 1. Quando triggera

- **Auto-trigger Brevo** quando form sul sito advisoryplus.it Ã¨ abbandonato (compilato â‰¥30% ma non submit) entro 24h â†’ ingest da form analytics + email field giÃ  catturato + trigger flow 2 email
- Invocata in **setup iniziale plugin v1.1** per definire il flow Brevo
- Invocata in **refresh annuale** per revisione tono
- Invocata da `advisory-plus:crm-lifecycle` come azione opzionale (non lifecycle stage, ma azione laterale)
- **Anti-fatigue cap**: stesso form (identificato da `form_id`) non triggera sequenza piÃ¹ di 1 volta in 30 giorni per lo stesso utente

Tempo target di esecuzione: **20-30 min** per produzione 2 email.

---

## 2. Output finale atteso

**Pacchetto Markdown** in `Output_approvati/crm/[YYYY-MM-DD]_abandoned-form-flow.md` + 2 file email separati:

```markdown
---
data: YYYY-MM-DD
flow: abandoned-form-advisoryplus
trigger_brevo: form_abandoned_event (form_id, completion_percentage â‰¥30%, email_field set)
durata_totale: 7 giorni
n_email: 2
exit_conditions: [form_completed â†’ ENGAGED + tag completed Â· 7gg no-action â†’ exit silently + tag abandoned_lost]
anti_fatigue_cap: stesso form max 1 trigger/30gg per utente
compliance: ðŸŸ¢
---

## Calendario sequenza
| # | Giorno | Subject | Preview | Voce | Tono |
|---|---|---|---|---|---|
| 1 | +1 | "Hai lasciato qualcosa a metÃ " | "Riprendi da dove ti eri fermato â€” un click" | Spiegato Facile | utility Â· accessibilitÃ  |
| 2 | +5 | "Possiamo aiutarti diversamente?" | "Se preferisci, una breve telefonata. O nessuna delle due." | Spiegato Facile | rispettoso Â· alternative |
| (3) | +7 | (no email Â· exit silently) | â€” | â€” | exit gracefully |

[Brevo automation setup tecnico â€” integrazione form analytics + UTM]

[Compliance check]
```

---

## 3. Struttura delle 2 email

### Email #1 â€” Giorno +1 Â· "Hai lasciato qualcosa a metÃ "
- **Voce**: Spiegato Facile
- **Subject candidati**:
  - "Hai lasciato qualcosa a metÃ "
  - "Riprendiamo da dove ti eri fermato?"
  - "Quel form aspetta â€” un click"
- **Preview**: "Riprendi da dove ti eri fermato â€” un click."
- **Body**: 150-200p
- **Struttura**:
  - Riconoscimento fattuale ("Ieri hai iniziato a compilare il form '[form_name]' su advisoryplus.it ma non l'hai concluso â€” capita")
  - Rassicurazione ("I dati che hai inserito sono salvati â€” non serve ricominciare")
  - CTA forte e una: link diretto al form pre-compilato (URL con token Brevo che recupera lo stato)
  - Chiusura: "Se hai cambiato idea o preferisci parlare con noi prima di compilare, basta rispondere a questa email."
- **CTA primaria**: link form pre-compilato
- **CTA secondaria** (testo nel body, non bottone): "Oppure scrivici per fare due chiacchiere prima"
- **Tono**: utility, fattuale, no push, no guilt

### Email #2 â€” Giorno +5 Â· "Possiamo aiutarti diversamente?"
- **Voce**: Spiegato Facile
- **Subject**: "Possiamo aiutarti diversamente?"
- **Preview**: "Se preferisci una breve telefonata. O nessuna delle due."
- **Body**: 150-200p
- **Struttura**:
  - Riconoscimento ("Capita che il form non sia il modo giusto per arrivare a una cosa che richiede una chiacchierata")
  - 3 alternative esplicite:
    1. "Completa il form ora" â†’ link form pre-compilato
    2. "Prenota una breve call introduttiva" â†’ link calendly/cal.com (CTA secondaria)
    3. "Non piÃ¹ interessato? Nessun problema â€” ignora questa email"
  - Chiusura: "Se non senti nulla, dopo 2 giorni non ti scriviamo piÃ¹ su questa cosa. Promesso."
- **CTA primaria**: link form pre-compilato
- **CTA secondaria**: link prenota call
- **Tono**: rispettoso, alternative chiare, exit graceful esplicitato

### (Email #3 â€” Giorno +7 Â· EXIT SILENTLY)
- **Nessuna email inviata**
- **Azione**: tag `BHV_abandoned_form_lost_[form_id]_[YYYY-MM-DD]` aggiunto (per analytics futuri) + uscita flow
- **No notifica**: l'utente non riceve "ti abbiamo perso" nÃ© altro

---

## 4. Personalizzazione (Brevo dynamic fields)

Dati passati dal form analytics al trigger Brevo:
- `email` (obbligatorio â€” senza non parte il flow)
- `form_id` (es. `richiedi_consulenza_pmi`, `prenota_call_famiglia`, `richiedi_preventivo_yacht`)
- `form_name` (human-readable per email body)
- `completion_percentage` (es. 60% â€” info interna, non in email)
- `resume_url` (link con token che recupera lo stato del form)
- `segment_implicito` (se il form ha campo "tipo cliente" giÃ  selezionato â€” usabile per personalizzare lievemente)

âš ï¸ **No personalizzazione invasiva**: l'email non deve sembrare che "sappiamo troppo". Riconoscimento fattuale ("hai iniziato il form") senza dettagli intrusivi sul contenuto compilato.

---

## 5. Exit conditions del flow

- **COMPLETED**: utente clicca link â†’ completa form â†’ tag `BHV_form_completed_[form_id]` + uscita flow + handoff a `crm-lifecycle` per attivazione stage opportuno
- **EXIT SILENT**: 7gg senza completion â†’ tag `BHV_abandoned_form_lost_[form_id]` + uscita silent (nessuna email finale)
- **OPT-OUT**: utente clicca unsubscribe â†’ immediato spostamento suppression list (override anche del flow corrente)
- **CALL booked**: utente clicca CTA secondaria call â†’ tag `BHV_call_booked` + uscita flow + handoff manuale CEO/MM per follow-up
- **EXPLICIT NO**: utente risponde "non interessato" â†’ uscita flow + tag `BHV_abandoned_form_explicit_no_[form_id]` (rispetto)
- **CRISIS mode** o **KILL switch attivo**: flow non parte / si interrompe

---

## 6. Compliance baseline (gate-doppio pre-attivazione)

âœ… **Disclaimer RUI integrale** in footer ogni email
âœ… **Denominazione mandatarie corretta** se citate (improbabile in queste 2 email â€” utility, non promozionali)
âœ… **Unsubscribe link** funzionante
âœ… **Indirizzo mittente fisico** in footer
âœ… **No urgency fittizia** ("ULTIMA POSSIBILITÃ€", "OFFERTA SCADE" â€” vietati anche perchÃ© Ã¨ utility, non promo)
âœ… **No guilt-tripping** ("hai abbandonato il form" passivo-aggressivo evitato)
âœ… **No claim ðŸ”´** vietati
âœ… **GDPR â€” base giuridica**: utente ha giÃ  fornito email nel form (consenso esplicito al contatto). Email di reminder Ã¨ coerente con la finalitÃ  per cui l'email Ã¨ stata raccolta (Art. 6.1.b GDPR â€” esecuzione misure precontrattuali su richiesta dell'interessato)
âœ… **Privacy by design**: nessun dettaglio intrusivo sul contenuto del form compilato nell'email body
âœ… **Anti-fatigue cap**: stesso form/utente max 1 trigger/30gg (Brevo condizione `last_abandoned_form_trigger > 30 days ago`)

---

## 7. KPI abandoned-form (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Open rate Email #1 | â‰¥40% (alta intent â€” utente conosce giÃ  il brand) |
| Open rate Email #2 | â‰¥25% |
| Completion rate (form â†’ submitted post-flow) | 15-25% |
| Call booking rate (CTA secondaria) | 5-10% |
| Lost rate finale | 65-80% |
| Unsubscribe rate sequenza | <1% |

**Insight**: completion rate 15-25% Ã¨ risultato sano. Lost rate maggioranza Ã¨ atteso (l'utente ha abbandonato per ragione, riportarlo costa). ROI del flow = bassa fatica, alto valore marginale sui pochi recuperati.

---

## 8. Integrazione tecnica (Sessione 7 publish + form analytics)

### Tracciamento abbandono form
- Form sul sito advisoryplus.it deve avere tracking JavaScript che invia evento a Brevo (o API endpoint Brevo) quando:
  - Utente raggiunge 30% completion E ha fornito email E lascia la pagina senza submit entro 24h
- Payload evento: `{email, form_id, form_name, completion_percentage, resume_url, timestamp}`
- Brevo riceve evento â†’ trigger automation flow â†’ invio Email #1 a giorno +1

### Resume URL
- Link con token unico che recupera lo stato del form (richiede storage temporaneo lato server sito â€” implementazione webmaster, NON in scope plugin v1.1)
- Token TTL: 14 giorni (poi expire automatico, utente ricompila da zero)
- Sicurezza: token non contiene dati sensibili in chiaro, solo riferimento

### Handoff completion
- Form completato â†’ webhook a Brevo â†’ tag `BHV_form_completed_[form_id]` + uscita flow + trigger lifecycle stage opportuno (es. ENGAGED se non era cliente, o passaggio a CRM clienti se diventa cliente)

---

## 9. Logica di esecuzione â€” passo-passo

1. **Ricevere brief MM** (setup iniziale o refresh)
2. **Cascata di contesto** (sez. 10)
3. **Per Email #1**: invoca `voce-spiegato-facile` via Task (sez. 3.1)
4. **Per Email #2**: invoca `voce-spiegato-facile` via Task (sez. 3.2)
5. **Aggiungere header** (subject + preview) + footer (disclaimer RUI + unsubscribe + indirizzo)
6. **Verificare**: subject â‰¤50 char, preview â‰¤90 char, body 150-200p
7. **Invocare** `advisory-plus:compliance-gate-doppio`
8. **Se ðŸŸ¡**: riformulazione, ri-check
9. **Se ðŸŸ¢**: comporre pacchetto deliverable
10. **Generare brief tecnico Brevo automation** (trigger + 2 step + exit conditions + anti-fatigue cap + integrazione form analytics)
11. **Consegna al MM** per approvazione esplicita CEO + handoff a webmaster per setup tracking JS

---

## 10. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 7 Compliance + GDPR)
2. `/01_Team/08_CRM_Lead_Manager.md` + `/01_Team/02_Copywriter.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` + `config/compagine.json`
4. `Output_approvati/crm/` altri flow (lead-nurture, win-back) per coerenza tono
5. Lista form attivi sul sito advisoryplus.it (handoff webmaster, anagrafica form_id)
6. Il brief operativo del MM

---

## 11. Cosa NON fare mai

- âŒ **Riferimenti intrusivi** al contenuto compilato ("Ho visto che hai inserito il tuo reddito diâ€¦" â†’ vietato, GDPR + privacy by design)
- âŒ **Urgency fittizia** ("OFFERTA SCADE OGGI", "ULTIMA POSSIBILITÃ€" â€” sono utility, non promo)
- âŒ **Guilt-tripping** ("ci hai abbandonato a metÃ  strada")
- âŒ **PiÃ¹ di 2 email per abbandono** (anti-fatigue + rispetto utente)
- âŒ **PiÃ¹ di 1 trigger/30gg** per stesso utente/form
- âŒ **Push commerciale** ("compra ora" â€” l'email serve a riprendere il form, non a vendere)
- âŒ **Saltare gate-doppio Compliance**
- âŒ **Trigger su form con <30% completion** (segnale debole, rischio spam)
- âŒ **Trigger su utente che non ha ancora dato consenso esplicito** (se email field non Ã¨ obbligatorio nel form â†’ no trigger)
- âŒ **Conservare token resume oltre 14gg** (cleanup automatico)

---

*SKILL v1.0 â€” advisory-plus:crm-abandoned-form â€” Sessione 6 Plugin Build â€” 2026-05-21*

