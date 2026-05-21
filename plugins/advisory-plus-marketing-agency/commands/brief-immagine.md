---
name: brief-immagine
description: Genera un brief pronto-uso per cc-nano-banana (Gemini 2.5 Flash Image) coordinato con Design System v1.0 Advisory+. Prompt completo + parametri tecnici + variante quadrata/orizzontale/verticale. Usalo quando ti serve un visual coordinato senza ragionarci su.
argument-hint: [tema in italiano] [opzionale: pillar | formato (post|reel|story|blog-cover|youtube-thumb)]
---

# /brief-immagine — Brief cc-nano-banana coordinato Design System

## Cosa fa

Costruisce un **prompt completo e validato** per la skill `cc-nano-banana` (Gemini 2.5 Flash Image API key `NANOBANANA_GEMINI_API_KEY`), garantendo:

- **Palette Design System v1.0** (Navy 700 `#001660` · Navy 800 `#011750` · Teal 500 `#2DD4C5` · Mist `#F2F4F9` · Ink `#0F1A38`)
- **Font lock**: solo Inter Tight / Source Serif 4 / JetBrains Mono (mai altre)
- **Dimensione canale-specifica**
- **Tono visivo** coerente con voce editoriale (Spiegato Facile = pulito · Badvisor = ironico · Caso Reale = umano · Analisi = data-driven)
- **No volti reali** (compliance + ethics)
- **No loghi compagnie** (compliance — non possiamo mostrare logo Generali su nostro materiale)
- **Sempre disclaimer RUI** dove canale lo consente

## Sintassi

```
/brief-immagine LTC famiglia
/brief-immagine "il dopo di noi" Famiglia reel
/brief-immagine tutela legale lavoro post
/brief-immagine versilia broker territorio blog-cover
```

Argument hint:
- **tema**: 2-6 parole italiano
- **pillar** (opzionale): match con uno dei 12 pillar Brand Book sez. 6+6bis. Se omesso, MM infers.
- **formato** (opzionale): default `post` (1080x1080)

## Skill innescata

`skills/process/visual/brief-image/SKILL.md` → genera il prompt → passa a `skills/dependencies/cc-nano-banana/run/SKILL.md` che chiama Gemini.

## Output

```
🎨 BRIEF IMMAGINE — LTC famiglia (post 1080x1080)
─────────────────────────────────

PILLAR: Il dopo di noi, il dopo di loro
VOCE VISIVA: Spiegato Facile (pulito · sereno · didattico)
CANALE: Instagram + LinkedIn post quadrato 1080x1080

PROMPT cc-nano-banana (pronto da incollare):
"""
Editorial illustration, flat vector style, soft geometric shapes.
Composition: An elderly mother (silhouette only, no face features) sitting in armchair, with adult daughter (silhouette only) standing behind, hand resting on shoulder. Soft warm light from window left.
Palette strict: Navy 700 #001660 dominant background, Navy 800 #011750 furniture, Teal 500 #2DD4C5 single accent on a small detail (flowers, blanket), Mist #F2F4F9 light areas, Ink #0F1A38 outlines.
NO faces visible, NO logos, NO text inside image.
Aspect ratio 1:1, 1080x1080px, clean negative space top-right 25% for text overlay.
Mood: serene, dignified, generational warmth.
Style references: editorial illustrations of Aatish Bhatia, but more minimal.
"""

PARAMETRI cc-nano-banana:
- model: gemini-2.5-flash-image-preview
- aspect_ratio: "1:1"
- output_size: 1080x1080
- safety: standard
- variations: 3 (per A/B + 1 backup)

OVERLAY TESTO (post-generazione, da gestire skill `visual/wrapper-overlay`):
- Heading: "Il dopo di noi" (Inter Tight Bold 64pt · #F2F4F9)
- Subheading: "Long Term Care, prima che diventi un'urgenza" (Inter Tight Regular 28pt · #2DD4C5)
- Footer: "Advisory+ · RUI A000669271" (JetBrains Mono 14pt · #F2F4F9 60% opacity)

COMPLIANCE:
🟢 No volti reali · No logo · Tono dignitoso · Disclaimer RUI presente
```

## Comportamento

- **Mai inventare claim numerici** nell'image (no "il 70% delle famiglie..." senza dato verificato)
- **Mai usare stock people photography**: solo illustrazioni vector flat o silhouette
- **Mai font diversi** dai 3 ammessi (lock duro)
- **Sempre 1 accent Teal**, mai dominante
- **Disclaimer RUI** dimensione minima leggibile mobile (12pt+)

## Formati supportati

| Formato | Dimensione | Canale |
|---|---|---|
| `post` | 1080x1080 | IG + LinkedIn + FB |
| `reel` | 1080x1920 | IG Reel + Stories |
| `story` | 1080x1920 | IG/FB Stories |
| `blog-cover` | 1600x900 | THE ADVISOR header |
| `youtube-thumb` | 1280x720 | YouTube thumbnail |
| `carousel` | 1080x1080 (multi) | IG/LinkedIn carousel (1-10 slide) |

## Pillar style guide (rapido)

| Pillar | Voce visiva | Elementi |
|---|---|---|
| Famiglia che protegge | Sereno · caldo · silhouette generazionali | Casa · mani · finestre · luce naturale |
| Dopo di noi (LTC) | Dignitoso · genealogico · senza pietismo | Generazioni · oggetti tramandati · scale del tempo |
| Risparmio sensato | Misurato · matematico · pulito | Geometrie · grafici stilizzati · monete vector |
| Tutela legale | Strutturale · architettonico · stabilità | Pilastri · bilance · porte · scudi minimali |
| Territorio (rimosso da v1.2) | — | (n/a) |
| Analisi | Data-driven · grafici · numeri | Bar chart · line chart · annotations JetBrains Mono |

## Esempio fail (cosa NON deve uscire)

❌ "famiglia sorridente foto realistica" → vietato (volti reali)
❌ "logo Generali in basso a destra" → vietato (compliance)
❌ "scritta '40% di sconto'" → vietato (claim + IVASS)
❌ "stile Pixar/Disney" → no (non coerente Design System)

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
