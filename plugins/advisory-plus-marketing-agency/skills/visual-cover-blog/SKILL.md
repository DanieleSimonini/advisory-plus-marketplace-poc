---
name: visual-cover-blog
description: Generator del Cover Blog System Advisory+ (Brand Book v1.2 sez. 8.1) â€” cover 1200Ã—630 per articoli blog THE ADVISOR con categoria editoriale visibile nel design. Consolida la categoria ðŸ“Š Analisi (NUOVA in v1.2, pendenza Art Director ora chiusa in Sessione 4) insieme alle 4 categorie esistenti (Educazione ðŸ§ , Caso Reale ðŸ“–, Voce CEO âœï¸, News di settore ðŸ“°). Composiziona prompt per cc-nano-banana o brief manuale per Canva (handoff alternativo) integrando: titolo articolo + categoria + voce editoriale + palette Design System + sub-identity Specialty se attiva (accent ocra Warning â‰¤5% per Specialty drops Mare/Arte/Terzo Settore). Triggera da skill content-blog-article automatica. Output: file PNG 1200Ã—630 + metadata. Invoca compliance-ai-disclosure solo se output foto-realistico (raro per cover blog â€” default illustrazione).
---
# ðŸ“° Skill visual-cover-blog â€” Generator Cover Blog System Advisory+

> **5 categorie consolidate (Educazione Â· Caso Reale Â· Analisi nuova v1.2 Â· Voce CEO Â· News). 1200Ã—630. Sub-identity Specialty con accent ocra â‰¤5%. Brand Book v1.2 sez. 8.1.**

---

## 1. Quando triggera

- Invocata automaticamente da skill content-blog-article quando il MM produce un nuovo articolo blog
- Invocata manualmente via `/adv-cover-blog [titolo] [categoria]` per generare cover on-demand
- Invocata per rigenerazione cover di articoli esistenti (es. dopo refresh Design System)

Tempo target di esecuzione: **3-5 minuti** (composizione + generazione cc-nano-banana).

---

## 2. Output finale atteso

**File PNG 1200Ã—630** + metadata consegnati al chiamante (content-blog-article):

```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/cover_blog_[id].png
formato: 1200Ã—630 landscape
motore: cc-nano-banana (Gemini 2.5 Flash Image)
categoria_editoriale: [Educazione ðŸ§  | Caso Reale ðŸ“– | Analisi ðŸ“Š | Voce CEO âœï¸ | News ðŸ“°]
voce: [Spiegato Facile / Caso Reale / Analisi / ecc.]
sub_identity_specialty: [P10 Mare | P11 Arte | P12 Terzo Settore | nessuna]
titolo_on_cover: [max 6-8 parole Â· contrast forte]
palette_dominante: [navy_700 + teal_500 | sub_identity_specialty]
ai_disclosure_richiesta: NO (illustrazione/concept, no foto-realistico)
---
```

---

## 3. Cover Blog System â€” le 5 categorie (consolidate in Sessione 4)

### Categoria 1 â€” ðŸ§  Educazione (voce Spiegato Facile primaria)
- **Visual style**: vector flat illustration didattica, oggetti quotidiani, mood caldo
- **Palette dominante**: Navy 700/800 background + Teal 500 accent + Mist surface
- **Tipografia titolo**: Inter Tight bold, dimensione grande (60-72pt), bianco su navy
- **Iconografia**: oggetti quotidiani (frigorifero, casa, ombrello, libro, ecc.) stilizzati
- **Categoria label**: "ðŸ§  Educazione" in corner alto sinistra, Inter Tight regular, accent Teal

### Categoria 2 â€” ðŸ“– Caso Reale (voce Caso Reale primaria)
- **Visual style**: editorial illustration narrativa, mood empatico sobrio
- **Palette dominante**: Navy 700/800 + Teal 500 accent + Mist
- **Tipografia titolo**: Inter Tight bold, accompagnata da Source Serif 4 per eventuale sottotitolo narrativo
- **Iconografia**: scene di vita stilizzate (no foto persone identificabili â€” illustrazione editoriale)
- **Categoria label**: "ðŸ“– Caso Reale" in corner alto sinistra
- **Nota footer**: "Caso reale, nomi di fantasia" in piede della cover (sottile)

### Categoria 3 â€” ðŸ“Š Analisi â­ NUOVA v1.2 (consolidata in Sessione 4)
- **Visual style**: data visualization, schematic, infographic clean
- **Palette dominante**: Navy 700/800 + Teal 500 accent + JetBrains Mono per dati on-cover
- **Tipografia titolo**: Inter Tight bold + JetBrains Mono per eventuali percentuali/dati visualizzati
- **Iconografia**: grafici stilizzati (curve, barre, percentuali), schemi normativi minimal, timeline
- **Categoria label**: "ðŸ“Š Analisi" in corner alto sinistra
- **Nota footer**: eventuale fonte primaria sintetica (es. "Fonte: IVASS 2024")

### Categoria 4 â€” âœï¸ Voce CEO (post autoriali firmati Daniele)
- **Visual style**: editorial, sobrio, firmato in modo evidente
- **Palette dominante**: Navy 700/800 + Teal 500 + Mist
- **Tipografia titolo**: Inter Tight bold + nome firmatario in Source Serif 4 italic
- **Iconografia**: minimale (icona penna, âš–ï¸, o nessuna)
- **Categoria label**: "âœï¸ Voce CEO" in corner alto sinistra
- **Footer firma**: "di Daniele Simonini, Agent, Admin & Advisor" in corner basso destro

### Categoria 5 â€” ðŸ“° News di settore (voce Analisi per news/normativa)
- **Visual style**: editorial news, contemporaneo, urgenza implicita
- **Palette dominante**: Navy 700/800 + Teal 500 + Mist
- **Tipografia titolo**: Inter Tight bold, dimensione molto grande (impact)
- **Iconografia**: minimal (icona settore, simbolo IVASS/Cass./ANIA se rilevante)
- **Categoria label**: "ðŸ“° News" in corner alto sinistra
- **Date stamp**: data evento (es. "Cass. 15/03/2024") in corner basso

---

## 4. Sub-identity Specialty (accent ocra Warning â‰¤5%)

Brand Book v1.2 sez. 8.1: i contenuti delle Specialty drops (P10 Mare & Yacht Â· P11 Arte & Patrimonio Â· P12 Terzo Settore) hanno una sub-identity visiva che si aggiunge alla categoria editoriale:

- **Accent ocra Warning** (#D97706 o equivalente) in piccola percentuale (â‰¤5% area visuale)
- Esempi: filetto inferiore della cover, badge "Specialty: [P10 Mare]" in corner alto destra, icona-marker specialty
- Mantenimento palette dominante Navy/Teal/Mist invariata
- L'ocra Ã¨ **accent secondario**, non sostituisce Teal

| Specialty | Accent zona | Icona/Badge |
|---|---|---|
| P10 Mare & Yacht | filetto inferiore + badge "ðŸ›¥ Mare" | onda stilizzata o ancora minimal |
| P11 Arte & Patrimonio | filetto laterale + badge "ðŸŽ¨ Arte" | cornice minimal o pennello |
| P12 Enti religiosi & Terzo Settore | filetto laterale + badge "ðŸ¤ Terzo Settore" | mani che si stringono stilizzate (no foto) |

---

## 5. Composizione titolo on-cover

- **Max 6-8 parole** (oltre la cover diventa illeggibile)
- **Inter Tight bold** dimensione 60-72pt
- **Contrast forte**: testo bianco su navy 700/800 OPPURE testo navy su mist (raro)
- **Allineamento**: centro-sinistra preferito (segue convenzione lettura occidentale)
- **Padding**: margini larghi (almeno 80px da bordi)
- **Sottotitolo opzionale**: Source Serif 4 regular 28-36pt, max 8-12 parole, posizione sotto titolo principale

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal chiamante (titolo articolo, categoria editoriale, voce, eventuale specialty attiva, pillar)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/design-system.json` per palette + font + Cover Blog System specifiche
4. **Lookup categoria** (sez. 3) per stile/iconografia/label
5. **Lookup sub-identity specialty** (sez. 4) se applicabile
6. **Comporre titolo on-cover** (max 6-8 parole, eventuale sottotitolo Source Serif)
7. **Composizione prompt cc-nano-banana** integrando: categoria style + palette + iconografia + sub-identity (se attiva) + titolo on-cover come testo
8. **Invocare `advisory-plus:visual-image-static-nano-banana`** via Task tool:
   ```
   Task(
     subagent_type: "advisory-plus:visual-image-static-nano-banana",
     prompt: "Cover blog 1200Ã—630 per categoria [X] Â· voce [Y] Â· titolo on-cover '[Z]' Â· sub-identity specialty [Q se attiva] Â· palette + iconografia + label + footer come da Cover Blog System sez. 3-4."
   )
   ```
9. **Ricevere file PNG** generato + metadata
10. **Salvare** in `Output_approvati/[file]_assets/cover_blog_[id].png` (convenzione `_assets/`)
11. **Restituire metadata + path file PNG** al chiamante (content-blog-article)

---

## 7. Casi particolari

### Articolo cross-categoria (es. Caso Reale + Analisi mista)
- Default: usa categoria primaria del frontmatter contenuto
- Se MM specifica esplicitamente "cover mista", composizione visiva ibrida (es. illustrazione narrativa + filetto grafico data viz)

### Specialty in lancio (es. P12 Terzo Settore luglio 2026)
- Prima cover di lancio: composizione speciale che esplicita il nuovo pillar (badge piÃ¹ visibile, eventuale filetto colore ocra leggermente piÃ¹ spesso del 5% ma â‰¤7% per primo mese)
- A regime: torna a accent ocra â‰¤5% standard

### Cover per articolo Voce CEO firmato Daniele
- Categoria 4 âœï¸ Voce CEO
- Footer firma in corner basso destro (Inter Tight regular 18pt)
- Visual style sobrio editoriale

### Cover che richiede grafico/dato specifico (Analisi)
- Skill compone prompt con descrizione esatta del grafico richiesto
- Es. "data visualization: line chart showing decrease from 100% to 88% over years 2020-2024, JetBrains Mono labels"
- Cover diventa "infografica leggera" coerente con voce Analisi

### Re-render cover esistente dopo refresh Design System
- Skill puÃ² rigenerare cover di articoli precedenti applicando nuovo Design System (palette/font aggiornati)
- ModalitÃ  batch: invocazione su lista articoli â†’ rigenerazione cover N
- Logging in `Log_visual_generati/[YYYY-MM]_cover_blog_refresh.md`

---

## 8. Cosa NON fare mai

- âŒ **Foto-realistic faces** su cover blog (default illustrazione)
- âŒ **Loghi mandatarie** in cover (vincolo IVASS)
- âŒ **Titolo on-cover >8 parole** (illeggibile)
- âŒ **Categoria editoriale non in mappa** (sez. 3 â€” sono 5 esatte)
- âŒ **Accent ocra Specialty >5% area visuale** (regola Brand Book v1.2 sez. 8.1)
- âŒ **Palette diverse da Design System** (no creative override)
- âŒ **Font diversi da Inter Tight / Source Serif 4 / JetBrains Mono**
- âŒ **Saltare label categoria editoriale** (Ã¨ elemento distintivo Cover Blog System)
- âŒ **ClichÃ© stock-photo insurance** (ombrelli, strette di mano, ecc.)
- âŒ **Saltare footer Caso Reale** "Caso reale, nomi di fantasia" su cover Caso Reale

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 8 Design System Â· sez. 8.1 Cover Blog System con consolidamento categoria ðŸ“Š Analisi v1.2)
2. `/01_Team/05_Art_Director.md` Â· `/01_Team/02_Copywriter.md`
3. `config/design-system.json` (palette, font, Cover Blog System)
4. `config/brand.json` (categorie editoriali blog, specialty attive)
5. Il brief contenuto del chiamante

---

*SKILL v1.0 â€” advisory-plus:visual-cover-blog â€” Sessione 4 Plugin Build â€” 2026-05-19 â€” CATEGORIA ðŸ“Š ANALISI CONSOLIDATA*

