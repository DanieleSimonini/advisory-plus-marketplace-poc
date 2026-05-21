---
name: visual-image-static-nano-banana
description: Wrapper Advisory+ per cc-nano-banana (Gemini 2.5 Flash Image via gemini-cli + extension, dependency esterna repo kkoppenhaver/cc-nano-banana, costo ~$0.04/img). Genera immagini static brand-coerenti per cover blog, post quadrati 1080Ã—1080, story 1080Ã—1920, hero newsletter 600Ã—200, thumbnail YouTube 1280Ã—720, illustrazioni inline. Composiziona prompt ottimizzati che integrano automaticamente Design System v1.0 (palette Navy 700 #001660 + Teal 500 #2DD4C5 + Mist #F2F4F9 + Ink #0F1A38) + font stack (Inter Tight headline + Source Serif 4 citazioni + JetBrains Mono dati) + voce editoriale (Spiegato Facile = illustrazioni didattiche calme Â· Badvisor = visual asciutti ad alto contrasto Â· Caso Reale = illustrazioni narrative non foto-realistiche Â· Analisi = grafici/schemi/dati visualizzati). Esclude automaticamente fattezze identificabili Daniele Simonini e altri soci. Esegue shell call a cc-nano-banana via Bash, riceve file PNG, salva in _assets/ del contenuto chiamante. Invoca compliance-ai-disclosure solo se output foto-realistico.
---
# ðŸŽ¨ Skill visual-image-static-nano-banana â€” Wrapper cc-nano-banana per immagini Advisory+

> **cc-nano-banana = Gemini 2.5 Flash Image. ~$0.04/img. Brand-coerente automatico via prompt engineering Design System v1.0.**

---

## 1. Quando triggera

- Invocata dalle skill content-* per generare visual (cover blog, post quadrati, stories, hero newsletter, thumbnail YouTube, illustrazioni inline)
- Mai auto-trigger autonomo: serve sempre brief visivo dal chiamante (`content-*` o MM)

Tempo target di esecuzione: **2-4 minuti per immagine** (dipende da latenza Gemini API).

---

## 2. Output finale atteso

**File PNG generato** consegnato al chiamante, salvato in:
```
Output_approvati/[file].md â†’ asset in Output_approvati/[file]_assets/[nome_visual]_[id].png
```

(convenzione `_assets/` ratificata CEO 2026-05-18)

+ **Metadata** sintetici restituiti al chiamante:
```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/[nome]_[id].png
formato: [es. 1080Ã—1080 quadrato | 1200Ã—630 landscape | 1080Ã—1920 verticale | 600Ã—200 hero]
motore: cc-nano-banana (Gemini 2.5 Flash Image)
prompt_used: [prompt finale inviato al motore]
costo_stimato_usd: ~0.04
ai_disclosure_richiesta: [SÃŒ se foto-realistico | NO se illustrazione/concept]
---
```

---

## 3. Specifiche formato per output

| Formato | Dimensioni | Uso tipico |
|---|---|---|
| Quadrato | 1080Ã—1080 | Post Instagram singolo, post LinkedIn brand (opzionale) |
| Landscape LinkedIn | 1200Ã—628 | Cover blog teaser LinkedIn |
| Landscape Facebook | 1200Ã—630 | Cover post Facebook brand |
| Landscape blog cover | 1200Ã—630 | Cover blog THE ADVISOR (template Cover Blog System) |
| Verticale Stories/Reel | 1080Ã—1920 | Stories IG/FB Â· Reel cover |
| Verticale YouTube Short | 1080Ã—1920 | Short YouTube thumbnail |
| Hero newsletter | 600Ã—200 | Banner hero newsletter Brevo |
| Thumbnail YouTube | 1280Ã—720 | Thumbnail video YouTube |
| Carosello slide | 1080Ã—1080 Ã— N | Carosello Instagram 3-10 slide |
| Inline articolo | 1200Ã—800 (variabile) | Immagini inline articolo blog |

---

## 4. Prompt engineering â€” pattern Design System

Il prompt finale inviato a cc-nano-banana **integra automaticamente** elementi Design System v1.0 per garantire coerenza brand. Pattern base:

```
[descrizione contenuto specifico richiesto dal chiamante]

Style: [Spiegato Facile | Badvisor | Caso Reale | Analisi style â€” vedi sez. 5]

Palette: deep navy blue #001660 (primary), darker navy #011750 (background), teal cyan #2DD4C5 (accent, single accent only), light mist gray #F2F4F9 (surface), dark ink #0F1A38 (text). NO other accent colors. NO red, green, orange (except specialty drops with ochre Warning â‰¤5%).

Typography (if text on image): Inter Tight bold for headlines, max 5-7 words on image. NO Source Serif except for editorial quotes. NO JetBrains Mono except for data displays.

Composition: clean modern editorial design, generous white space, grid-aligned, professional consulting feel. NO clutter. NO stock-photo clichÃ©. NO clichÃ©d insurance imagery (umbrellas in rain, handshakes, family-with-house silhouettes).

EXCLUDE: photorealistic faces of identifiable people. NO clone of Italian male, ~50 years old, professional consultant appearance (avoid Daniele Simonini-resembling features). NO faces at all if illustration, prefer abstract/conceptual.

Output: [formato esatto, es. 1080Ã—1080 square PNG transparent or solid background per chiamante].
```

---

## 5. Style per voce editoriale

### Spiegato Facile â€” illustrazioni didattiche calme
- **Stile**: vector flat illustration, soft gradients, friendly mood
- **Elementi**: oggetti quotidiani (frigorifero, chiavi, casa, ombrello, libro), metafore semplici, icone
- **Mood**: caldo, accessibile, rassicurante
- **Esempio prompt**: "Vector flat illustration of a refrigerator with thought bubbles showing insurance concepts. Friendly, modern, didactic. Palette as specified."

### Badvisor â€” visual asciutti ad alto contrasto
- **Stile**: minimalist, bold contrast, typography-heavy
- **Elementi**: forme geometriche, pittogrammi essenziali, testi grandi on-image
- **Mood**: provocatorio (verso paradosso), netto, sveglio
- **Esempio prompt**: "Bold minimalist visual with strong typography. Single concept, high contrast. Conceptual, not literal. Palette as specified."

### Caso Reale â€” illustrazioni narrative non foto-realistiche
- **Stile**: editorial illustration, scene narrative, color-grading caldo
- **Elementi**: scene di vita quotidiana (cucina, ufficio, casa di anziano), oggetti narrativi
- **Mood**: empatico, sobrio, mai sentimentale
- **CRITICO**: **NO foto-realistic faces** â€” usa illustrazione editoriale dove i volti sono stilizzati o non visibili
- **Esempio prompt**: "Editorial illustration of an elderly woman's hand on a kitchen counter, soft afternoon light, conceptual not photorealistic. No identifiable face. Warm narrative mood."

### Analisi â€” grafici/schemi/dati visualizzati
- **Stile**: data visualization, schematic, infographic clean
- **Elementi**: grafici, percentuali on-image (JetBrains Mono), schemi normativi, timeline
- **Mood**: asciutto, oggettivo, autorevole
- **Esempio prompt**: "Clean data visualization showing percentage decrease over years. Schematic, infographic style. JetBrains Mono font for numbers, Inter Tight for labels. Palette as specified."

---

## 6. Esclusioni automatiche â€” vincoli sempre attivi

### Persone identificabili
- **EXCLUDE: clone Daniele Simonini** (Italian male ~50 anni, professional consultant)
- **EXCLUDE: clone altri soci** (Agostini, Barrella, Fappani, senior advisor)
- **EXCLUDE: foto-realistic faces in general** se non strettamente necessario al brief
- Default: prefer abstract, conceptual, illustration

### ClichÃ© assicurativi vietati
- Ombrelli sotto la pioggia
- Strette di mano corporate
- Sagome famiglia-con-casa
- Mani che proteggono una famiglia di omini
- Salvadanai a maialino
- Tutti i clichÃ© stock-photo "insurance"

### Riferimenti territoriali
- **EXCLUDE**: panoramiche Versilia/Apuana/Toscana riconoscibili
- Foto/illustrazioni di luoghi sempre generiche

### Loghi mandatarie
- **MAI** loghi mandatarie generati nel visual (vincolo IVASS â€” loghi vanno solo in disclosure footer, non in visual social/cover)

---

## 7. Logica di esecuzione â€” passo-passo

1. **Ricevere brief visivo** dal chiamante (contenuto, voce, formato, eventuali elementi specifici)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/design-system.json` per palette/font correnti (fonte di veritÃ )
4. **Leggere** `config/budget.json` sez. `image_gen_monthly_cap` per verificare quota residua
5. **Se quota residua <80%**: warning al MM
6. **Se quota residua = 0%**: blocco con notifica
7. **Comporre prompt finale** integrando: brief contenuto + style per voce + Design System palette/font + esclusioni vincoli + formato richiesto
8. **Eseguire shell call** a cc-nano-banana via Bash:
   ```bash
   nano-banana generate \
     --prompt "[prompt finale]" \
     --width [W] --height [H] \
     --output "Output_approvati/[file]_assets/[nome]_[id].png" \
     --api-key $GEMINI_API_KEY
   ```
9. **Ricevere output PNG** generato
10. **Verifica visiva automatica** (lookup metadata immagine: dimensioni corrette, file size non degenere)
11. **Se output foto-realistico** rilevato (heuristic): invoca `advisory-plus:compliance-ai-disclosure` tipologia C per AI disclosure
12. **Loggare** in `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_log.md` con: data, contenuto chiamante, prompt usato, costo stimato, esito
13. **Restituire metadata + path file PNG** al chiamante

---

## 8. Casi particolari

### Generazione fallita (API down, quota Gemini esaurita)
- Skill non simula: errore esplicito al chiamante
- Suggerisce fallback: `advisory-plus:visual-image-static-canva` (Sessione 4 se Canva MCP Ã¨ attivo) o stock generico Pexels/Unsplash via Cloudinary

### Generazione di carosello multi-slide (es. 5 slide Ã— 1080Ã—1080)
- Loop N invocazioni con prompt coerenti tra di loro (stesso style, stessa palette, narrative continuity)
- Costo cumulato (5 slide Ã— $0.04 = ~$0.20)
- Output: 5 file PNG con naming `_slide_1.png`, `_slide_2.png`, etc.

### Brief non chiaro o ambiguo
- Skill chiede chiarimento al chiamante PRIMA di consumare quota Gemini
- Esempio: "Voce indicata: Analisi. Brief contenuto: 'visual articolo P5 LTC'. Posso generare una visualizzazione dati COVIP sulla LTC oppure uno schema concettuale del bisogno LTC. Quale preferisci?"

### Richiesta visual con persona identificabile (cliente, socio, partner)
- ðŸ”´ blocco immediato
- Suggerisce: "Use real photo with explicit written consent, do not generate AI portrait."

### Budget guardrail attivo (`config/budget.json` cap mensile raggiunto)
- ðŸ”´ blocco generazione
- Notifica MM e CEO: "Budget image-gen mensile esaurito. Sospensione generazione fino a inizio mese o aumento cap."

### Validazione bozza prima di consumare quota
- ModalitÃ  "dry-run": skill puÃ² restituire SOLO il prompt che genererebbe senza eseguire shell call
- Utile per MM/CEO che vogliono validare la composizione del prompt prima di consumare quota Gemini
- Triggera via parametro `--dry-run`

---

## 9. Cosa NON fare mai

- âŒ **Generare clone Daniele Simonini o altri soci** (vincolo etico CEO 2026-05-16, esclusione automatica nel prompt)
- âŒ **Generare loghi mandatarie** (vincolo IVASS)
- âŒ **Ignorare Design System palette** (palette fissa, no creative override)
- âŒ **Generare clichÃ© stock-photo insurance** (umbrellas, handshakes, family silhouettes)
- âŒ **Foto-realistic faces** senza necessitÃ  (default illustrazione astratta)
- âŒ **Ignorare budget cap** in `config/budget.json` (rispetto guardrails)
- âŒ **Saltare AI disclosure** se output foto-realistico (invocazione compliance-ai-disclosure obbligatoria)
- âŒ **Saltare log** in `Log_visual_generati/[YYYY-MM]_log.md`
- âŒ **Auto-modificare** Design System o palette (modifiche sono di Art Director + Brand Strategist)

---

## 10. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 8 Design System v1.0 Â· sez. 14 ETICA AI)
2. `/01_Team/05_Art_Director.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/design-system.json` (palette, font, formati standard)
4. `config/brand.json` (esclusioni mandatarie + ETICA AI)
5. `config/budget.json` (cap mensile image-gen)
6. Il brief visivo del chiamante

---

*SKILL v1.0 â€” advisory-plus:visual-image-static-nano-banana â€” Sessione 4 Plugin Build â€” 2026-05-19*

