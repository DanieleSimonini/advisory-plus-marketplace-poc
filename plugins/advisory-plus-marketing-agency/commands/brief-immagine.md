---
name: brief-immagine
description: Genera un brief pronto-uso per cc-nano-banana (Gemini 2.5 Flash Image) coordinato con Design System v1.0 Advisory+. Prompt completo + parametri tecnici + variante quadrata/orizzontale/verticale. Usalo quando ti serve un visual coordinato senza ragionarci su.
argument-hint: [tema in italiano] [opzionale: pillar | formato (post|reel|story|blog-cover|youtube-thumb)]
---

# /brief-immagine — Brief nano-banana coordinato Design System v1.0

Quando vieni invocato con `/brief-immagine $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. Sei l'**Art Director Advisory+** per questo task.

## Step 1 — Parse argomenti

`$ARGUMENTS` può contenere:
- **Tema** (obbligatorio): descrizione del contenuto in italiano, es. "TCM famiglia protetta", "LTC RSA Camaiore"
- **Pillar** (opzionale): `pillar=P1|P2|P3|P4|P5` — se omesso, inferiscilo dal tema (vedi mapping in /spunto Step 3)
- **Formato** (opzionale): `formato=post|reel|story|blog-cover|youtube-thumb` — default `post` (quadrato 1080×1080)

Se tema mancante:

```
❌ Tema mancante.

Sintassi:
/brief-immagine [tema] [opzionale: pillar=P1-5] [formato=post|reel|story|blog-cover|youtube-thumb]

Esempi:
/brief-immagine TCM famiglia protetta
/brief-immagine LTC RSA Camaiore formato=blog-cover
/brief-immagine Tutela legale famiglia pillar=P4 formato=reel
```

## Step 2 — Carica Design System v1.0

Leggi (se non già in cascata di contesto):

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\04_Risorse\Brand_Visual\Design_System_v1.html
```

E Brand Book sez. 8 in:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\00_Brand_Book_v1.1.md
```

Se i file non sono disponibili, usa questi parametri di fallback (memorizzati dal Brand Book v1.1 sez. 8):

```
COLORI (esadecimali per nano-banana):
- Primario navy 700:  #001660
- Background scuro:   #011750
- Accent unico teal:  #2DD4C5
- Testo ink:          #0F1A38
- Surface mist:       #F2F4F9

FONT (open source):
- Heading/UI/Body: Inter Tight
- Citazioni edit.: Source Serif 4
- Dati/Mono:       JetBrains Mono

STILE FOTOGRAFICO:
- Volti italiani realistici, no stereotipi
- Luce naturale, ambientazioni domestiche/professionali italiane
- Composizione minimalista, ampio spazio negativo
- NO emoji nelle immagini, NO testo all-caps inglese
- NO loghi compagnie mandatarie nelle immagini (compliance)
```

## Step 3 — Mappa formato → dimensioni

| Formato | Dimensioni px | Aspect ratio | Uso |
|---|---|---|---|
| `post` (default) | 1080 × 1080 | 1:1 | Instagram/Facebook/LinkedIn quadrato |
| `reel` | 1080 × 1920 | 9:16 | Reel IG, TikTok, YouTube Short |
| `story` | 1080 × 1920 | 9:16 | IG/FB Stories |
| `blog-cover` | 1920 × 1080 | 16:9 | Copertina articolo blog THE ADVISOR |
| `youtube-thumb` | 1280 × 720 | 16:9 | Thumbnail video YouTube |

## Step 4 — Inferisci moodboard per pillar

Mapping pillar → mood visual:

| Pillar | Tono visivo | Soggetti tipici | Palette dominante |
|---|---|---|---|
| P1 La famiglia che protegge | Caldo, sicuro, intimo | Famiglia giovane, mani, abbraccio, casa | Navy + accent teal + warm light |
| P2 Il dopo di noi, il dopo di loro | Sereno, dignità, generazionale | Anziano + figlio adulto, mani strette, finestra | Navy + soft teal + warm gray |
| P3 Risparmio sensato | Pulito, equilibrato, futuro | Salvadanaio, grafico ascendente sobrio, tazza caffè | Navy + accent teal + cream |
| P4 Tutela legale invisibile | Discreto, scudo, sicurezza | Ombrello, ponte, mano protettiva, contratto | Navy + accent teal + cool gray |
| P5 Territorio Advisory+ | Versilia, mare, comunità | Costa toscana, sede ufficio, team al lavoro | Navy + accent teal + sea blue |

## Step 5 — Genera il prompt nano-banana

Costruisci un prompt in **inglese** (cc-nano-banana / Gemini 2.5 Flash Image lavora meglio in inglese) che includa:

1. **Subject + scene** (1 frase)
2. **Composition** (regola dei terzi, spazio negativo, focal point)
3. **Lighting** (luce naturale, ora del giorno, mood)
4. **Color palette** (3 colori espliciti hex dal Design System)
5. **Style references** (es. "editorial photography, Magnum-style, Italian lifestyle, premium")
6. **Negative prompt** (cose da evitare: testo, loghi, watermark, volti deformati)
7. **Aspect ratio** (esplicito)

## Step 6 — Output

Mostra esattamente questo blocco:

```
═══════════════════════════════════════════════════
🎨 BRIEF IMMAGINE · Advisory+
Tema: [tema italiano]
Pillar: [P1-5 nome esteso]
Formato: [formato] · Dimensioni: [WxH] px · Aspect: [ratio]
═══════════════════════════════════════════════════

📝 PROMPT NANO-BANANA (copia-incolla in cc-nano-banana o Gemini Flash Image)

```
[prompt completo in inglese, 4-8 righe]
Style: [style references]
Color palette: [3 hex codes]
Negative prompt: [cose da evitare]
Aspect ratio: [ratio]
Output size: [WxH] px
```

🎨 PARAMETRI TECNICI

Colori dominanti: [hex 1] · [hex 2] · [hex 3]
Font overlay (se applicabile): Inter Tight Bold per heading, Inter Tight Regular per body
Loghi: Logo Advisory+ in [bianco|colori] da 04_Risorse/Loghi/, posizione [angolo basso destra | top center]

📐 VARIANTI ALTERNATIVE (genera anche queste se serve riadattare)

Variante quadrata 1080×1080 (post): [prompt adattato 1 riga]
Variante verticale 1080×1920 (reel/story): [prompt adattato 1 riga]
Variante orizzontale 1920×1080 (blog/YouTube): [prompt adattato 1 riga]

═══════════════════════════════════════════════════
COMPLIANCE: il brief NON include loghi di compagnie mandatarie nelle immagini né claim su prodotto. Disclaimer RUI separato (non in immagine, in caption).
═══════════════════════════════════════════════════
```

## Vincoli di stile

- **Prompt nano-banana in INGLESE** (modello performa meglio)
- **Mai stereotipi**: no famiglia bianca standardizzata, no anziano triste solo
- **Mai testo inglese sull'immagine** se è per pubblico IT
- **NO loghi compagnie mandatarie** nelle immagini (compliance)
- **NO firme/watermark** AI generation visibili
- **NO uso di tool Skill** — self-contained

## Edge case

- Se Design System file non leggibile → usa fallback in Step 2 (parametri memorizzati)
- Se pillar non inferibile → chiedi 1 sola volta "Pillar P1-P5?" e fermati in attesa (eccezione al fire-and-forget)
- Se tema è esplicitamente promo prodotto specifico (es. "TCM Famiglia Sicura promo lancio") → aggiungi alert: "🟡 questo brief promo richiede review Compliance Officer prima di generare l'immagine: lancia /compliance-check su caption associata"

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained.*
