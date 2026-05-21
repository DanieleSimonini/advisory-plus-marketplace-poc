---
name: visual-video-composite-explainer
description: Wrapper Advisory+ per la pipeline canonical di composite video Pillar-explainer (HeyGen webm avatar con alpha + Remotion kinetic typography + brand overlay + light bg gradient). Validata empiricamente il 2026-05-19 sera con PoC Pillar 5 LTC (9 iterazioni di convergenza, stress test su 3 avatar/look). Genera video composite 25-60 sec adatti a YouTube Short, Reel IG, post LinkedIn video, embed newsletter â€” con avatar a destra che parla, testo kinetic a sinistra, logo Advisory+ alto sinistra, accent bar Teal 500 verticale. Pipeline obbligatoria (NON tentare chromakey, lumakey, blend mode CSS): (1) HeyGen API con parametro `outputFormat: "webm"` per photo_avatar (alpha VP9 nativo all'origine, non `removeBackground=true` che Ã¨ download flag fallibile e vale solo per video_avatar con matting esplicito), (2) Remotion `OffthreadVideo` con prop `transparent` (rispetta alpha sorgente), (3) light bg gradient biancoâ†’mist (l'alone scrivania residuo del matting AI si fonde invisibile col bg chiaro â€” NO dark bg + mix-blend-mode lighten, Remotion headless Chromium non rispetta blend mode), (4) layout parametrizzato con constanti `AVATAR_RIGHT_OFFSET=-400` e `TEXT_AREA_WIDTH=1100` in alto al file Composite.tsx (riusabilitÃ  invariante per avatar/outfit/look futuri). ModalitÃ  render production: ModalitÃ  A weekly batch (PC CEO acceso 30 min/sett, MM notifica via Friday email, CEO clicca `run-render-batch.ps1`). Upgrade pianificato ModalitÃ  D Remotion Lambda cloud render in v1.2 autunno 2026. AI disclosure OBBLIGATORIA (avatar HeyGen visibile in scena = AI Act UE art. 50, invoca compliance-ai-disclosure tipologia A).
---
# ðŸŽ¬ Skill visual-video-composite-explainer â€” Pipeline composite HeyGen webm + Remotion

> **Pipeline canonical validata empiricamente PoC 2026-05-19 (CEO: "Perfetta!!!" su render v9). NON tentare alternative.**
> **Stack: HeyGen `outputFormat=webm` â†’ Remotion `OffthreadVideo transparent` â†’ light bg gradient â†’ layout parametrizzato.**

---

## 1. Quando triggera

- Invocata dalle skill `content-youtube-video` (per Short explainer 30-90s) e `content-reel-script` (per Reel composite avatar + testo kinetic)
- Invocata da `content-blog-article` quando l'articolo prevede video embedded (Pillar 5/6/9 con avatar che parla + cifre/concetti chiave kinetic-animati)
- Mai auto-trigger: serve sempre brief script dal chiamante (script HeyGen + lista 4-8 cue testuali kinetic + pillar + voce avatar)

Tempo target di esecuzione end-to-end: **~25-40 min** per video composite 25-60 sec (HeyGen generation 8-15 min + Remotion render 5-12 min + brand overlay assembly 5-10 min). ModalitÃ  A weekly batch: render concentrato in 1 sessione PC settimanale di ~30 min.

---

## 2. Output finale atteso

**File MP4 composite finale** + sorgente Remotion TypeScript + webm avatar alpha consegnati al chiamante:

```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/composite_[pillar]_[tema]_[id].mp4
source_remotion: Output_approvati/[file]_assets/Composite.tsx
avatar_webm_alpha: Output_approvati/[file]_assets/avatar_[name]_alpha.webm
formato: 1920Ã—1080 H.264 30fps (YouTube/LinkedIn) o 1080Ã—1920 (Short/Reel)
durata: [N] sec
pipeline: HeyGen webm alpha + Remotion OffthreadVideo transparent + light bg gradient + brand overlay
avatar_selezionato: [Gino landscape grey blazer | Gina landscape blue pinstriped | altri stock italiani]
voce_selezionata: [voice_id HeyGen]
testo_kinetic_cues: [N cue testuali animati]
layout_parametri:
  AVATAR_RIGHT_OFFSET: -400
  TEXT_AREA_WIDTH: 1100
  AVATAR_SCALE: 1.0
bg_gradient: "linear-gradient(135deg, #FFFFFF 0%, #F2F4F9 100%)"
brand_overlay:
  logo_top_left: "Advisory+ colori originali"
  accent_bar_left: "Teal 500 verticale"
  watermark_bottom: "Advisory+ Â· RUI A000669271"
ai_disclosure: OBBLIGATORIA â€” invocata compliance-ai-disclosure tipologia A
modalita_render: "A weekly batch" (PC CEO PowerShell run-render-batch.ps1)
costo_minuti_heygen_consumati: [N min]
quota_mensile_heygen_residua: [Y min / 15 min]
---
```

---

## 3. Pipeline canonical â€” 4 step OBBLIGATORI

### Step 1 â€” HeyGen API: `outputFormat: "webm"` (NON `removeBackground=true`)

**Insight architetturale chiave PoC 2026-05-19:**

- `outputFormat: "webm"` Ã¨ il **vero parametro API di matting source** per `photo_avatar` (Creator tier ok). Attiva matting AI HeyGen (MODNet/RVM-like) all'origine, produce VP9 con alpha channel nativo, robusto su qualunque outfit/look.
- `removeBackground=true` Ã¨ invece un **URL flag download post-processing** che vale solo per `video_avatar` trainati con matting esplicito â†’ fallibile su photo_avatar.

**Chiamata corretta:**

```typescript
// Tramite HeyGen MCP ufficiale (mcp__heygen__create_video_from_avatar)
{
  avatar_id: "[photo_avatar_id stock italiano]",
  voice_id: "[voice_italian_id]",
  input_text: "[script ricevuto dal chiamante]",
  outputFormat: "webm",   // â¬…ï¸ KEY â€” alpha VP9 nativo
  test: false,
  dimension: { width: 1920, height: 1080 }
}
```

**Output atteso:** file `.webm` ~20-30 MB per 25 sec a 1080p, alpha channel pulito, **zero preprocessing necessario**.

**Validato empiricamente (PoC 2026-05-19) su:**
- Gina photo_avatar pinstripe blazer 25.4 sec â†’ alpha pulito âœ…
- Gino photo_avatar grey blazer 21.8 sec â†’ alpha pulito âœ…
- Gina photo_avatar BLACK blazer 25.4 sec (stress test outfit-nero-su-bg-nero) â†’ alpha pulito âœ…

**Pipeline invariante** rispetto a avatar/outfit/look futuri.

### Step 2 â€” Remotion `OffthreadVideo` con prop `transparent`

```typescript
import { OffthreadVideo } from 'remotion';

<OffthreadVideo
  src={staticFile('avatar_gina_true_alpha.webm')}
  transparent={true}   // â¬…ï¸ KEY â€” rispetta alpha VP9 sorgente
  style={{
    position: 'absolute',
    right: AVATAR_RIGHT_OFFSET,
    top: 0,
    height: '100%',
    objectFit: 'cover',
  }}
/>
```

**Note:**
- `OffthreadVideo` (non `Video`) Ã¨ obbligatorio per video con alpha channel (Remotion docs: "Required for transparent webm")
- Headless Chromium con `transparent={true}` consuma piÃ¹ RAM (~2x): chiudere altri tab/programmi durante render
- 30fps target consigliato (60fps esplode il render time senza beneficio percettibile)

### Step 3 â€” Light bg gradient (NON dark bg + blend mode)

```typescript
// AbsoluteFill di background
<AbsoluteFill style={{
  background: 'linear-gradient(135deg, #FFFFFF 0%, #F2F4F9 100%)',
  // Bianco Paper â†’ Mist (Brand Book v1.2 sez. 8.2)
}}>
```

**PerchÃ© light bg e non dark bg + `mix-blend-mode: lighten`:**

Tentato in PoC v5 (Vox/Wendover style) â†’ **Remotion headless Chromium NON rispetta blend mode CSS su `OffthreadVideo`**: render ignora `mix-blend-mode`, avatar appare su rettangolo nero pieno. Confirmed bug noto Remotion, no workaround disponibile in v4.x.

**Soluzione adottata (light bg gradient biancoâ†’mist):**

L'alone scrivania residuo del matting AI HeyGen (~5-10% intorno al busto) si fonde **invisibile** col bg chiaro perchÃ© ha luminanza simile. Risultato visivo: avatar pulito su gradient brand-coerente, zero artefatti percepibili.

**Trade-off accettato:** identitÃ  visuale "bianco/chiaro" (non "scuro/cinematic"). Per esigenze dark-bg future â†’ necessario re-shoot avatar HeyGen con sfondo studio scuro nativo (non disponibile in stock photo_avatar), o pivot a Remotion-only tipografico.

### Step 4 â€” Layout parametrizzato (constanti in alto al file)

```typescript
// === LAYOUT CONSTANTS (modificabili per future skill iterations) ===
const AVATAR_RIGHT_OFFSET = -400;  // px â€” sposta avatar a destra fuori frame parziale (50% busto visibile)
const TEXT_AREA_WIDTH = 1100;       // px â€” larghezza area kinetic typography sinistra
const AVATAR_SCALE = 1.0;           // moltiplicatore scala avatar (default 1.0 = no scale)
const BRAND_OVERLAY_OPACITY = 1.0;  // logo + accent bar
const ACCENT_BAR_WIDTH = 8;         // px â€” barra verticale Teal 500 left edge
// === FINE LAYOUT CONSTANTS ===
```

**Razionale:** PoC v9 ha codificato questi valori dopo stress test. Tenerli in alto al file Composite.tsx li rende **modificabili in 1 punto** quando un futuro brief richiederÃ  aspect ratio o framing diversi (es. portrait 9:16 per Reel â†’ cambierÃ  AVATAR_RIGHT_OFFSET e TEXT_AREA_WIDTH).

**Eventuale evoluzione futura:** estrarre in `config/composite-layout.json` per skill `visual/video-composite-explainer-v2` (v1.2 plugin).

---

## 4. 9 lessons learned dal PoC convergenza v1 â†’ v9

Codificate per evitare di rifare gli stessi errori in produzione:

| # | Versione PoC | Approccio | Esito | Lesson learned |
|---|---|---|---|---|
| 1 | v1 â€” no filter | Webm HeyGen senza alpha + bg nero | âŒ avatar su rettangolo nero | HeyGen default webm NON ha alpha. Serve `outputFormat=webm` esplicito |
| 2 | v2 â€” chromakey SVG aggressive | feColorMatrix matrix forte | âŒ chiazze bianche su giacca/capelli | Chromakey su pixel space NON sa distinguere bg dagli elementi scuri legittimi |
| 3 | v3 â€” chromakey SVG conservative | feColorMatrix matrix soft | âŒ pattern bianco residuo | Soglia chromakey impossibile da calibrare in modo robusto |
| 4 | v4 â€” ffmpeg colorkey + transparent | Pre-process ffmpeg | âŒ pattern bianco persiste | Colorkey pixel space stesso problema del SVG |
| 5 | v5 â€” ffmpeg lumakey BT.601 | Lumakey su luma channel | âŒ uccide pixel interni scuri | Lumakey impossibile distinguere bg da capelli/ombre |
| 6 | v6 â€” dark bg Navy 800 + mix-blend-mode lighten | Vox/Wendover style | âŒ Remotion ignora blend mode | Remotion headless Chromium NON rispetta `mix-blend-mode` su `OffthreadVideo` |
| 7 | v7 â€” `outputFormat=webm` HeyGen | Matting AI all'origine | âœ… alpha VP9 nativo finalmente! | Il parametro API corretto era nascosto nello schema HeyGen: `outputFormat=webm` per photo_avatar |
| 8 | v8 â€” light bg + transparent | Gradient biancoâ†’mist | âœ… "Perfetta!!! alone scrivania accettabile" | Light bg fonde invisibile l'alone residuo del matting AI |
| 9 | v9 â€” layout parametrizzato | Constanti in alto al file | âœ… "Perfetta!!!" â€” definitivo | Parametrizzazione layout = invariante per avatar/outfit/look futuri |

**Conclusione strategica:** la qualitÃ  del composite **dipende dal matting al source** (HeyGen `outputFormat=webm`), NON da post-processing nel renderer. Qualunque chromakey/lumakey/blend mode post-hoc Ã¨ destinato a fallire su avatar generici con illuminazione complessa.

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief composite** dal chiamante: script HeyGen + 4-8 cue testuali kinetic + pillar + voce avatar + durata target + formato (1920Ã—1080 o 1080Ã—1920)
2. **Eseguire kickoff** per contesto workspace
3. **Verifica quota mensile** HeyGen residua (lookup `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md`)
4. **Lookup avatar/voce** per pillar (vedi `config/heygen.json` mapping pillarâ†’avatar)
5. **Verifica script per durata**: stima tempo (~130-150 parole/min parlato) â†’ se sfora budget mensile residuo, segnala MM
6. **Invocare HeyGen MCP** via Task tool con parametro `outputFormat: "webm"`:
   ```
   Task(
     subagent_type: "mcp__heygen__create_video_from_avatar",
     prompt: "Genera video avatar con: avatar_id [X], voice_id [Y], input_text [script], outputFormat 'webm', dimension 1920Ã—1080."
   )
   ```
7. **Polling stato job HeyGen** fino a `status: completed` (~8-15 min)
8. **Download file .webm** in `Output_approvati/[file]_assets/avatar_[name]_alpha.webm` via Bash (curl)
9. **Comporre file `Composite.tsx`** da template con constanti layout in alto al file + cue testuali kinetic ricevuti dal chiamante:
   ```bash
   cp scripts/video/Composite.template.tsx Output_approvati/[file]_assets/Composite.tsx
   # sed-replace dei placeholder con script/cues/avatar_path
   ```
10. **Render Remotion** in locale via Bash (ModalitÃ  A weekly batch):
    ```bash
    # ModalitÃ  immediate (debug):
    cd /sessions/.../mnt/dev-remotion && npx remotion render src/Composite.tsx CompositeMain out/composite_[id].mp4

    # ModalitÃ  A weekly batch (production):
    # Generare entry in /05_Calendario_editoriale/Render_queue/[YYYY-MM]_batch.json
    # Lo script PowerShell run-render-batch.ps1 (lanciato dal CEO) consuma la queue venerdÃ¬ sera o sabato mattina
    ```
11. **Verifica integritÃ  file MP4** (dimensioni > 0, durata coerente con target)
12. **Invocare `compliance-ai-disclosure` tipologia A** via Task tool per generare caption disclosure + on-screen sigla
13. **Loggare** in `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md` con: data, durata, costo minuti consumati, quota residua, esito, modalitÃ  render
14. **Restituire metadata + path MP4 + path webm + path Composite.tsx** al chiamante + AI disclosure pacchetto

---

## 6. ModalitÃ  A weekly batch â€” workflow dettagliato

Pattern operativo standard post-go-live (decisione runtime 2026-05-19, in attesa di ModalitÃ  D Remotion Lambda cloud render v1.2):

### Workflow

1. **LunedÃ¬-GiovedÃ¬:** skill `visual/video-composite-explainer` accumula job in `/05_Calendario_editoriale/Render_queue/[YYYY-MM]_batch.json` (un job = avatar webm pronto + Composite.tsx pronto, manca solo render finale MP4)
2. **Friday email** (venerdÃ¬ 18:00) include sezione "Render queue" con elenco job pendenti + tempo render stimato totale (es. "4 video composite, ~25 min totale, PC acceso sabato 09:00-09:30")
3. **Sabato mattina (o orario scelto CEO):** CEO esegue il batch:
   ```powershell
   # Da Esplora Risorse, doppio click su:
   C:\dev-remotion\run-render-batch.ps1
   # Oppure da PowerShell:
   cd C:\dev-remotion
   .\run-render-batch.ps1
   ```
4. Lo script:
   - Legge `Render_queue/[YYYY-MM]_batch.json`
   - Itera ogni job, renderizza con `npx remotion render`
   - Salva MP4 in path target del job
   - Aggiorna log job: stato `rendered`, timestamp, dimensione file
   - A fine batch: notifica completion via cmd output + opzionale email
5. **MM lunedÃ¬ mattina:** verifica log batch, pubblica i video composite via `publish/scheduling` orchestrator

### Vantaggi ModalitÃ  A

- CEO ~30 min/sett impegno fisico (PC acceso, click script)
- Costo elettricitÃ  trascurabile
- Render in locale = privacy massima (asset non lasciano il computer)
- Compatibile con setup attuale (Node v24.15.0 + Remotion 4.x + ffmpeg)
- Zero costi cloud aggiuntivi

### Limiti ModalitÃ  A

- CEO dipendenza fisica: se CEO in ferie senza PC â†’ job in coda fino al rientro
- PC CEO impegnato 25-40 min Ã— N video durante render (non bloccante per altre attivitÃ  se >8GB RAM)
- Throughput max ~8-12 video composite/settimana

### Path di evoluzione

- **ModalitÃ  D (v1.2 autunno 2026):** Remotion Lambda cloud render. Costo ~$0.01-0.05/min video Ã— ~10 video/sett = ~â‚¬5-15/mese. Throughput illimitato, zero CEO touch. Da quotare con utilizzo reale dei primi 3 mesi go-live.

---

## 7. Casi particolari

### Quota HeyGen mensile esaurita (15 min Creator tier)

- ðŸ”´ blocco generazione webm avatar
- Notifica MM: "Quota HeyGen 15 min/mese esaurita. Suggerimenti: (a) rinvio video composite al mese prossimo, (b) passa a Remotion-only tipografico (visual-video-remotion), (c) richiedi upgrade Team $72/mese 30 min."
- Job esistenti giÃ  con webm in `_assets/` possono comunque essere renderizzati (la quota Ã¨ solo per generazione avatar, non per render Remotion locale)

### Avatar HeyGen pillar non disponibile in stock

- ðŸ”´ blocco
- Suggerimento: "Avatar default per pillar [X] non piÃ¹ disponibile in HeyGen stock. Verifica dashboard HeyGen â†’ Avatars â†’ Stock. Selezionare avatar alternativo coerente con Brand Book v1.2 sez. 14.4 (italiano-friendly etÃ  35-55 business attire). Aggiornare `config/heygen.json` mapping."

### Pillar 2 Voce CEO Daniele

- ðŸ”´ blocco hard automatico (denylist `config/heygen.json` blocca avatar Italian male ~50 e voice cloning Daniele)
- Suggerimento: "Pillar 2 Voce CEO = Daniele in persona obbligatorio (Brand Book v1.2 sez. 14.4). Per video composite, registrazione audio Daniele autentica + Remotion-only tipografico. Skill alternativa: `visual/video-remotion`."

### Aspect ratio diverso da landscape 1920Ã—1080

- Per Short/Reel 1080Ã—1920: aggiornare constanti layout
  - `AVATAR_RIGHT_OFFSET = -200` (avatar piÃ¹ centrato in portrait)
  - `TEXT_AREA_WIDTH = 900` (testo sopra l'avatar)
  - Rivedere posizionamento logo + accent bar per portrait
- Stress test obbligatorio prima di pubblicare (un solo render PoC con avatar nuovo)

### Sottotitoli burned-in

- **Obbligatori per pubblicazione social** (80% pubblico no-audio)
- Generati lato Remotion da array di cue text + timing (NON sottotitoli HeyGen auto-generati, che sono separati dal video)
- Font: Inter Tight Bold 600, posizione bassa centrale, contrast forte (Ink #0F1A38 con outline Paper #FFFFFF 2px)
- Correzione manuale obbligatoria su tecnicismi assicurativi italiani (handoff a MM/Copywriter)

### Validazione pre-produzione (dry-run)

- ModalitÃ  `--dry-run`: skill restituisce solo il brief HeyGen composto + Composite.tsx skeleton senza eseguire MCP call nÃ© render
- Utile per MM/CEO che vogliono validare avatar + voce + script prima di consumare quota mensile

---

## 8. Cosa NON fare mai

- âŒ **Chromakey/colorkey/lumakey post-hoc** su pixel space (PoC v2-v5 falliti â€” uccide pixel interni avatar)
- âŒ **Dark bg + `mix-blend-mode: lighten`** (PoC v6 fallito â€” Remotion headless ignora blend mode)
- âŒ **`removeBackground=true`** URL flag su photo_avatar HeyGen (Ã¨ per video_avatar trainati, fallibile)
- âŒ **`<Video>`** invece di `<OffthreadVideo>` su asset con alpha (Remotion default non rispetta alpha)
- âŒ **Avatar clone Daniele/soci** (denylist hard `config/heygen.json` + Brand Book v1.2 sez. 14.4)
- âŒ **Voice cloning Daniele** (vietato definitivo)
- âŒ **Doppiaggio AI di audio autentico Daniele** in altra lingua (vietato Brand Book v1.2 sez. 14.4)
- âŒ **Saltare AI disclosure** (avatar visibile in scena = AI Act UE art. 50 obbligatorio)
- âŒ **Saltare sottotitoli burned-in** per pubblicazione social
- âŒ **Sforare quota HeyGen mensile** senza notifica MM
- âŒ **Modificare constanti layout senza stress test** (almeno 1 PoC render prima di mettere in produzione)
- âŒ **Saltare log** in `Log_visual_generati/[YYYY-MM]_heygen.md`

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 14 stack video + ETICA AI definitiva + sez. 8 Design System palette/font)
2. `/01_Team/09_Content_Producer.md` Â· `/01_Team/05_Art_Director.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (vincoli avatar + AI Act UE)
4. `config/heygen.json` (mapping pillar â†’ avatar default + denylist clone)
5. `config/design-system.json` (palette + font + scala)
6. `config/budget.json` (cap mensile HeyGen 15 min Creator)
7. `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md` (quota residua)
8. `docs/SETUP_HEYGEN.md` (sezione "Avatar matting & transparency" â€” outputFormat=webm vs removeBackground)
9. Il brief composite del chiamante

---

## 10. Riferimenti tecnici esterni

- **Remotion docs OffthreadVideo + transparent:** https://www.remotion.dev/docs/offthreadvideo
- **HeyGen API docs `outputFormat` (Schema create_video_from_avatar):** schema MCP ufficiale `mcp__heygen__create_video_from_avatar`
- **PoC sorgenti canonical archiviati:** `/99_Archivio/Test_runtime/remotion_composite/src/Composite.tsx`
- **PoC asset webm validati:** `C:\dev-remotion\public\avatar_gina_true_alpha.webm` + `avatar_gino_grey_alpha.webm` + `avatar_gina_black_alpha.webm`

---

*SKILL v1.0 â€” advisory-plus:visual-video-composite-explainer â€” Sessione 14 Plugin Build v1.1.2 housekeeping â€” 2026-05-19*
*Pipeline canonical validata empiricamente PoC 2026-05-19 sera (9 iterazioni convergenza Â· CEO "Perfetta!!!" su render v9)*

