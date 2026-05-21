---
name: content-newsletter
description: Compone la newsletter mensile Advisory+ pronta per invio via Brevo SMTP (libreria shell + API REST v3). Orchestra: voce editoriale (brand voice + Spiegato Facile per highlight + Analisi per news settore) â†’ invoca voce-* via Task tool â†’ riceve testo â†’ applica struttura newsletter (intro 80p + 3 highlight 150p ciascuno + CTA 50p + footer Compagine 80p) â†’ produce template HTML Brevo-ready (placeholder finalizzato da Sessione 7 skill brevo-template) â†’ genera subject line â‰¤50 char + preview text â‰¤90 char ottimizzati per open rate â†’ integra hero banner 600Ã—200 brief visivo â†’ integra disclaimer RUI completo nel footer (newsletter canale che lo consente Brand Book v1.2 sez. 7) â†’ denomina correttamente mandatarie se citate (Generali Italia â€“ Cattolica Assicurazioni, DAS Difesa Legale, UCA Tutela Legale e Peritale, Europ Assistance) â†’ Compliance gate â†’ consegna al MM file Markdown + render HTML pronto per Brevo.
---
# ðŸ’Œ Skill content-newsletter â€” Newsletter mensile Advisory+

> **600-900 parole. 1 al mese. Brevo SMTP. Disclaimer RUI integrato. Subject line e preview cruciali per open rate.**

---

## 1. Quando triggera

- Invocata dal MM 1 volta al mese durante settimana di pubblicazione (frequenza standard: 1/mese)
- Invocata da skill `month-plan` quando pipeline ATL flagga newsletter da preparare 3-7gg prima dell'invio
- Mai auto-trigger

Tempo target di esecuzione: **15-20 minuti**.

---

## 2. Output finale atteso

**File Markdown + render HTML Brevo-ready** consegnato al MM:

```markdown
---
canale: newsletter_brevo
data_invio: YYYY-MM-DD
orario_invio: [es. mar 09:30 â€” picco open rate B2B/retail mix]
mese_riferimento: [Mese YYYY]
pillar_dominante: P[N] [Nome]
firma: brand Advisory+ con footer compagine
subject_line: "[max 50 char]"
preview_text: "[max 90 char]"
hero_banner: brief_visual_hero_[id].md (600Ã—200)
template_brevo: nl_advisoryplus_v1 (popolato in Sessione 7)
lista_destinatari: [es. "main_list" â€” DA POPOLARE in Sessione 6]
disclaimer_rui: INCLUSO_IN_FOOTER
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

# SUBJECT
[Testo subject line â‰¤50 char â€” es. "Maggio in Advisory+: 3 cose da sapere"]

# PREVIEW TEXT
[Testo preview â‰¤90 char â€” es. "LTC, news IVASS, e una storia che vale la pena leggere."]

# CORPO NEWSLETTER

## Hero banner (600Ã—200)
[Brief visual hero Â· stile Â· palette Â· titolo on-image]

## Intro (80 parole)
[SalutÎ¿ Â· contesto mese Â· ponte verso i 3 highlight]

## Highlight 1 (150 parole)
**Titolo highlight**
[Corpo Â· 1 idea chiara Â· CTA implicito (link a articolo blog completo)]

## Highlight 2 (150 parole)
**Titolo highlight**
[Corpo]

## Highlight 3 (150 parole)
**Titolo highlight**
[Corpo]

## CTA (50 parole)
[Invito alla conversazione Â· "Risparmi tempo prenotando una chiamata Â· link prenotazione"]

## Footer Compagine (80 parole)
[4 soci ordine alfabetico + 4 senior advisor â€” referenze contatto Â· denominazione mandatarie corrette se citate Â· disclaimer RUI completo]

---

## DISCLAIMER RUI (in footer)

*Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo.*

*[se cita mandatarie]: Mandati con Generali Italia â€“ Cattolica Assicurazioni, DAS Difesa Legale, UCA Tutela Legale e Peritale, Europ Assistance.*

*Hai ricevuto questa email perchÃ© ti sei iscritto/a a Advisory+ Newsletter. [Link unsubscribe Brevo] Â· [Link preferenze]*
```

---

## 3. Specifiche newsletter Advisory+

### Lunghezza totale
- **600-900 parole** complessive (intro + 3 highlight + CTA + footer)
- Sweet spot per open + click rate B2B/retail mix
- Oltre 1000p = lettore abbandona, scroll fatigue

### Struttura fissa
1. **Hero banner** 600Ã—200 (con titolo on-image evocativo)
2. **Intro 80 parole** (saluto + contesto del mese + ponte ai 3 highlight)
3. **3 Highlight 150 parole ciascuno** (= 450p centrali)
   - Ogni highlight ha un titolo H2 (negrettÎ¿)
   - Ogni highlight presenta 1 idea + CTA implicito (link a articolo blog o pagina sito per approfondire)
4. **CTA 50 parole** (invito alla conversazione, non vendita aggressiva)
5. **Footer Compagine 80 parole** (referenze contatto + denominazione mandatarie + disclaimer RUI)

### Subject line
- **Max 50 caratteri** (oltre Gmail/Outlook tronca)
- Stile coerente con voce brand: chiaro, non sensazionalistico
- Evitare: emoji eccessive (1 max), MAIUSCOLO, "URGENTE!", "GRATIS!"
- Pattern raccomandati:
  - "Mese in Advisory+: [3 cose chiave]"
  - "[Tema mese]: [hook sintetico]"
  - "[Nome socio firma] su [tema]" (per newsletter firmate da socio)
- Skill propone 2 varianti, MM sceglie

### Preview text (pre-header)
- **Max 90 caratteri**
- Estende/specifica il subject (cliente vede subject + preview prima di aprire)
- Pattern: "[Subject sintetico]: dettaglio + curiositÃ "
- Esempio: Subject "Maggio in Advisory+: 3 cose da sapere" + Preview "LTC, news IVASS, e una storia che vale la pena leggere."

### Voci editoriali in newsletter
- **Intro**: brand voice (chiaro, accogliente)
- **Highlight 1** (educazione mese): Spiegato Facile
- **Highlight 2** (news settore o analisi): Analisi compressa (apparato citazionale ridotto ma presente)
- **Highlight 3** (caso o storia del mese): Caso Reale (con disclaimer "Caso reale, nomi di fantasia" inline)
- **CTA**: brand voice
- **Footer**: brand voice corporate

### Hero banner
- **600Ã—200 pixel** (formato newsletter standard, ottimizzato per email client)
- Stile coerente con Design System (Navy 700/800 background + Teal 500 accent)
- Titolo on-image evocativo (max 5-7 parole)
- Brief visual prodotto da skill `adv-image-newsletter-hero` (Sessione 4)

### Disclaimer RUI
- **Sempre nel footer** (newsletter Ã¨ canale che lo consente)
- Formula standard completa (vedi sez. 2 output atteso)
- + denominazione mandatarie corrette se citate
- + frase legale Brevo per unsubscribe + preferenze (richiesto da GDPR)

### Orario di invio raccomandato
- **Mar-Mer-Gio**: 09:00-10:00 (picco open rate B2B/retail)
- **Mar mattina Ã¨ il giorno migliore** per open rate Brevo benchmark Italia
- **Lun + Ven sera + weekend**: evitare

---

## 4. Composizione highlight â€” logica selezione

### Highlight 1 â€” "Educazione del mese"
- Tema centrale: 1 concetto del Pillar 1 Educazione o del pillar dominante mese
- Voce: Spiegato Facile
- CTA: link a articolo blog evergreen sullo stesso tema
- Esempio: "Cos'Ã¨ davvero la franchigia? Te la spiego con il frigorifero rotto."

### Highlight 2 â€” "News del settore" o "Analisi del mese"
- Tema centrale: novitÃ  IVASS/ANIA/COVIP del mese, sentenza rilevante, dato di mercato
- Voce: Analisi compressa
- Apparato citazionale: fonte+anno inline obbligatorio
- CTA: link a articolo blog completo se prodotto
- Esempio: "ANIA 2025: ramo vita -12%. Tre implicazioni per chi pianifica oggi."

### Highlight 3 â€” "Storia del mese" o "Caso Reale"
- Tema centrale: caso fittizio rappresentativo di un pillar attivo
- Voce: Caso Reale
- Disclaimer "Caso reale, nomi di fantasia" inline
- CTA: link a articolo blog Caso Reale completo o pagina pillar
- Esempio: "Marta, 52 anni. Sua madre Ada, 81, Ã¨ caduta in bagno. Ecco cosa Ã¨ successo dopo."

### Pillar di riferimento per gli highlight
- **Pillar dominante del mese** (output `pillars-of-month.json`): protagonista di almeno 1 highlight su 3
- **Pillar 3 News di settore**: sempre presente come highlight 2
- **Pillar 1 Educazione**: sempre presente come highlight 1
- **Specialty se attiva**: opzionalmente come highlight 3 (in alternativa al Caso Reale standard)

---

## 5. Mandatarie nel footer â€” denominazione corretta

Dal Brand Book v1.2 sez. 7:

> Mandati con **Generali Italia â€“ Cattolica Assicurazioni**, **DAS Difesa Legale**, **UCA Tutela Legale e Peritale**, **Europ Assistance**.

- Mai abbreviazioni ("Generali" da solo, "DAS" da solo)
- Mai loghi mandatarie nel corpo della newsletter (solo testo nel footer)
- Mai uso commerciale dei loghi (vietato dalle compagnie stesse)

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (mese riferimento, pillar dominante, eventuali highlight pre-decisi, articoli blog del mese disponibili come CTA, data invio)
2. **Eseguire kickoff**
3. **Leggere** `Output_approvati/` blog del mese per identificare articoli usabili come CTA highlight
4. **Selezionare** 3 highlight (educazione + news/analisi + storia/caso)
5. **Invocare voce editoriale** via Task tool, una per highlight:
   ```
   Task(
     subagent_type: "advisory-plus:voce-spiegato-facile",
     prompt: "Highlight 1 newsletter â€” tema [X] Â· 150 parole Â· CTA link [URL articolo]."
   )
   Task(
     subagent_type: "advisory-plus:voce-analisi",
     prompt: "Highlight 2 newsletter â€” tema [Y] news/analisi Â· 150 parole Â· apparato citazionale fonte+anno Â· CTA link [URL]."
   )
   Task(
     subagent_type: "advisory-plus:voce-caso-reale",
     prompt: "Highlight 3 newsletter â€” tema [Z] storia Â· 150 parole Â· disclaimer inline Â· CTA link [URL]."
   )
   ```
6. **Comporre intro** (brand voice, 80p)
7. **Comporre CTA** (brand voice, 50p, invito conversazione non commerciale)
8. **Comporre footer Compagine** (80p, denominazione mandatarie corrette, disclaimer RUI completo)
9. **Generare subject line** (2 varianti â‰¤50 char) e **preview text** (1 variante â‰¤90 char)
10. **Produrre brief hero banner** (handoff a skill `adv-image-newsletter-hero` Sessione 4)
11. **Renderizzare in HTML Brevo-ready** (placeholder Sessione 7 â€” per ora produzione Markdown strutturato)
12. **Invocare Compliance Officer** via Task tool (attenzione: disclaimer RUI completo, denominazione mandatarie, Caso Reale disclaimer inline, Analisi apparato citazionale, no rendimenti garantiti)
13. **Se ðŸŸ¡/ðŸ”´**: riformulazione, ri-check
14. **Se ðŸŸ¢**: consegna al MM file completo

---

## 7. Casi particolari

### Newsletter del mese di lancio specialty (es. luglio 2026 Pillar 12 Terzo Settore)
- Highlight 3 dedicato a specialty (storytelling Caso Reale ente terzo settore tipico)
- Hero banner con sub-identity specialty (accent ocra Warning â‰¤5%, Brand Book v1.2 sez. 8.1)
- Eventuale richiamo a articolo blog di lancio specialty

### Newsletter ModalitÃ  Ferie (luglio-agosto)
- Versione ridotta: solo intro + 1 highlight + CTA + footer (no 3 highlight)
- Subject: "Advisory+ in pausa fino al [data]. Ci sentiamo a settembre."
- 1 articolo evergreen come highlight unico (no news fresche)

### Newsletter crisi (sinistro mandataria, evento settoriale grave)
- Skip newsletter del mese o ritardo invio (sensibilitÃ  di brand)
- Eventuale email separata di gestione crisi (NON questa skill â€” gestione manuale MM/CEO)

### Newsletter firmata Daniele (occasionale)
- Subject: "Daniele Simonini: [tema]"
- Intro firmata 1Âª persona Daniele
- Footer come standard ma con focus su Daniele referente

---

## 8. Cosa NON fare mai

- âŒ **Subject line >50 char** (troncamento Gmail/Outlook)
- âŒ **Preview text >90 char**
- âŒ **Subject MAIUSCOLO o con eccessive emoji** (spam filter rischio)
- âŒ **Loghi mandatarie nel corpo** (solo testo footer)
- âŒ **Abbreviazioni mandatarie** ("Generali", "DAS" da soli)
- âŒ **Sforare 900p totali** (scroll fatigue)
- âŒ **Saltare disclaimer RUI** o link unsubscribe (GDPR rischio)
- âŒ **Riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Citazione prezzi specifici di prodotto** senza contesto
- âŒ **CTA commerciale aggressivo** ("Acquista ora!", "Offerta scade!")
- âŒ **Caso Reale senza disclaimer inline**
- âŒ **Analisi senza apparato citazionale** o con fonti vietate
- âŒ **Hero banner con foto persone identificabili** senza consenso
- âŒ **Invio fuori finestra mar-mer-gio mattina** senza motivazione strategica

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance â€” disclaimer newsletter Â· sez. 8 Design System Â· sez. 9 Compagine)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/02_Copywriter.md` Â· `/01_Team/08_CRM_Lead_Manager.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (mapping voce-canale, disclaimer standard, denominazione mandatarie)
4. `config/compagine.json` (footer Compagine: ordine alfabetico soci + senior advisor)
5. `config/design-system.json` (hero banner specifiche)
6. `config/pillars-of-month.json`
7. `Output_approvati/` blog del mese (per CTA highlight)
8. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-newsletter â€” Sessione 3 Plugin Build â€” 2026-05-18*

