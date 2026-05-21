---
name: visual-stories
description: Generator visual Advisory+ per Stories Instagram e Facebook (formato 1080Ã—1920 verticale) + decisione finale set highlight permanenti Instagram (riapertura punto esitazione #1 Sessione 3 in collaborazione Art Director). Composiziona visual coordinati per set di 3-5 slide Stories consecutive (skill content-stories-set produce testo, questa skill produce visual): hook visivo + slide contenuto centrale + CTA visivo. Integra Design System v1.0 (palette Navy 700/800 + Teal 500 accent + Mist surface + Ink contrast) + tipografia Inter Tight grande per testo on-image + sticker IG nativi (poll/question/countdown/link) come placeholder visivi nel brief. Decisione highlight permanenti Instagram (Art Director consolida in questa skill): set 5 highlight (Chi siamo Â· FAQ Educazione Â· Casi Reali Â· Pillar di stagione Â· Eventi) con cover dedicate 1080Ã—1920. Output: file PNG 1080Ã—1920 per slide + cover highlight quando applicabile. Mai foto persone identificabili senza consenso. Mai loghi mandatarie.
---
# ðŸ“± Skill visual-stories â€” Generator visual Stories + decisione highlight permanenti

> **1080Ã—1920 Ã— N slide. Sticker IG nativi placeholder. Highlight permanenti 5 set consolidati con Art Director.**

---

## 1. Quando triggera

- Invocata automaticamente da skill content-stories-set durante composizione del set Stories
- Invocata manualmente via `/adv-stories-visual [tema] [N_slide]` per generare visual on-demand
- Invocata via `/adv-highlight-cover [highlight_name]` per generare cover di un highlight permanente (uso occasionale, una tantum per ogni highlight nuovo o refresh)

Tempo target di esecuzione: **5-10 minuti per set di 3-5 slide** (multiple invocazioni cc-nano-banana).

---

## 2. Output finale atteso

**File PNG 1080Ã—1920 multipli** + metadata consegnati al chiamante (content-stories-set):

```markdown
---
visual_id: [id univoco]
formato: 1080Ã—1920 verticale (Stories)
motore: cc-nano-banana (Gemini 2.5 Flash Image)
set_slides: [N slide]
visual_paths:
  - Output_approvati/[file]_assets/stories_slide_1_[id].png
  - Output_approvati/[file]_assets/stories_slide_2_[id].png
  - Output_approvati/[file]_assets/stories_slide_3_[id].png
  - ... fino a N slide
sticker_placeholder:
  slide_1: [poll/question/countdown/link/nessuno]
  slide_N: [link/CTA/nessuno]
highlight_destination: [nome highlight se add-to-highlight | nessuno]
ai_disclosure_richiesta: NO (illustrazione/concept)
---
```

---

## 3. Specifiche Stories Advisory+

### Formato
- **1080Ã—1920 pixel verticale**
- File PNG (mai JPG)

### Composizione tipo per slide
| Slide | Funzione | Visual |
|---|---|---|
| Slide 1 (hook) | Apertura attenzione | Visual forte centrato + testo grande (5-7 parole) + placeholder sticker poll/question |
| Slide 2-3 (contenuto) | Sviluppo concetto | Visual coerente + testo grande (5-10 parole) + eventuale icona/elemento |
| Slide 4 (contenuto) | Sviluppo (opzionale per set di 5) | Visual coerente + testo |
| Slide finale (CTA) | Chiusura azione | Logo Advisory+ + tagline "Consulenza assicurativa. Sul serio." + testo CTA + placeholder sticker link |

### Palette e tipografia
- **Palette dominante**: Navy 700/800 background, Teal 500 accent, Mist surface se testo scuro su sfondo chiaro
- **Tipografia**: Inter Tight bold grande (100-140pt per stories â€” mobile readability)
- **Testo on-image**: max 5-10 parole per slide (rispetta vincolo content-stories-set)
- **Contrast forte**: bianco su navy OR navy su mist

### Sticker IG nativi â€” placeholder visivi
Il visual generato include **placeholder grafici** dove andranno posizionati i sticker IG nativi durante l'upload manuale dal MM/Daniele (gli sticker veri sono interattivi, vanno aggiunti in app):

- **Poll**: rettangolo placeholder in posizione bassa centrale con scritta "POLL SÃŒ/NO"
- **Question**: rettangolo placeholder con scritta "QUESTION BOX"
- **Countdown**: rettangolo placeholder con scritta "COUNTDOWN TIMER"
- **Link sticker**: rettangolo placeholder con scritta "LINK STICKER" (corner basso) â€” se feature attiva sull'account; altrimenti omettere e scrivere "Link in bio" sul visual

### Esclusioni
- **Mai foto persone identificabili** senza consenso (compliance privacy)
- **Mai loghi mandatarie** (vincolo IVASS â€” Stories non hanno disclosure formale)
- **Mai clichÃ© stock-photo** insurance
- **Mai riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- **Mai musica coperta da copyright** se Stories include audio (caso raro â€” gestito separatamente da MM)

---

## 4. Highlight permanenti Instagram â€” set consolidato (Art Director, Sessione 4)

**Decisione consolidata in Sessione 4 con input Art Director** (riapertura punto esitazione #1 Sessione 3):

Set **5 highlight permanenti** Instagram Advisory+:

### Highlight 1 â€” ðŸ› Chi siamo
- **Cover**: visual brand "Advisory+" + sigla compagine
- **Contenuto**: presentazione Studio Solutions S.r.l. + 4 soci ordine alfabetico + 5 sedi + RUI (NB: contenuto non promozionale, evergreen)
- **Frequenza aggiornamento**: trimestrale (refresh se compagine cambia)

### Highlight 2 â€” ðŸ’¡ FAQ Educazione
- **Cover**: visual didattico + "FAQ" testo grande
- **Contenuto**: domande frequenti assicurazione (franchigia, scoperto, massimale, ecc.) â€” Stories ricorrenti voce Spiegato Facile
- **Frequenza aggiornamento**: mensile (aggiungi 1-2 FAQ/mese)

### Highlight 3 â€” ðŸ“– Casi Reali
- **Cover**: visual editoriale narrativo + "Casi Reali" testo
- **Contenuto**: best of Caso Reale dell'anno (snippet 3-5 slide ciascuno)
- **Disclaimer**: tutti i Casi Reali devono avere "Caso reale, nomi di fantasia" inline
- **Frequenza aggiornamento**: trimestrale

### Highlight 4 â€” ðŸŽ¯ Pillar di stagione
- **Cover**: visual con accent del pillar attivo + nome pillar
- **Contenuto**: educational del pillar dominante del mese/trimestre (es. P5 LTC giugno-luglio, P6 Risparmio ottobre-dicembre)
- **Frequenza aggiornamento**: mensile (cambia col pillar-of-month)

### Highlight 5 â€” ðŸ“… Eventi
- **Cover**: visual editoriale neutro + "Eventi" testo
- **Contenuto**: recap eventi Advisory+ passati e calendar prossimi (open day, webinar, fiere)
- **Frequenza aggiornamento**: post-evento o pre-evento

### Cover degli highlight â€” design
- Formato **1080Ã—1920** (visualizzato come cerchio 110Ã—110 in pratica)
- Centro dell'immagine deve essere riconoscibile nel cerchio (i bordi vengono croppati)
- Palette Design System
- Icona/elemento centrale + nome highlight micro sotto (testo molto piccolo, leggibile zoom)

### Pendenza chiusa
Questa decisione **chiude il punto esitazione #1 di Sessione 3**. Set 5 highlight ratificato. Variazioni future richiedono decisione esplicita Art Director + Brand Strategist + CEO.

---

## 5. Logica di esecuzione â€” passo-passo

### Per Stories set (chiamato da content-stories-set)
1. **Ricevere brief** dal chiamante (testo per ciascuna slide, sticker tipo per slide 1 e slide finale, numero slide, eventuale highlight destination)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/design-system.json` per palette + font + Stories specifiche
4. **Per ciascuna slide**, comporre prompt cc-nano-banana:
   - Slide hook: visual forte + testo grande + placeholder sticker
   - Slide contenuto: visual coerente + testo
   - Slide CTA: logo + tagline + placeholder sticker link
5. **Invocare `advisory-plus:visual-image-static-nano-banana`** N volte (una per slide) via Task tool
6. **Ricevere file PNG** per ciascuna slide
7. **Salvare tutti i file** in `Output_approvati/[file]_assets/stories_slide_[N]_[id].png` (convenzione `_assets/`)
8. **Restituire metadata + lista path** al chiamante

### Per Highlight cover (chiamato manualmente via /adv-highlight-cover)
1. **Ricevere brief** dal MM (nome highlight tra i 5 consolidati: Chi siamo / FAQ Educazione / Casi Reali / Pillar di stagione / Eventi)
2. **Eseguire kickoff**
3. **Lookup specifiche** highlight (sez. 4) per icona/elemento centrale
4. **Comporre prompt cc-nano-banana** per cover 1080Ã—1920 con elemento centrale riconoscibile nel cerchio (bordi safe)
5. **Invocare visual-image-static-nano-banana**
6. **Salvare** in `Output_approvati/highlight_covers/[nome_highlight]_cover_[id].png`
7. **Restituire** path al MM

---

## 6. Casi particolari

### Set Stories per pillar specialty (P10/P11/P12 attiva)
- Visual con accent ocra Warning â‰¤5% (sub-identity specialty Brand Book v1.2 sez. 8.1)
- Badge specialty in corner alto destra di slide 1
- Allineato a Cover Blog System sub-identity

### Set Stories di countdown evento (CTA con countdown sticker IG)
- Slide 1: hook evento (visual + titolo + data)
- Slide 2: dettagli (luogo + relatori se applicabile)
- Slide 3: countdown sticker placeholder
- Slide 4 (finale): CTA "Iscriviti" + link sticker
- Cover highlight "Eventi" puÃ² raccoglierlo permanentemente post-evento

### Set Stories Q&A (sticker question raccolta domande)
- Slide 1: visual + "La tua domanda assicurativa?" + question sticker placeholder
- Slide 2: chiusura con CTA "Riceverai risposta nelle prossime Stories"
- Set semplificato (2 slide bastano)
- Risposte raccolte â†’ poi materiale per FAQ Educazione highlight (alimenta highlight 2)

### Re-render cover highlight dopo refresh Design System
- Skill puÃ² rigenerare cover degli highlight applicando palette/font aggiornati
- Trigger manuale via `/adv-highlight-cover [nome] --refresh`

### Set Stories per cross-post Facebook
- Stessi PNG (formato 1080Ã—1920 compatibile Facebook Stories)
- MM gestisce cross-post manuale durante upload Meta Business Suite

---

## 7. Cosa NON fare mai

- âŒ **Foto persone identificabili** senza consenso scritto
- âŒ **Loghi mandatarie** in visual Stories (Stories non hanno disclosure formale)
- âŒ **Testo on-image >10 parole** per slide (illeggibile)
- âŒ **Palette diverse da Design System**
- âŒ **ClichÃ© stock-photo insurance**
- âŒ **Riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- âŒ **Sticker placeholder confondibili con vero sticker** (chiarezza: deve essere ovvio che Ã¨ placeholder per upload manuale)
- âŒ **Variare highlight set consolidato** senza decisione Art Director + Brand Strategist + CEO (sez. 4 â€” 5 highlight ratificati)
- âŒ **JPG invece di PNG** (degrada testo)
- âŒ **Cover highlight con elemento decentrato** (cerchio crop, centro deve essere riconoscibile)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 8 Design System Â· sez. 8.1 sub-identity Specialty)
2. `/01_Team/05_Art_Director.md` Â· `/01_Team/03_Social_Media_Manager.md`
3. `config/design-system.json` (palette, font, Stories specifiche)
4. `config/brand.json` (specialty attive)
5. Il brief contenuto del chiamante (content-stories-set o MM per highlight cover)

---

*SKILL v1.0 â€” advisory-plus:visual-stories â€” Sessione 4 Plugin Build â€” 2026-05-19 â€” HIGHLIGHT PERMANENTI IG SET 5 CONSOLIDATO (punto esitazione #1 S3 chiuso)*

