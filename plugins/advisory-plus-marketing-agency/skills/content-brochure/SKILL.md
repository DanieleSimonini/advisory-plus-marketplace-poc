---
name: content-brochure
description: Compone una brochure corporate Advisory+ in formato A4 2-3 pagine (linea Famiglia, retail) o booklet 8 pagine (linea Imprese o Specialty drops). Orchestra: voce editoriale (brand corporate â€” Spiegato Facile per spiegazione prodotti + Analisi per dati di mercato/benefit verificati, mai Badvisor in brochure, raramente Caso Reale che resta su canali editoriali) â†’ invoca voce-* via Task tool â†’ riceve testo strutturato â†’ applica struttura brochure (cover Â· intro Â· 3-5 sezioni contenuto Â· disclaimer RUI completo Â· footer) â†’ invoca Art Director (skill brand `art-director`) per template full layout â†’ integra denominazione mandatarie corretta (Generali Italia â€“ Cattolica, DAS Difesa Legale, UCA Tutela Legale e Peritale, Europ Assistance) â†’ integra loghi mandatarie ESCLUSIVAMENTE in area disclosure footer (Brand Book v1.2 sez. 7 vincolo IVASS) â†’ Compliance gate raddoppiato (brochure Ã¨ materiale corporate, livello max attenzione) â†’ consegna al MM brief completo per Art Director + testo strutturato.
---
# ðŸ“„ Skill content-brochure â€” Brochure corporate Advisory+

> **Materiale corporate stampabile. A4 retail 2-3 pp Â· Booklet B2B/Specialty 8 pp. Disclaimer RUI integrale obbligatorio. Loghi mandatarie SOLO in disclosure.**

---

## 1. Quando triggera

- Invocata dal MM per produzione brochure stagionale (es. linea Famiglia primavera, linea Imprese inizio anno) o one-shot (lancio specialty, evento territoriale, partnership istituzionale)
- Invocata da skill `campaign-30-60-90` quando una campagna include materiale corporate stampabile
- Pipeline ATL lunga (30gg+) â€” brief 30gg prima della consegna stampati

Tempo target di esecuzione: **30-45 minuti** per testo (l'impaginazione full passa a Art Director).

---

## 2. Output finale atteso

**Brief completo per Art Director + testo strutturato Markdown** consegnato al MM:

```markdown
---
canale: brochure_corporate
formato: [A4_2_pagine | A4_3_pagine | booklet_8_pagine]
linea_prodotto: [Famiglia | Imprese | Specialty_P10_Mare | Specialty_P11_Arte | Specialty_P12_TerzoSettore | Corporate_Generale]
pillar_riferimento: [P_X]
voce: [Spiegato Facile / Analisi / Brand corporate]
firma: brand Advisory+
data_consegna_stampati: YYYY-MM-DD
mandatarie_citate: ["Generali Italia â€“ Cattolica Assicurazioni", "DAS Difesa Legale", "UCA Tutela Legale e Peritale", "Europ Assistance"] # solo se applicabile
loghi_mandatarie: SOLO_IN_DISCLOSURE_FOOTER (vincolo IVASS)
disclaimer_rui: INTEGRALE
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
handoff_art_director: brief_art_director_brochure_[id].md
---

# COVER (pagina 1)
**Titolo brochure:** [es. "La tua famiglia, protetta. Sul serio."]
**Sottotitolo:** [es. "Linea Famiglia: vita, salute, casa, tutela legale."]
**Visual cover:** [stile Â· palette Â· elementi Â· NO foto persone identificabili senza consenso]
**Logo Advisory+:** in cover (logo principale brand, NON loghi mandatarie)
**Tagline:** "Consulenza assicurativa. Sul serio."

# INTRO (pagina 2 â€” o prima sezione pagina 1 se A4 ridotto)
[200-300 parole Â· saluto Â· chi siamo (Studio Solutions S.r.l. + Advisory+ marchio commerciale + RUI A000669271) Â· cosa offriamo (consulenza assicurativa professionale) Â· perchÃ© ora (contesto pillar)]

# SEZIONI CONTENUTO (pagine 3-N)

## Sezione 1 â€” [Titolo prodotto/tema]
[300-500 parole Â· voce Spiegato Facile o Analisi Â· spiegazione tecnica accessibile Â· benefit verificati (no claim assoluti) Â· eventuali bullet point]

## Sezione 2 â€” [Titolo prodotto/tema]
[300-500 parole]

## Sezione 3 â€” [Titolo prodotto/tema] (se A4 3pp o booklet)
[...]

## ... fino a 5 sezioni per booklet 8 pp ...

# FOOTER (ultima pagina)

## Compagine
[4 soci ordine alfabetico (Agostini Â· Barrella Â· Fappani Â· Simonini) â€” referenze contatto Â· 4 senior advisor â€” referenze Â· sede legale Studio Solutions S.r.l. Â· 5 sedi operative (logistica, non narrativa) Â· contatti generali (telefono Â· email Â· sito)]

## Mandatarie (in area disclosure)
**Mandati con:**
- Generali Italia â€“ Cattolica Assicurazioni [logo nativo]
- DAS Difesa Legale [logo nativo]
- UCA Tutela Legale e Peritale [logo nativo]
- Europ Assistance [logo nativo]

## Disclaimer RUI integrale
*Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo. Le informazioni contenute in questo materiale non costituiscono offerta di prodotti assicurativi nÃ© consulenza personalizzata.*

# BRIEF VISUAL PER ART DIRECTOR
[Brief completo per skill `art-director`:
- Formato (A4 verticale 210Ã—297 mm Â· booklet 8pp 148Ã—210 mm cad.)
- Numero pagine
- Palette Design System (Navy 700/800 + Teal 500 + Mist + Ink)
- Font (Inter Tight headline Â· Source Serif 4 citazioni Â· JetBrains Mono dati)
- Tipologia immagini (illustrazioni vs foto stock generiche Â· NO foto persone identificabili)
- Posizione loghi mandatarie (footer area disclosure, mai cover, mai pagine contenuto)
- Logo Advisory+ in cover principale
- Schema impaginazione preferito (single-col vs 2-col Â· margini Â· interlinea)
- Output: file PDF print-ready + InDesign source se applicabile
- Stampa: pipeline tipografica esterna (handoff successivo)]
```

---

## 3. Specifiche brochure Advisory+

### Formati
- **A4 verticale 2 pagine** (retail leggero, da distribuire in sede o eventi): cover + corpo
- **A4 verticale 3 pagine** (retail completo, linea Famiglia): cover + intro + sezione prodotti
- **Booklet 148Ã—210 mm Ã— 8 pagine** (B2B Imprese o Specialty): cover + intro + 4-5 sezioni contenuto + compagine + footer
- **Formati altri** (folding, A5, ecc.): valutare caso per caso con Art Director

### Tipologie tipiche per linea prodotto

| Linea | Formato | Voce primaria | Note |
|---|---|---|---|
| **Linea Famiglia** (Pillar 4-5-7-8) | A4 3pp | Spiegato Facile | Retail, tono caldo accessibile |
| **Linea Imprese & Professionisti** (Pillar 9) | Booklet 8pp | Analisi + Spiegato Facile entry | B2B, registro professional |
| **Specialty Mare** (P10) | Booklet 8pp | Caso Reale + Analisi taglio fiscale | Lifestyle + tecnico |
| **Specialty Arte** (P11) | Booklet 8pp | Analisi + Caso Reale | Tecnico + esempi |
| **Specialty Terzo Settore** (P12) | Booklet 8pp | Analisi | Normativa + presentazione enti tipo |
| **Corporate Generale** (chi siamo) | A4 2-3pp | Brand corporate | Presentazione studio |

### Lunghezza totale per formato
- **A4 2pp**: 500-800 parole testo
- **A4 3pp**: 900-1500 parole testo
- **Booklet 8pp**: 2000-3500 parole testo

### Voci editoriali in brochure
- **Spiegato Facile** primaria per linee retail (Famiglia)
- **Analisi** primaria per linee B2B (Imprese) e specialty con taglio normativo (Arte, Terzo Settore)
- **Brand corporate** per intro e sezioni "chi siamo" (registro accogliente + autorevole)
- **Caso Reale** raro in brochure (Ã¨ voce editoriale, brochure Ã¨ materiale corporate) â€” solo per Specialty Mare con storytelling esemplificativo
- **Badvisor**: VIETATO in brochure (registro non adatto a materiale corporate)

### Loghi mandatarie â€” vincolo IVASS Brand Book v1.2 sez. 7
- **SOLO nell'area disclosure del footer** (mai cover, mai pagine contenuto)
- Loghi nativi ricevuti dalle compagnie mandatarie (assets ufficiali, non versioni elaborate)
- Denominazione corretta sempre:
  - **Generali Italia â€“ Cattolica Assicurazioni** (mai solo "Generali" o solo "Cattolica")
  - **DAS Difesa Legale**
  - **UCA Tutela Legale e Peritale**
  - **Europ Assistance**

### Disclaimer RUI integrale
- **Sempre nell'ultima pagina** (footer disclosure)
- Formula completa estesa per brochure (piÃ¹ ampia di newsletter/blog):
  > *Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo. Le informazioni contenute in questo materiale non costituiscono offerta di prodotti assicurativi nÃ© consulenza personalizzata.*

### Tagline brand
- **"Consulenza assicurativa. Sul serio."** (Brand Book v1.2 sez. 5)
- Posizione: cover o footer (Art Director decide)

### Sedi
- **5 sedi operative** (Viareggio sede legale + Massa, Carrara, Pietrasanta, Camaiore) â€” Brand Book v1.2 sez. 2 li tratta come logistica operativa, NON come narrativa territoriale
- **Posizionamento NAZIONALE** mantenuto: la brochure parla a chiunque, le sedi sono "dove ci si puÃ² incontrare", non "siamo del territorio"
- Sezione "Dove siamo" in footer: lista indirizzi sede legale + 4 sedi operative, senza enfasi territoriale

---

## 4. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (formato, linea prodotto, pillar, mandatarie da citare, data consegna stampati, eventuale evento di destinazione)
2. **Eseguire kickoff**
3. **Identificare voce primaria** in base a linea (default mapping sez. 3)
4. **Invocare voce editoriale** via Task tool con brief brochure:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: brochure [linea] Â· formato [A4_Xpp/booklet_8pp] Â· pillar [N] Â· lunghezza [X] parole totali Â· 3-5 sezioni contenuto Â· registro brand corporate Â· 1 sola variante completa."
   )
   ```
5. **Ricevere** testo strutturato
6. **Comporre intro brand corporate** (200-300p) con presentazione Studio Solutions + Advisory+ + RUI
7. **Comporre footer Compagine** (4 soci ordine alfabetico + 4 senior advisor + sede legale + 5 sedi operative + contatti)
8. **Verifica denominazione mandatarie** corretta (grep "Generali" da solo, "DAS" da solo, "UCA" da solo, "Europ" da solo â†’ correggere se trovato)
9. **Comporre disclaimer RUI integrale** in footer
10. **Comporre brief Art Director** con tutti i metadati visivi (formato, palette, font, tipologia immagini, posizione loghi)
11. **Invocare skill `art-director`** via Task tool per validazione brief visivo e ipotesi di layout:
    ```
    Task(
      subagent_type: "advisory-plus:art-director",
      prompt: "Validazione brief brochure [linea] [formato] Â· ipotesi layout Â· stima fattibilitÃ  in pipeline ATL [N]gg."
    )
    ```
12. **Invocare Compliance Officer** via Task tool per gate RADDOPPIATO (brochure Ã¨ livello max attenzione):
    - Verifica denominazione mandatarie corretta
    - Verifica disclaimer RUI integrale presente
    - Verifica loghi mandatarie SOLO in disclosure
    - Verifica no claim assoluti, no rendimenti garantiti, no prezzi specifici
    - Verifica posizionamento nazionale (no enfasi territoriale)
    - Verifica eventuale apparato citazionale Analisi (se voce Analisi presente)
13. **Se ðŸŸ¡/ðŸ”´**: riformulazione, ri-check
14. **Se ðŸŸ¢**: consegna al MM brief completo per Art Director + testo finale Markdown

---

## 5. Casi particolari

### Brochure di evento (open day sede, fiera)
- A4 2pp leggero
- Cover con titolo evento + data + luogo
- Sezione contenuto: descrizione evento + relatori + agenda
- Footer come standard

### Brochure di partnership (co-marketing con ente/ordine/associazione)
- Logo Advisory+ + logo partner in cover (eccezione al "solo logo Advisory+ in cover", ma SOLO se partnership ufficiale formalizzata)
- Loghi mandatarie restano SOLO in disclosure (regola IVASS invariata)
- Sezione "Partnership con [Partner]" in posizione di rilievo
- Disclaimer RUI integrale + eventuale disclaimer partner (concordato)
- Compliance gate triplicato (brochure + partnership = max attenzione)

### Brochure lancio specialty drop (es. P12 Terzo Settore luglio 2026)
- Booklet 8pp
- Cover con sub-identity specialty (accent ocra Warning â‰¤5%, Brand Book v1.2 sez. 8.1)
- Sezione 1 "Cos'Ã¨ il terzo settore" (Spiegato Facile divulgativo)
- Sezione 2-4 "Coperture per ETS/CTS/enti religiosi" (Analisi con normativa)
- Sezione 5 "Caso esemplificativo" (Caso Reale fittizio)
- Footer mandatarie pertinenti (probabilmente Generali Italia â€“ Cattolica per ramo enti)

### Brochure aggiornata vs prima edizione
- Versionamento esplicito (es. "v1.0 mag 2026" in footer)
- Diff version precedente in Verbale chat (cosa Ã¨ cambiato e perchÃ©)
- Compliance gate riapplicato (modifiche possono introdurre claim non aggiornati)

---

## 6. Cosa NON fare mai

- âŒ **Loghi mandatarie in cover o pagine contenuto** (solo in disclosure footer â€” vincolo IVASS hard)
- âŒ **Abbreviazioni mandatarie** ("Generali" da solo, "DAS" da solo, ecc.)
- âŒ **Saltare disclaimer RUI integrale** (brochure Ã¨ canale obbligatorio)
- âŒ **Posizionamento territoriale** (Versilia/Apuana/Toscana â€” anche se le sedi sono lÃ¬, brand Ã¨ nazionale)
- âŒ **Foto persone identificabili** senza consenso scritto (compliance privacy)
- âŒ **Badvisor in brochure** (registro non adatto)
- âŒ **Caso Reale in brochure standard** (raro, solo per Specialty Mare)
- âŒ **Claim assoluti** ("la migliore", "leader", "unica") â€” Compliance bloccherÃ 
- âŒ **Promesse rendimenti garantiti** o promesse di esito
- âŒ **Citazione prezzi specifici di prodotto** senza contesto
- âŒ **Confronti denigratori** con concorrenti
- âŒ **Tagline diversa** da "Consulenza assicurativa. Sul serio." senza decisione esplicita CEO
- âŒ **Brochure firmata da singolo socio** (Ã¨ materiale corporate brand, firma collettiva Compagine in footer)

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento nazionale Â· sez. 4 voci Â· sez. 5 tagline Â· sez. 7 Compliance vincoli brochure e mandatarie Â· sez. 8 Design System Â· sez. 9 Compagine)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/02_Copywriter.md` Â· `/01_Team/05_Art_Director.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (denominazione mandatarie, tagline, disclaimer standard)
4. `config/design-system.json` (formati brochure, palette, font, loghi)
5. `config/compagine.json` (footer Compagine: ordine alfabetico, sedi)
6. Brochure precedenti in `Output_approvati/` (coerenza cross-edizione)
7. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-brochure â€” Sessione 3 Plugin Build â€” 2026-05-18*

