---
name: crm-win-back
description: Sequenza riattivazione dormant (>90gg no-open) â†’ 3 email graduate su 21 giorni (giorno 0 Â· giorno 7 Â· giorno 14) + auto-unsubscribe finale se nessun engagement. Tono RISPETTOSO, no senso di colpa, no urgenza fittizia, no push commerciale. Voce dominante Spiegato Facile, ultima email Caso Reale con disclaimer "Caso reale, nomi di fantasia" come ultimo tentativo emotivo. Exit gracefully: se utente non risponde, auto-unsub + spostamento in suppression list permanente (GDPR + sanitÃ  lista). Compliance gate-doppio pre-attivazione + cap frequenza: stesso utente NON puÃ² ricevere win-back piÃ¹ di 1 volta in 12 mesi (anti-fatigue). Implementazione Brevo automation triggered da skill `crm-lifecycle` quando contatto entra in stage DORMANT.
---
# ðŸ”„ Skill crm-win-back â€” Riattivazione dormant (3 email Â· 21gg Â· exit gracefully)

> **Tono rispettoso. No colpevolizzazione. Auto-unsub se silenzio. Compliance gate-doppio.**

---

## 1. Quando triggera

- **Auto-trigger Brevo** quando contatto entra in stage `LCS_05_dormant` (>90gg no-open) â†’ trigger flow win-back (3 email su 21gg)
- Invocata in **setup iniziale plugin v1.1** per definire il flow Brevo
- Invocata in **refresh annuale** per revisione tono e esempi
- Invocata da `advisory-plus:crm-lifecycle` come componente del Win-back stage
- Mai trigger manuale per singolo utente (sempre via lifecycle cron)
- **Anti-fatigue cap**: stesso utente non puÃ² ricevere win-back piÃ¹ di 1 volta in 12 mesi

Tempo target di esecuzione: **30-45 min** per produzione 3 email.

---

## 2. Output finale atteso

**Pacchetto Markdown** in `Output_approvati/crm/[YYYY-MM-DD]_winback-flow.md` + 3 file email separati:

```markdown
---
data: YYYY-MM-DD
flow: winback-newsletter-advisoryplus
trigger_brevo: tag_added "LCS_05_dormant"
durata_totale: 21 giorni
n_email: 3
exit_conditions: [apre +click â‰¥1 â†’ ENGAGED Â· completa 21gg senza engagement â†’ LOST + auto-unsub]
anti_fatigue_cap: stesso utente max 1 win-back/12 mesi
compliance: ðŸŸ¢
---

## Calendario sequenza
| # | Giorno | Subject | Preview | Voce | Tono |
|---|---|---|---|---|---|
| 1 | 0 (immediata) | "Ti stiamo perdendo?" o variante | ... | Spiegato Facile | dolce richiamo |
| 2 | +7 | "Cosa puoi cambiare nelle tue preferenze" | ... | Spiegato Facile | utility Â· preference center |
| 3 | +14 | "Un ultimo caso reale" | ... | Caso Reale | emotivo finale |
| (4) | +21 | (no email Â· auto-unsub se no engagement) | â€” | â€” | exit gracefully |

[Brevo automation setup tecnico]

[Compliance check]
```

---

## 3. Struttura delle 3 email

### Email #1 â€” Giorno 0 Â· "Ti stiamo perdendo?"
- **Voce**: Spiegato Facile
- **Subject candidati** (test A/B opzionale):
  - "Ti stiamo perdendo?"
  - "Ci sei ancora?"
  - "Una domanda veloce"
- **Preview**: "Ci basta un click â€” o pochi secondi per cambiare le preferenze."
- **Body**: 200-250p
- **Struttura**:
  - Riconoscimento ("Da un po' non ci leggi piÃ¹ â€” vogliamo solo capire se ha ancora senso restare in contatto")
  - 3 opzioni esplicite per il lettore:
    1. "Voglio continuare, ma con meno frequenza" â†’ preference center
    2. "Voglio cambiare argomenti" â†’ preference center (segmento + pillar)
    3. "Preferisco lasciarmi guidare" â†’ no-action (1 click su CTA conferma)
  - "Se non senti nulla, dopo 21 giorni ti rimuoviamo dolcemente dalla lista â€” niente di personale"
- **CTA**: preference center + "Resto in contatto" (1 click)
- **Tono**: caldo, rispettoso, fattuale, no colpevolizzazione

### Email #2 â€” Giorno +7 Â· "Cosa puoi cambiare"
- **Voce**: Spiegato Facile
- **Subject**: "Cosa puoi cambiare nelle tue preferenze"
- **Preview**: "Voci, frequenza, argomenti â€” tutto modulabile in pochi click."
- **Body**: 200-250p
- **Struttura**:
  - Re-introduzione delle 4 voci editoriali (Spiegato Facile Â· Badvisor Â· Caso Reale Â· Analisi) â€” 1 riga ciascuna
  - 12 pillar in 3 colonne (Always-on Â· Pillar di mese Â· Specialty) â€” link per scegliere quali ricevere
  - "Se solo gli argomenti specifici ti interessano, possiamo limitare a quelli"
- **CTA**: preference center (con pre-fill segmento se conosciuto)
- **Tono**: utility, no emotional pressure

### Email #3 â€” Giorno +14 Â· "Un ultimo caso reale"
- **Voce**: Caso Reale
- **Subject**: "Un caso che vale 3 minuti â€” anche se Ã¨ l'ultimo"
- **Preview**: "Marta, suo padre Ada, una caduta in bagno. Cos'Ã¨ cambiato il giorno dopo."
- **Body**: 350-400p
- **Struttura**:
  - Storia Caso Reale (preferenzialmente Pillar 5 LTC se segmento sconosciuto, altrimenti pillar del segmento dichiarato del lead)
  - Disclaimer "Caso reale, nomi di fantasia" in calce
  - Chiusura: "Se anche dopo questo non ti scrivi piÃ¹, ci lasciamo qui. Senza rancore."
- **CTA**: link articolo blog completo + preference center secondario
- **Tono**: emotivo asciutto, dignitÃ  del lettore protetta

### (Email #4 â€” Giorno +21 Â· AUTO-UNSUB)
- **Nessuna email inviata**
- **Azione**: spostamento automatico in suppression list permanente (Tag `LCS_07_lost`)
- **Notifica**: opzionale email "Confermiamo la rimozione â€” ci farebbe piacere rivederti se cambi idea" (1 sola, fact-stating, no guilt)
- **Decisione MM**: la notifica finale puÃ² essere attivata o no in `config/brand.json` sez. winback (default OFF â€” exit clean)

---

## 4. Personalizzazione per segmento (Brevo dynamic fields)

Se il lead ha segmento dichiarato (`SEG_*`), personalizzare:
- Email #2: pre-fill preferenze pillar con quelli del segmento (es. SEG_05 Professionisti â†’ P9 Imprese pre-selezionato)
- Email #3: Caso Reale del pillar coerente con il segmento

Default se segmento sconosciuto: Caso Reale Pillar 5 LTC (alta universalitÃ  retail) o Pillar 7 Tutela Legale (alta conseguenzialitÃ ).

---

## 5. Exit conditions del flow

- **ENGAGED**: utente apre â‰¥1 email del flow + click â‰¥1 CTA â†’ tag `LCS_02_engaged` + return a newsletter regolare
- **LOST**: utente completa 21gg senza engagement â†’ tag `LCS_07_lost` + auto-unsub + spostamento suppression list
- **OPT-OUT manuale**: utente clicca unsubscribe in qualsiasi punto â†’ immediato spostamento suppression list
- **CRISIS mode**: blocco temporaneo del flow se kill switch attivo o crisis mode
- **KILL switch**: `AUTOMAZIONE_ATTIVA = false` â†’ flow non si avvia (lifecycle resta DORMANT in attesa)

---

## 6. Compliance baseline (gate-doppio pre-attivazione)

âœ… **Disclaimer RUI integrale** in footer ogni email
âœ… **Disclaimer "Caso reale, nomi di fantasia"** in Email #3
âœ… **Denominazione mandatarie corretta** se citate
âœ… **Unsubscribe link** funzionante e prominente
âœ… **Preference center accessibile** in ogni email (CTA primaria Email #2)
âœ… **Indirizzo mittente fisico** in footer
âœ… **No urgency fittizia** ("ULTIMA CHIAMATA" Â· "STIAMO PER CANCELLARTI" â€” vietati)
âœ… **No guilt-tripping** ("ci hai abbandonato" Â· "ci manchi" pesante â€” evitati)
âœ… **No claim ðŸ”´** vietati (rendimenti garantiti, prezzi, testimonial non autorizzati, dati inventati)
âœ… **Anti-fatigue cap**: stesso utente max 1 win-back/12 mesi (Brevo trigger condizione `last_winback_date IS NULL OR last_winback_date > 12 months ago`)
âœ… **GDPR**: spostamento auto-unsub a LOST rispetta diritto cancellazione

---

## 7. KPI win-back (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Open rate sequenza (cumulato) | â‰¥25% |
| Re-engagement rate (dormant â†’ engaged) | 20-30% |
| Lost rate (auto-unsub finale) | 70-80% |
| Spam complaint rate sequenza | <0.1% |
| Unsubscribe esplicito (durante sequenza) | <15% |

**Pattern atteso**: la maggioranza dei dormant Ã¨ realmente persa (70-80%). Win-back recupera 20-30%, che Ã¨ risultato sano. Lost rate alta = lista pulita = deliverability migliore.

---

## 8. Logica di esecuzione â€” passo-passo

1. **Ricevere brief MM** (setup iniziale o refresh)
2. **Cascata di contesto** (sez. 9)
3. **Per Email #1**: invoca `voce-spiegato-facile` via Task con brief specifico (sez. 3.1)
4. **Per Email #2**: invoca `voce-spiegato-facile` via Task (sez. 3.2)
5. **Per Email #3**: invoca `voce-caso-reale` via Task (sez. 3.3 â€” pillar dipendente dal segmento)
6. **Per ogni email**: aggiungere header (subject + preview) + footer (Compagine + disclaimer RUI integrale + unsubscribe + indirizzo mittente)
7. **Verificare**: subject â‰¤50 char, preview â‰¤90 char, body in range
8. **Invocare** `advisory-plus:compliance-gate-doppio`
9. **Se ðŸŸ¡**: riformulazione, ri-check (max 1 iterazione)
10. **Se ðŸŸ¢**: comporre pacchetto deliverable
11. **Generare brief tecnico Brevo automation** (trigger + 3 step + exit conditions + anti-fatigue cap)
12. **Consegna al MM** per approvazione esplicita CEO pre-attivazione iniziale

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance + GDPR)
2. `/01_Team/08_CRM_Lead_Manager.md` + `/01_Team/02_Copywriter.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` + `config/compagine.json`
4. `Output_approvati/crm/` lead-nurture + segmentation + lifecycle (per coerenza cross-skill)
5. `Output_approvati/06_Email_CRM/` win-back precedenti se esistono
6. Il brief operativo del MM

---

## 10. Cosa NON fare mai

- âŒ **Tono guilt-tripping** ("ci hai abbandonato", "ci manchi" pesante, "abbiamo provato a contattarti" passivo-aggressivo)
- âŒ **Urgency fittizia** ("ULTIMA CHIAMATA", "TI CANCELLEREMO", maiuscolo emotivo)
- âŒ **Subject clickbait** (no "Apri o ti perdi una cosa importante")
- âŒ **PiÃ¹ di 1 win-back/12 mesi** allo stesso utente (anti-fatigue)
- âŒ **Auto-unsub silenzioso** senza comunicazione preventiva (Email #1 informa l'utente)
- âŒ **Push commerciale** (la win-back non vende, riallinea o saluta)
- âŒ **Saltare gate-doppio Compliance** pre-attivazione
- âŒ **Personalizzazione segmento da inferenza** (sempre solo self-declared â€” vedi crm-segmentation)
- âŒ **Frequenza maggiore di 3 email in 21gg** (rischio spam complaint)
- âŒ **Mantenere LOST in lista attiva** (suppression list permanente, GDPR)
- âŒ **Notifica auto-unsub aggressiva** (se attivata, fact-stating, no manipolazione emotiva)

---

*SKILL v1.0 â€” advisory-plus:crm-win-back â€” Sessione 6 Plugin Build â€” 2026-05-21*

