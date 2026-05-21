---
name: visual-thumbnail-youtube
description: Generator thumbnail YouTube Advisory+ 1280Ã—720 (formato standard YouTube) per video del nuovo canale (Brand Book v1.2 sez. 14). Composiziona thumbnail brand-coerenti integrando Design System v1.0 (palette Navy 700 + Teal 500 + tipografia Inter Tight bold) + categoria contenuto (Educazione/Caso Reale/Analisi/Voce CEO/News allineate a Cover Blog System) + titolo on-thumbnail max 6-8 parole con contrast forte + logo Advisory+ in corner + eventuale visual element (avatar generico HeyGen se video usa avatar, illustrazione concept altrimenti). Mai foto Daniele o altri soci sul thumbnail (anche se video usa avatar AI, per evitare confusione "avatar AI vs persona reale"). Triggera da content-youtube-video. Output: file PNG 1280Ã—720 + metadata. Invoca compliance-ai-disclosure solo se thumbnail include avatar HeyGen visibile (caso raro â€” default illustrazione concept). Mai loghi mandatarie. Mai clichÃ© YouTube (frecce rosse giganti, emoji shock, MAIUSCOLO).
---
# ðŸ“º Skill visual-thumbnail-youtube â€” Generator thumbnail YouTube Advisory+

> **1280Ã—720. Brand-coerente con Cover Blog System. Mai foto Daniele/soci. Mai clichÃ© clickbait. Brand Book v1.2 sez. 14.**

---

## 1. Quando triggera

- Invocata automaticamente da skill content-youtube-video durante composizione del pacchetto video
- Invocata manualmente via `/adv-thumbnail-youtube [titolo] [categoria]` per generare thumbnail on-demand
- Invocata per A/B testing thumbnail (raro: genera 2-3 varianti per stesso video)

Tempo target di esecuzione: **3-5 minuti**.

---

## 2. Output finale atteso

**File PNG 1280Ã—720** + metadata consegnati al chiamante (content-youtube-video):

```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/thumbnail_youtube_[id].png
formato: 1280Ã—720 landscape
motore: cc-nano-banana (Gemini 2.5 Flash Image)
categoria_contenuto: [Educazione ðŸ§  | Caso Reale ðŸ“– | Analisi ðŸ“Š | Voce CEO âœï¸ | News ðŸ“°]
formato_video: [explainer 5-10 min | short 60-90 sec | case-study 4-8 min]
titolo_on_thumbnail: [max 6-8 parole Â· contrast forte]
include_avatar_heygen: [NO default | SÃŒ se video usa HeyGen e brief richiede esplicitamente]
ai_disclosure_richiesta: [NO se illustrazione | SÃŒ se avatar HeyGen visibile]
---
```

---

## 3. Specifiche thumbnail YouTube Advisory+

### Formato
- **1280Ã—720 pixel** (standard YouTube)
- **Ratio 16:9 landscape**
- File PNG (mai JPG per non degradare il testo on-image)

### Coerenza con Cover Blog System
Le thumbnail YouTube ricalcano lo stesso linguaggio visivo del Cover Blog System (sez. 3 della skill `visual-cover-blog`), adattato al formato landscape 16:9:

| Categoria | Stile thumbnail YouTube |
|---|---|
| ðŸ§  Educazione | Vector flat illustration didattica + titolo grande |
| ðŸ“– Caso Reale | Editorial illustration narrativa + titolo + footer "Caso reale, nomi di fantasia" sottile |
| ðŸ“Š Analisi (v1.2) | Data visualization + dato chiave on-thumbnail (JetBrains Mono) + titolo |
| âœï¸ Voce CEO | Editorial sobrio + nome "Daniele Simonini" in calce |
| ðŸ“° News | Editorial news + eventuale date stamp + titolo impact |

### Tipografia titolo on-thumbnail
- **Inter Tight bold** dimensione molto grande (80-100pt) â€” leggibile su mobile YouTube
- **Max 6-8 parole** (oltre illeggibile su anteprima mobile)
- **Contrast forte**: testo bianco su navy 700/800 OPPURE testo navy su mist
- Allineamento variabile (centro, sinistra, destra) a seconda della composizione

### Logo Advisory+
- **In corner alto destra** (sigla `+` o logo `mark`, non logo full per non saturare lo spazio)
- Dimensione discreta: ~80-100px altezza
- Watermark invisibile non necessario

### Visual element
- **Default: illustrazione concept** generata da cc-nano-banana (no foto-realistico)
- **Eccezione**: se il video usa HeyGen avatar e il brief MM lo richiede esplicitamente, screenshot dell'avatar HeyGen (frame del video) â€” in questo caso AI disclosure obbligatoria + sigla "Avatar AI" visibile sul thumbnail per evitare confusione utente
- **MAI**: foto Daniele Simonini o altri soci (rischio confusione "video AI con thumbnail persona reale")

### Sub-identity Specialty (se attiva)
- Accent ocra Warning â‰¤5% area visuale (badge "Specialty: [P10/P11/P12]" o filetto)
- Come per Cover Blog System sez. 4

---

## 4. Esclusioni â€” clichÃ© YouTube vietati

Advisory+ Ã¨ brand consulenziale professionale: i clichÃ© tipici di YouTube clickbait sono **vietati**.

- âŒ **Frecce rosse giganti** che puntano a qualcosa nel thumbnail
- âŒ **Emoji shock** (ðŸ¤¯ ðŸš¨ ðŸ˜± in dimensione enorme)
- âŒ **TITOLI IN MAIUSCOLO** ("LA VERITÃ€ CHE NESSUNO TI DICE")
- âŒ **Faccia espressiva** del creator (no Daniele, no avatar HeyGen con espressione esagerata)
- âŒ **Numeri cerchiati con marcatore rosso** ("3 COSE!" cerchiato)
- âŒ **"CLICK BAIT" text patterns** ("SHOCKING!", "MUST WATCH!", "INCREDIBILE!")
- âŒ **Cerchio rosso registrazione** (mimica live)
- âŒ **Loghi mandatarie** (vincolo IVASS)

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal chiamante (titolo video, categoria, formato video, pillar, eventuale uso HeyGen avatar)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/design-system.json` per palette + font + thumbnail YouTube specifiche
4. **Lookup categoria** (sez. 3) per stile coerente con Cover Blog System
5. **Comporre titolo on-thumbnail** (max 6-8 parole, Inter Tight bold grande)
6. **Determinare visual element**:
   - Default: illustrazione concept (no avatar visibile)
   - Se brief MM richiede screenshot avatar HeyGen: includi + AI disclosure
7. **Composizione prompt** cc-nano-banana integrando: categoria + palette + iconografia + sub-identity (se attiva) + titolo on-thumbnail + esclusioni clichÃ©
8. **Invocare `advisory-plus:visual-image-static-nano-banana`** via Task tool:
   ```
   Task(
     subagent_type: "advisory-plus:visual-image-static-nano-banana",
     prompt: "Thumbnail YouTube 1280Ã—720 categoria [X] Â· voce [Y] Â· titolo '[Z]' Â· visual element [illustrazione concept | avatar HeyGen screenshot] Â· esclusioni clichÃ© YouTube clickbait."
   )
   ```
9. **Ricevere file PNG** generato + metadata
10. **Se include avatar HeyGen visibile**: invocare `advisory-plus:compliance-ai-disclosure` tipologia A per generare sigla "Avatar AI Â· Advisory+" da overlay manualmente o brief Art Director
11. **Salvare** in `Output_approvati/[file]_assets/thumbnail_youtube_[id].png`
12. **Restituire metadata + path file PNG** al chiamante (content-youtube-video)

---

## 6. Casi particolari

### Thumbnail per Pillar 2 Voce CEO (Daniele)
- Categoria âœï¸ Voce CEO
- **Mai foto Daniele** sul thumbnail (per coerenza: il video Ã¨ prodotto dalla redazione, l'autorialitÃ  Ã¨ espressa diversamente)
- Visual element: editorial illustration + nome "Daniele Simonini" in calce
- Eccezione: se Daniele appare IN PRIMA PERSONA in camera nel video (no HeyGen) â†’ screenshot autentico ammesso

### Thumbnail per video con avatar HeyGen visibile
- Brief MM richiede esplicitamente avatar in thumbnail
- Screenshot avatar da video HeyGen
- AI disclosure obbligatoria: sigla "Avatar AI Â· Advisory+" sovrapposta in corner basso (non in caption â€” Ã¨ on-thumbnail diretto)
- Compliance Officer gate raddoppiato

### A/B testing thumbnail
- Skill puÃ² generare 2-3 varianti per stesso video (composizioni diverse, palette diverse all'interno del Design System)
- MM decide quale usare per pubblicazione
- Costo: 2-3 Ã— $0.04 cc-nano-banana

### Thumbnail per YouTube Short
- Stesso formato 1280Ã—720? **NO**: Short usa thumbnail 1080Ã—1920 verticale (formato Short)
- Per Short, invocare `visual-image-static-nano-banana` direttamente con formato verticale (non questa skill che Ã¨ specifica per landscape)
- Nota: questa skill Ã¨ per **video lunghi YouTube** (explainer + case-study); Short usa thumbnail verticali generate da altra invocazione

### Thumbnail per video co-marketing
- Logo partner ammesso (autorizzato dalla partnership)
- Logo Advisory+ + logo partner in corner alto
- Loghi mandatarie restano vietati

---

## 7. Cosa NON fare mai

- âŒ **Foto Daniele o altri soci** sul thumbnail (anche se video Ã¨ in prima persona â€” eccezione rara, da valutare caso per caso)
- âŒ **ClichÃ© YouTube clickbait** (frecce rosse, emoji shock, MAIUSCOLO, faccia espressiva esagerata, cerchi rossi)
- âŒ **Titolo on-thumbnail >8 parole** (illeggibile mobile)
- âŒ **Loghi mandatarie** (vincolo IVASS)
- âŒ **Palette diverse da Design System** (no creative override)
- âŒ **Saltare AI disclosure** se avatar HeyGen visibile sul thumbnail
- âŒ **Categoria non in mappa Cover Blog System** (sez. 3 â€” sono 5 esatte)
- âŒ **JPG invece di PNG** (degrada testo on-image)
- âŒ **Sub-identity Specialty >5% area** (regola Brand Book v1.2 sez. 8.1)
- âŒ **Formato diverso da 1280Ã—720** (per Short usa 1080Ã—1920 con altra skill)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 8 Design System Â· sez. 8.1 Cover Blog System (allineamento categoria thumbnail) Â· sez. 14 stack video YouTube)
2. `/01_Team/05_Art_Director.md` Â· `/01_Team/09_Content_Producer.md`
3. `config/design-system.json` (palette, font, thumbnail YouTube specifiche)
4. `config/brand.json` (categorie editoriali + specialty)
5. Il brief contenuto del chiamante (content-youtube-video)

---

*SKILL v1.0 â€” advisory-plus:visual-thumbnail-youtube â€” Sessione 4 Plugin Build â€” 2026-05-19*

