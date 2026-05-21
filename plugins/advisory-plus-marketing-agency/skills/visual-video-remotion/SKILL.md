---
name: visual-video-remotion
description: Wrapper Advisory+ per Remotion (TypeScript/React video framework, open source, skill remotion-dev/skills). Genera video tipografici brand-coerenti per Reel motion graphics, Stories animation, intro/outro brand per YouTube, transizioni, dati visualizzati animati (perfetto per voce Analisi). Composiziona file TypeScript Remotion integrando Design System v1.0 (palette Navy 700 + Teal 500 + tipografie Inter Tight + JetBrains Mono per dati) + asset di brand (logo Advisory+ animato, tagline). Supporta voice-over autentica (registrazione audio Daniele o operatore brand) â€” pattern raccomandato per Pillar 2 Voce CEO (alternativa autentica a HeyGen avatar che Ã¨ vietato per Daniele). Esegue render via Node.js + Remotion CLI installato sul computer del CEO (Fase 1c setup), riceve file MP4, salva in _assets/. NESSUNA AI disclosure obbligatoria (Remotion Ã¨ motion graphics + voce off autentica = contenuto umano, non rientra in AI Act UE artt. 50, 52 â€” Brand Book v1.2 sez. 14.4).
---
# ðŸŽžï¸ Skill visual-video-remotion â€” Wrapper Remotion motion graphics

> **TypeScript/React open source. Brand-coerente automatico. Voice-over autentica. Nessuna AI disclosure (Ã¨ umano).**

---

## 1. Quando triggera

- Invocata dalle skill content-reel-script (per Reel tipografici motion graphics) e content-youtube-video (per intro/outro brand + b-roll animati)
- Invocata anche per video standalone Pillar 2 Voce CEO (quando Daniele vuole video senza apparire in camera ma con voce autentica)
- Mai auto-trigger: serve brief dal chiamante

Tempo target di esecuzione: **10-20 minuti per video** (dipende da durata e complessitÃ  + render time Remotion in locale).

---

## 2. Output finale atteso

**File MP4** + metadata + sorgente TypeScript Remotion consegnati al chiamante:

```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/[nome]_[id].mp4
source_remotion: Output_approvati/[file]_assets/[nome]_[id].remotion.tsx
formato: 1080Ã—1920 verticale (Reel/Stories) o 1920Ã—1080 orizzontale (YouTube)
durata: [N] sec
motore: Remotion (TypeScript/React)
voce_off: [autentica_Daniele | autentica_brand_operatore | testo_on_screen_solo (no audio)]
audio_file: [path file audio voice-over se esistente, altrimenti N/A]
ai_disclosure: NESSUNA (Remotion Ã¨ motion graphics + voice-over umana, non AI generativa)
---
```

---

## 3. Specifiche Remotion Advisory+

### Stack tecnico
- **Remotion** open source (https://remotion.dev/)
- **Node.js** richiesto sul computer del CEO (Fase 1c setup)
- **Skill remotion-dev/skills** importate come template base
- **Render in locale** (no cloud cost) â†’ costo marginale solo elettricitÃ 

### Formati output
- **Reel/Stories**: 1080Ã—1920 verticale 30fps
- **YouTube**: 1920Ã—1080 orizzontale 30fps
- **Newsletter video embedded**: 1280Ã—720 orizzontale 30fps (raro)

### Design System integrato
Tutti i file TypeScript Remotion importano automaticamente da `config/design-system.json`:

```typescript
import { Palette, Fonts, Logo } from '@advisoryplus/design-system';

// Disponibili:
Palette.navy_700  // #001660 primary
Palette.navy_800  // #011750 background
Palette.teal_500  // #2DD4C5 accent
Palette.mist      // #F2F4F9 surface
Palette.ink       // #0F1A38 text
Palette.warning_ochre // accent ocra â‰¤5% per Specialty drops

Fonts.inter_tight   // headline + UI
Fonts.source_serif  // citazioni editoriali
Fonts.jetbrains_mono // dati numerici

Logo.full  // logo Advisory+ completo (per intro/outro)
Logo.mark  // solo marchio (per watermark corner)
```

### Voice-over autentica
- **Pattern raccomandato per Pillar 2 Voce CEO**: registrazione audio Daniele autentica (mai HeyGen voice)
- **Pattern brand**: voice-over operatore Advisory+ autentico (chiunque della redazione)
- **Pattern silente**: video solo con testo on-screen + musica royalty-free (no voice-over) â€” opzione per Reel veloci
- File audio formato: WAV o MP3, 44.1 kHz, mono o stereo

### Sottotitoli burned-in
- Generati automaticamente dal Remotion via `@remotion/captions` con timing da audio
- Posizione bassa centrale, font Inter Tight bold, contrast forte
- Correzione manuale possibile editing TSX se errori (raro su voce-over autentica vs HeyGen)

### Musica
- **Royalty-free obbligatoria** (Epidemic Sound, Artlist, YouTube Audio Library, Freesound CC0)
- Tracciamento licenza in `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_remotion_audio_licenses.md`
- Mai musica coperta da copyright (rischio takedown)

---

## 4. Template Remotion ricorrenti

### Template 1 â€” Intro YouTube/Reel brand
- Logo Advisory+ animato (fade-in + scale) + tagline "Consulenza assicurativa. Sul serio." + bumper 3-5 sec
- Riutilizzabile cross-video
- File: `intro_brand.remotion.tsx`

### Template 2 â€” Outro YouTube/Reel CTA
- "Iscriviti al canale" animation + logo + tagline + 3-5 sec
- File: `outro_cta.remotion.tsx`

### Template 3 â€” Reel tipografico Spiegato Facile
- Sequenza testo on-screen a passi numerati (1, 2, 3) + analogia visiva con icona
- File: `reel_didattico.remotion.tsx`

### Template 4 â€” Reel Badvisor punch
- Hook testo grande + asimmetria visiva + chiusura sarcastica
- File: `reel_badvisor.remotion.tsx`

### Template 5 â€” Reel Analisi data visualization
- Grafico animato (curve, barre, dati che crescono) + apparato citazionale on-screen
- File: `reel_analisi_data.remotion.tsx`

### Template 6 â€” Reel Caso Reale storytelling
- Sequenza testo + illustrazione editoriale (no foto persone) + disclaimer "Caso reale, nomi di fantasia"
- File: `reel_caso_reale.remotion.tsx`

### Template 7 â€” YouTube b-roll animation
- Schemi normativi animati + timeline + dati visualizzati per articoli Analisi
- File: `youtube_broll.remotion.tsx`

I template sono in `scripts/remotion-templates/` (popolati progressivamente nelle prime iterazioni del plugin).

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal chiamante (script, durata, formato, voice-over file path se esistente, template Remotion preferito)
2. **Eseguire kickoff** per contesto workspace
3. **Lookup template** Remotion adatto (sez. 4) â€” se brief non specifica, scegli template default per voce/canale
4. **Comporre file TypeScript Remotion** (`[nome]_[id].remotion.tsx`) partendo dal template + dati specifici (testo, durata, voice-over file)
5. **Eseguire render Remotion via Bash + Node.js**:
   ```bash
   npx remotion render \
     "Output_approvati/[file]_assets/[nome]_[id].remotion.tsx" \
     [composition_id] \
     "Output_approvati/[file]_assets/[nome]_[id].mp4" \
     --props='{"voiceover": "path/audio.mp3"}'
   ```
6. **Verifica output MP4** generato (lookup file size, durata corretta)
7. **Loggare** in `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_remotion.md` con: data, durata, template usato, esito
8. **Restituire metadata + path file MP4 + sorgente TSX** al chiamante

**Nessuna invocazione `advisory-plus:compliance-ai-disclosure`** (Remotion Ã¨ motion graphics + voice-over umana, non rientra in AI Act UE artt. 50, 52).

---

## 6. Casi particolari

### Voice-over Daniele autentica per Pillar 2 (alternativa a HeyGen vietato)
- Daniele registra audio (smartphone va bene per audio breve, ideale microfono pro)
- Audio salvato in `Output_approvati/[file]_assets/voiceover_daniele_[id].mp3`
- Skill genera video Remotion con voce-over autentica + visual tipografico
- **Pubblicazione semi-manuale** (Daniele approva personalmente, come per LinkedIn personale)

### Video Reel completamente silente (no voice-over)
- Testo on-screen + musica royalty-free
- Sottotitoli generati da testo on-screen stesso
- Veloce da produrre (~5 min render)

### Video con dati visualizzati per voce Analisi
- Template `reel_analisi_data.remotion.tsx` o `youtube_broll.remotion.tsx`
- Dati hard-coded nel TSX (non auto-fetch dinamico)
- Apparato citazionale on-screen (fonte + anno visibili nel video)

### Video co-marketing con logo partner
- Logo partner integrato nel TSX (asset PNG transparente in `Output_approvati/[file]_assets/partners/`)
- Logo Advisory+ + logo partner in intro o outro
- Loghi mandatarie restano vietati on-screen (vincolo IVASS invariato)

### Render fallito (Node.js error, Remotion error)
- Skill restituisce errore esplicito + log Bash al MM
- Suggerimento: verifica setup Node.js + Remotion (Fase 1c setup CEO computer)

### Pubblicazione di video Remotion che include screenshot interfaccia HeyGen (raro, ipotetico)
- Skill ignora: il video Remotion in sÃ© non Ã¨ AI generativa; eventuali contenuti AI mostrati al suo interno ricadrebbero sotto compliance-ai-disclosure (caso edge da gestire manualmente)

---

## 7. Cosa NON fare mai

- âŒ **Generare voice-over con AI** (Remotion Ã¨ per motion graphics + voice umana o silente â€” no AI voice in Remotion)
- âŒ **Inserire foto persone identificabili** nel TSX senza consenso scritto
- âŒ **Inserire loghi mandatarie** nel video (vincolo IVASS â€” solo in disclosure footer materiali corporate, non in video)
- âŒ **Music coperta da copyright** (solo royalty-free, tracciata in log audio_licenses)
- âŒ **Ignorare Design System** (palette/font fissi da `config/design-system.json`)
- âŒ **Saltare log** in `Log_visual_generati/[YYYY-MM]_remotion.md`
- âŒ **Generare AI disclosure** (Remotion Ã¨ umano, no disclosure necessaria â€” Ã¨ errore se invocata)
- âŒ **Pubblicare con sottotitoli sbagliati** (correzione manuale TSX se needed)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 8 Design System Â· sez. 14 stack video â€” Remotion specifications)
2. `/01_Team/09_Content_Producer.md` Â· `/01_Team/05_Art_Director.md`
3. `config/design-system.json` (palette, font, asset)
4. `scripts/remotion-templates/` (template TSX riutilizzabili)
5. Il brief del chiamante

---

*SKILL v1.0 â€” advisory-plus:visual-video-remotion â€” Sessione 4 Plugin Build â€” 2026-05-19*

