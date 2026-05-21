---
name: crm-lead-nurture
description: Compone e configura la sequenza email automatica di lead nurture post-signup newsletter Advisory+ ("welcome flow"). 5 email scaglionate su 3-4 settimane (giorno 0 Â· giorno 3 Â· giorno 7 Â· giorno 14 Â· giorno 21) che educano sul posizionamento + 4 voci editoriali + 12 pillar + invitano a esplorare un pillar pertinente al segmento target dichiarato dal lead. Ogni email ha subject â‰¤50 char + preview â‰¤90 char, body 250-400p con voce coerente (Spiegato Facile didattico dominante), CTA a basso attrito (no push commerciale), disclaimer RUI integrale in footer, denominazione mandatarie corretta. Implementazione via Brevo automation workflow (shell + API REST v3) â€” Sessione 7 publish + script Brevo. Compliance Officer gate doppio prima dell'attivazione del flow.
---
# ðŸ’Œ Skill crm-lead-nurture â€” Welcome flow newsletter (5 email su 3-4 settimane)

> **Lead nuovi â†’ fidelizzati. 5 email scaglionate. Voce coerente. Compliance gate-doppio pre-attivazione.**

---

## 1. Quando triggera

- Invocata una tantum a setup iniziale plugin per attivare il welcome flow Brevo
- Invocata per refresh annuale (revisione tono, esempi, pillar di apertura)
- Invocata on-demand dal MM se decide di aggiornare un'email specifica della sequenza
- Invocata da `advisory-plus:crm-lifecycle` come componente del lifecycle "Welcome stage"
- Mai auto-trigger continuo: brief MM o setup iniziale

Tempo target di esecuzione: **45-75 minuti** (5 email da comporre + brief tecnico Brevo automation).

---

## 2. Output finale atteso

**Pacchetto Markdown** in `Output_approvati/crm/[YYYY-MM-DD]_lead-nurture_welcome-flow.md` + 5 file email separati `[YYYY-MM-DD]_email-[N]_[slug].md`:

```markdown
---
data: YYYY-MM-DD
flow: welcome-newsletter-advisoryplus
versione: vN
trigger_brevo: contact_added_to_list "Newsletter Advisory+"
durata_totale: 21 giorni (3-4 settimane)
n_email: 5
exit_conditions: [opt-out manuale Â· diventa cliente Â· 3 hard bounce consecutivi]
compliance: ðŸŸ¢
---

## Sintesi (3-5 righe)
[Obiettivo flow Â· cosa fa nel CRM Brevo Â· KPI attesi]

## Calendario sequenza
| # | Giorno | Subject | Preview | Voce | CTA |
|---|---|---|---|---|---|
| 1 | 0 (immediata) | ... | ... | Spiegato Facile | Leggi articolo pillar [N] |
| 2 | +3 | ... | ... | Spiegato Facile | Esplora 4 voci editoriali |
| 3 | +7 | ... | ... | Caso Reale | Vedi un caso reale del pillar attivo |
| 4 | +14 | ... | ... | Analisi | Leggi un'analisi recente |
| 5 | +21 | ... | ... | Spiegato Facile + soft CTA | Vuoi parlare con noi? |

## Brevo automation setup (brief tecnico)
[Trigger Â· condizioni Â· email da utilizzare Â· personalizzazione fields Â· A/B test predisposto se attivo]

## Compliance check
[ðŸŸ¢/ðŸŸ¡/ðŸ”´ + note per ogni email]
```

E 5 file email completi, ognuno con: subject, preview, body 250-400p, CTA, footer (Compagine + disclaimer RUI completo + unsubscribe + indirizzo mittente).

---

## 3. Struttura delle 5 email

### Email #1 â€” Giorno 0 (immediata) Â· Benvenuto
- **Voce**: Spiegato Facile
- **Obiettivo**: presentare Advisory+ (chi siamo, 5 pilastri di differenziazione, perchÃ© ci interessa il tuo bisogno assicurativo)
- **Body**: 250-300p
- **CTA**: link al blog THE ADVISOR, articolo pillar P1 Educazione recente
- **Tono**: caldo, fattuale, no push prodotto

### Email #2 â€” Giorno +3 Â· Le 4 voci editoriali
- **Voce**: Spiegato Facile
- **Obiettivo**: spiegare come comunichiamo (le 4 voci editoriali â€” Spiegato Facile, Badvisor, Caso Reale, Analisi) con 1 esempio breve per voce
- **Body**: 300-350p
- **CTA**: link a articolo Caso Reale recente (preview voce narrativa)
- **Tono**: meta-narrativo, "ecco come parliamo"

### Email #3 â€” Giorno +7 Â· Un caso reale che ti sorprenderÃ 
- **Voce**: Caso Reale
- **Obiettivo**: storytelling concreto su un pillar (preferenzialmente coerente con segmento target del lead se conosciuto, altrimenti default Pillar 5 LTC o Pillar 7 Tutela Legale â€” temi alta-conseguenza)
- **Body**: 350-400p
- **CTA**: link al blog per articolo completo
- **Tono**: narrativo, emotivo asciutto, disclaimer "Caso reale, nomi di fantasia" in calce

### Email #4 â€” Giorno +14 Â· Cosa dicono i numeri
- **Voce**: ðŸ“Š Analisi
- **Obiettivo**: dato di mercato significativo (fonte IVASS/ANIA/COVIP/ISTAT con anno) su un tema rilevante per il segmento target del lead
- **Body**: 300-350p
- **CTA**: link a Articolo Analisi correlato
- **Apparato citazionale**: fonte+anno obbligatori, almeno 1 fonte primaria

### Email #5 â€” Giorno +21 Â· Vuoi parlare con noi?
- **Voce**: Spiegato Facile + soft CTA
- **Obiettivo**: chiusura sequenza, invito a consulenza non vincolante (no push, presenza disponibile)
- **Body**: 250-300p
- **CTA**: form contatti / prenota call Â· esplicito "senza impegno, prima conoscenza gratuita"
- **Tono**: rilassato, "ci siamo, quando vuoi"

---

## 4. Personalizzazione per segmento (Brevo dynamic fields)

Se il lead ha dichiarato segmento (campo opzionale form newsletter), personalizzare:
- Email #3 (Caso Reale) â†’ caso del pillar pertinente al segmento
- Email #4 (Analisi) â†’ dato pertinente al segmento

Mapping di default segmento â†’ pillar dominante:
- Segmento 1 Famiglie giovani genitori â†’ Pillar 4 Famiglia & Vita
- Segmento 2 Adulti con genitori anziani â†’ Pillar 5 AnzianitÃ  & LTC
- Segmento 3 Pre-pensionati â†’ Pillar 6 Risparmio & Investimento
- Segmento 4 Patrimonializzati â†’ Pillar 6 + Pillar 8 Casa & Patrimonio
- Segmento 5 Professionisti P.IVA â†’ Pillar 9 Imprese & Professionisti
- Segmento 6 PMI famigliari â†’ Pillar 9
- Segmento 7 Imprese strutturate â†’ Pillar 9 + Pillar 7 Tutela Legale
- Segmento 8 Terzo Settore â†’ Pillar 12 Specialty
- Segmento 9 Specialty (yacht/arte/religiosi) â†’ Pillar 10/11/12

Se segmento non dichiarato â†’ default Pillar 1 Educazione + Pillar 4/5/7 (alta universalitÃ  retail).

---

## 5. Exit conditions del flow (Brevo)

Il flow viene interrotto se:
- Lead fa **opt-out** manuale (unsubscribe link)
- Lead diventa **cliente** (campo CRM `customer_status = active`)
- Lead riceve **3 hard bounce consecutivi** (lista pulita automaticamente, Brand Book v1.2 sez. 7 cura sanitÃ  lista)
- **Crisis mode globale** attivo (email subject "MODALITÃ€ CRISI" da CEO â†’ blocco temporaneo tutti i flow non utility)
- **Kill switch** `AUTOMAZIONE_ATTIVA = false`

---

## 6. KPI welcome flow (riferimento per data-kpi-channel-baseline)

| KPI | Target mese 1 | A regime |
|---|---|---|
| Open rate medio sequenza | â‰¥30% | â‰¥35% |
| CTR medio sequenza | â‰¥3% | â‰¥5% |
| % lead che completa sequenza | â‰¥75% | â‰¥85% |
| Conversion lead â†’ contatto qualificato (entro 30gg) | 1-3% | 3-7% |
| Unsubscribe rate cumulato sequenza | <2% | <1.5% |

---

## 7. Compliance baseline (gate-doppio pre-attivazione)

âœ… **Disclaimer RUI integrale in footer** di OGNI email (formula Brand Book v1.2 sez. 7):
> *Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo.*

âœ… **Denominazione mandatarie corretta** se citate (Generali Italia â€“ Cattolica Assicurazioni Â· DAS Difesa Legale Â· UCA Tutela Legale e Peritale Â· Europ Assistance).
âœ… **Disclaimer "Caso reale, nomi di fantasia"** in Email #3.
âœ… **Apparato citazionale fonte+anno** in Email #4 (voce Analisi).
âœ… **Unsubscribe link** funzionante e visibile in footer (GDPR + Brevo policy).
âœ… **Indirizzo mittente fisico** in footer (Via Marco Polo 180/C, 55049 Viareggio LU â€” requisito legale anti-spam).
âœ… **Posizionamento nazionale** (no riferimenti territoriali Versilia/Apuana â€” Brand Book v1.2 sez. 2).
âœ… **No claim ðŸ”´ vietati** (no rendimenti garantiti, no prezzi specifici, no testimonial senza consenso, no dati inventati).

âŒ **Mai**:
- Push commerciale aggressivo nelle email #1-#4 (Email #5 ha soft CTA, mai hard sell)
- Loghi mandatarie in body delle email (solo se necessario in disclosure footer, mai come asset visivo)
- A/B test su subject/body senza Compliance gate-doppio (skill `data-ab-test-design` + `compliance-gate-doppio`)

---

## 8. Logica di esecuzione â€” passo-passo

1. **Ricevere brief MM** (setup iniziale o refresh)
2. **Cascata di contesto** (sez. 9)
3. **Per ogni email #1-#5**: invoca via Task tool la voce appropriata con brief specifico:
   ```
   Task(subagent_type: "advisory-plus:voce-[name]",
        prompt: "Brief: email newsletter welcome flow #[N] Â· giorno [N] Â· lunghezza [N]p Â· subject â‰¤50 char Â· preview â‰¤90 char Â· CTA [...] Â· pillar [N] Â· 1 sola variante completa")
   ```
4. **Ricevere** body email
5. **Aggiungere** header email (oggetto Brevo + preview) + footer (Compagine 4 soci ordine alfabetico + disclaimer RUI integrale + unsubscribe + indirizzo mittente)
6. **Verificare**: subject â‰¤50 char, preview â‰¤90 char, body 250-400p
7. **Invocare** `advisory-plus:compliance-gate-doppio` (Compliance Officer + Brand Strategist)
8. **Se ðŸŸ¡**: riformulazione, ri-check (max 1 iterazione)
9. **Se ðŸŸ¢**: comporre pacchetto deliverable (sez. 2)
10. **Generare brief tecnico Brevo automation** (trigger + step + condizioni + exit) per implementazione Sessione 7 publish script
11. **Consegna al MM** per approvazione esplicita CEO pre-attivazione

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 3 segmenti target Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance)
2. `/01_Team/00_Marketing_Manager.md` + `/01_Team/08_CRM_Lead_Manager.md` + `/01_Team/02_Copywriter.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (sez. identitÃ  + disclaimer + mandatarie + pillar map + voci Â· sez. lead_nurture default)
4. `config/compagine.json` (footer 4 soci ordine alfabetico)
5. `Output_approvati/06_Email_CRM/` welcome flow precedenti (se esistono â€” per evoluzione)
6. Il brief operativo del MM

---

## 10. Cosa NON fare mai

- âŒ **Push prodotto aggressivo** nelle prime 4 email (CTA soft, edutainment first)
- âŒ **Saltare gate-doppio Compliance** pre-attivazione flow
- âŒ **Inventare dati** in Email #4 voce Analisi (Brand Book v1.2 sez. 7)
- âŒ **Personalizzazione segmento senza consenso** dichiarato dal lead (GDPR)
- âŒ **Frequenza piÃ¹ alta di 5 email in 3 settimane** (rischio spam complaint)
- âŒ **Subject clickbait** o "promesse" non sostanziate
- âŒ **Lingua diversa da italiano** (mercato IT default; estensione EN solo per richiesta esplicita CEO)
- âŒ **Mancanza unsubscribe link** (GDPR + violazione Brevo TOS)
- âŒ **Riferimenti territoriali** Versilia/Apuana
- âŒ **Pubblicazione senza approvazione CEO** del primo set (refresh iterativi successivi â†’ MM autonomo)

---

*SKILL v1.0 â€” advisory-plus:crm-lead-nurture â€” Sessione 6 Plugin Build â€” 2026-05-21*

