---
name: content-reel-script
description: Compone uno script Reel (Instagram + Facebook Reels cross-post nativo Meta) pronto per produzione video 30-60 sec. Orchestra: voce editoriale (Spiegato Facile prevalente per Reel didattici Â· Badvisor con TETTO 20% mese per Reel di rottura/punch Â· Caso Reale per snippet narrativi brevi Â· Analisi rara â€” solo se dato visualizzabile in 30 sec) â†’ invoca voce-* via Task tool con vincolo "video micro-script con hook in 3 sec" â†’ riceve script asciutto â†’ applica struttura Reel (hook 0-3s vincolo algoritmico IG/Reels, sviluppo 3-45s, CTA 45-60s) â†’ genera storyboard 4-5 scene 1080Ã—1920 + caption Reel 100-150p + hashtag 8-10 â†’ produce sottotitoli burned-in OBBLIGATORI (80% pubblico IG guarda senza audio) â†’ handoff a skill visual Sessione 4 per produzione (Remotion per Reel tipografici/motion graphics OR HeyGen per Reel con avatar parlante generico, MAI clone Daniele) â†’ Compliance gate â†’ consegna al MM pacchetto script + storyboard + caption Reel + brief produzione.
---
# ðŸŽ¬ Skill content-reel-script â€” Script Reel Instagram + Facebook

> **Video 30-60 sec. Hook in 3 secondi obbligatorio. Sottotitoli burned-in. Voce Badvisor con tetto. Stack 5 motori: Remotion tipografico o HeyGen avatar generico.**

---

## 1. Quando triggera

- Invocata dal MM per slot Reel del piano settimanale (frequenza standard: 1-2/sett su IG, cross-post nativo FB)
- Invocata per Reel reattivi a tema caldo (max 48h dall'evento)
- Invocata da skill `month-plan` quando pipeline ATL flagga Reel da produrre 7gg prima della pubblicazione (per video con HeyGen avatar che richiedono produzione esterna)
- Mai auto-trigger

Tempo target di esecuzione: **10-15 minuti** (script + storyboard, escluso rendering video che Ã¨ fase separata Sessione 4).

---

## 2. Output finale atteso

**Pacchetto script + storyboard + caption + brief produzione** consegnato al MM:

```markdown
---
canale: [instagram_reel + facebook_reel_crosspost]
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. mer 19:00, ven 12:00 â€” finestre IG engagement]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Badvisor / Caso Reale / Analisi]
durata: [30s / 45s / 60s]
formato_video: 1080Ã—1920 verticale
motore_produzione: [Remotion_tipografico / HeyGen_avatar_generico]
firma: brand Advisory+
visual_brief: brief_reel_[id].md (storyboard + handoff produzione)
caption_reel: [100-150p Â· primo paragrafo â‰¤150 char]
hashtag: 8-10 (mix tematici, NO localitÃ )
sottotitoli_burned_in: OBBLIGATORI (80% pubblico no-audio)
quota_mensile_badvisor: [X% â€” tetto hard 20%]
ai_disclosure: [richiesta solo se HeyGen avatar usato â€” vedi sez. 5]
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

# SCRIPT CON TIMING

## HOOK (0-3 secondi) â­ CRITICO â€” il 70% del successo Reel sta qui
**Voce off / on-screen text:**
[Frase di 5-10 parole MAX Â· paradosso o domanda scomoda o apertura narrativa o tesi pungente]

**Visual scene 1:**
[Descrizione cosa si vede on-screen nei primi 3 sec Â· deve fermare il pollice del lettore mid-scroll]

## SVILUPPO (3-45 secondi)
**Voce off / on-screen text:**
[Corpo del messaggio Â· 1 sola idea Â· 60-120 parole script totali per 30-45 sec di parlato]

**Visual scenes 2-4:**
[Descrizione cosa si vede on-screen per ogni cambio di scena Â· transizioni tipo "cut" o "fade" Â· max 4-5 scene totali]

## CTA (45-60 secondi)
**Voce off / on-screen text:**
[Invito 5-15 parole Â· "Link in bio" o "Scrivici un DM" o "Commenta con [emoji] se ti Ã¨ successo"]

**Visual scene finale:**
[Logo Advisory+ + tagline "Consulenza assicurativa. Sul serio." + CTA on-screen]

# STORYBOARD VISUAL â€” 4-5 SCENE 1080Ã—1920

## Scena 1 (0-3s) â€” HOOK
- Visual: [descrizione]
- Testo on-screen: [max 5-7 parole, font grande, contrast forte]
- Audio: [musica suggerita Â· voce off Daniele o brand Â· effetti sonori]

## Scena 2 (3-15s)
- Visual: [descrizione]
- Testo on-screen: [max 8-10 parole]
- Audio: [...]

## Scena 3 (15-30s)
- Visual: [descrizione]
- Testo on-screen: [max 8-10 parole]
- Audio: [...]

## Scena 4 (30-45s)
- Visual: [descrizione]
- Testo on-screen: [max 8-10 parole]
- Audio: [...]

## Scena 5 (45-60s) â€” CTA
- Visual: logo Advisory+ + tagline
- Testo on-screen: [CTA]
- Audio: [outro music]

# CAPTION REEL (post sotto al video)
[PRIMO PARAGRAFO â‰¤150 char â€” riprende il hook del video]

[Sviluppo 100-150 parole totali Â· spiega ciÃ² che il video sintetizza Â· invita a guardare con audio se possibile]

[Chiusura: "Link in bio per approfondire" o equivalente]

# HASHTAG
#AdvisoryPlus #[tema1] #[tema2] #[tema3] #[tema4] #[tema5] #[tema6] #[tema7]

# BRIEF PRODUZIONE (handoff a skill visual Sessione 4)
**Motore raccomandato:** [Remotion_tipografico / HeyGen_avatar_generico]
**Palette:** Navy 700/800 + Teal 500 + Mist + Ink (Design System v1.0)
**Font on-screen:** Inter Tight grande, bold per hook
**Sottotitoli:** burned-in obbligatori, posizione bassa centrale, contrast forte
**Logo finale:** Advisory+ + tagline
**Asset richiesti:** [musica royalty-free Â· eventuali foto stock generiche Â· NO foto persone identificabili]
**Output finale:** file MP4 1080Ã—1920 H.264, durata esatta [N]s
```

---

## 3. Specifiche Reel Instagram + Facebook

### Durata
- **30-60 secondi** sweet spot algoritmico Reel (dwell-time premiato sotto 60s)
- **30s**: Reel di rottura, Badvisor, hook potente unico
- **45s**: Reel didattico Spiegato Facile, 1 concetto sviluppato
- **60s**: Reel narrativo Caso Reale (limite max per non perdere drop-off)
- **Oltre 60s**: NO, sposta su altri formati video (vedi `content-youtube-video`)

### Hook 0-3 secondi â€” vincolo critico
- L'algoritmo IG/Reels decide nei primi 3 sec se mostrare il video a piÃ¹ persone
- Il 70% del successo Reel sta qui
- Pattern hook efficaci:
  - **Paradosso** (Badvisor): "Hai un piano per le ferie. Per tua madre quandoâ€¦"
  - **Domanda scomoda** (Badvisor): "Conosci la marca della tua macchina. Sai cosa copre la tua polizza casa?"
  - **Apertura narrativa** (Caso Reale): "Marta, 52 anni. Sua madre Ã¨ caduta in bagno."
  - **Tesi pungente** (Analisi): "ANIA 2025: il ramo vita Ã¨ crollato del 12%. Ecco perchÃ©."
  - **Domanda quotidiana** (Spiegato Facile): "Cos'Ã¨ davvero la franchigia? Te la spiego con il frigorifero rotto."
- Hook visivo + testuale in **contemporanea**: testo on-screen + visual che ferma lo scroll

### Sottotitoli burned-in
- **OBBLIGATORI** (80% del pubblico IG guarda Reel senza audio)
- Burned-in = scritti direttamente nel video, non auto-generati dalla piattaforma
- Posizione: bassa centrale (evita la zona caption che copre il fondo dello schermo)
- Contrast forte: testo bianco su fondo scuro semi-trasparente o testo bold su outline
- Font: Inter Tight bold size grande

### Stack motori di produzione
Definito Brand Book v1.2 sez. 14:

| Motore | Quando usare | Costo |
|---|---|---|
| **Remotion** (TypeScript/React) | Reel tipografici, motion graphics, animazioni dati, hook puramente visivi | Open source Â· skill `remotion-dev/skills` |
| **HeyGen avatar generico** | Reel con avatar parlante professionale (NO clone Daniele Simonini â€” decisione CEO 2026-05-16) | Piano Creator $24/mese Â· 15 min video/mese |
| **cc-nano-banana** | Static images per cover Reel o frame chiave | ~$0.04/img |

### Compliance AI disclosure su Reel con HeyGen
Se il Reel usa HeyGen avatar:
- **Disclosure AI obbligatoria in caption Reel**: "Video con avatar AI a scopo divulgativo. Daniele Simonini e i soci Advisory+ non sono rappresentati in alcun modo dall'avatar."
- **Disclosure on-screen sottile** in scena finale (es. corner basso destra "Avatar AI Â· contenuto Advisory+")
- Vedi sez. 5 per dettaglio AI Act UE

### Voce editoriale per Reel
- **Spiegato Facile** â€” primaria per Reel didattici Pillar 1, P4, P6 base, P8
- **Badvisor** (tetto 20%) â€” Reel di rottura/punch, hook potente
- **Caso Reale** â€” Reel narrativi brevi (snippet 30-60s storia)
- **Analisi** rara â€” solo se il dato si visualizza in modo forte in 30 sec (es. "ANIA 2025: -12%. Ecco perchÃ©." con grafico animato Remotion)

### Caption Reel
- **100-150 parole** (piÃ¹ breve di caption Instagram standard)
- Primo paragrafo â‰¤150 caratteri (vincolo "...altro" IG)
- 8-10 hashtag mix tematici (no localitÃ )
- CTA: "Link in bio" o "DM" o "Commenta con [emoji]"

### Orario di pubblicazione raccomandato
- **Mer-Gio-Ven**: 19:00-21:00 (sera peak Reel)
- **Sab-Dom**: 11:00-13:00

---

## 4. Tetto Badvisor 20% â€” verifica obbligatoria pre-invocazione

Come per altre skill di voce: verifica quota Badvisor cumulata mese (tutti i canali) prima di invocare voce Badvisor su Reel. Se â‰¥20% â†’ bloccare e proporre Spiegato Facile o Caso Reale.

I Reel Badvisor sono particolarmente d'impatto (formato premia provocazione) ma proprio per questo vanno dosati.

---

## 5. AI disclosure su Reel con HeyGen avatar â€” AI Act UE artt. 50, 52

Brand Book v1.2 sez. 14.4 + decisione CEO 2026-05-16: **MAI clone Daniele Simonini nÃ© di altri soci con HeyGen**. Solo **avatar generico professionale**.

Disclosure framework semplificato applicato:

### In caption Reel (obbligatoria)
Formula raccomandata (validazione finale con consulente privacy/legale esterno â€” pendenza pre-go-live):
> *Video con avatar AI a scopo divulgativo. Daniele Simonini e i soci Advisory+ non sono rappresentati in alcun modo dall'avatar.*

### On-screen sottile (raccomandata, conferma Art Director)
Corner basso destra, sigla compatta:
> *Avatar AI Â· Advisory+*

### Quando NON serve disclosure
- Reel **tipografici Remotion** (no avatar, solo motion graphics + voce off Daniele autentica o brand voice neutra)
- Reel con **voce off umana autentica** (Daniele o operatore brand)

### Quando serve disclosure raddoppiata (Compliance + revisione consulente esterno)
- Reel con voce avatar AI parlante che simula Daniele (VIETATO â€” non produrre nemmeno)
- Reel con doppiaggio AI di Daniele (VIETATO definitivo â€” Brand Book v1.2 sez. 14)
- Reel con avatar AI che fa affermazioni su prodotti specifici (richiede doppia revisione Compliance)

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (pillar, voce, tema, durata target 30/45/60s, eventuale ancoraggio, motore preferito Remotion/HeyGen)
2. **Eseguire kickoff**
3. **Se voce Badvisor**: verifica quota 20% mese
4. **Invocare voce editoriale** via Task tool con brief Reel micro-script:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale Reel IG+FB Â· durata [N]s (~150-200 parole script max per 60s di parlato) Â· hook OBBLIGATORIO in 5-10 parole nei primi 3 sec Â· struttura hookâ†’sviluppoâ†’CTA Â· 1 sola variante (Reel Ã¨ formato unico)."
   )
   ```
5. **Ricevere** script asciutto
6. **Strutturare script con timing** (hook 0-3s Â· sviluppo 3-45s Â· CTA 45-60s)
7. **Generare storyboard** 4-5 scene 1080Ã—1920 con descrizione visual + testo on-screen + audio
8. **Comporre caption Reel** 100-150p (primo paragrafo â‰¤150 char) + hashtag 8-10
9. **Determinare motore produzione**:
   - Default Remotion tipografico
   - HeyGen avatar generico solo se brief MM lo richiede esplicitamente (e disclosure AI sarÃ  obbligatoria)
10. **Produrre brief produzione** per skill visual Sessione 4 (palette, font, sottotitoli burned-in, asset richiesti, output MP4 specifiche)
11. **Se HeyGen avatar**: aggiungere disclosure AI in caption + brief on-screen disclosure
12. **Invocare Compliance Officer** via Task tool (attenzione: claim, voce dosaggio, disclosure AI se HeyGen, no clone Daniele, sottotitoli accuratezza)
13. **Se ðŸŸ¡/ðŸ”´**: riformulazione, ri-check
14. **Se ðŸŸ¢**: consegna al MM pacchetto completo

---

## 7. Casi particolari

### Reel reattivo a evento di settore (sentenza/normativa)
- Voce Analisi visualizzata (dato + grafico animato Remotion)
- Tempistica 24-48h dall'evento
- Apparato citazionale comprimibile in caption Reel (fonte+anno inline)

### Reel Caso Reale narrativo
- Durata massima 60s (Caso Reale ha bisogno di respiro narrativo)
- Visual: foto stock generiche + testo on-screen ricostruttivo
- Disclaimer "Caso reale, nomi di fantasia" ridotto on-screen in scena finale
- Mai foto persone identificabili

### Reel Pillar 2 Voce CEO (Daniele)
- Voce off **autentica Daniele** (registrazione audio reale, mai HeyGen/AI doppiaggio)
- Visual: avatar generico HeyGen VIETATO (Ã¨ voce personale Daniele, deve restare autentica)
- Alternativa: Reel tipografico Remotion con voce off Daniele autentica
- Pubblicazione semi-manuale (Daniele rilegge/riascolta e clicca personalmente)

### Reel teaser di articolo blog appena pubblicato
- Visual cover articolo + 3 punti chiave on-screen
- CTA "Link in bio per leggere completo"
- 30-45 sec sufficienti

### Reel di sequenza tematica (es. "5 cose che non sai su LTC" â€” 1 Reel per cosa, 5 Reel in 5 settimane)
- Hashtag serie dedicato per ritrovabilitÃ 
- Caption con "Puntata X/5"
- Visual coordinato (template ripetibile Remotion)

---

## 8. Cosa NON fare mai

- âŒ **Reel sopra 60 secondi** (drop-off pesante, sposta su YouTube)
- âŒ **Hook in 3 secondi assente o debole** (algoritmo non spinge il video)
- âŒ **Sottotitoli auto-generati** invece di burned-in (80% pubblico no-audio)
- âŒ **Avatar HeyGen clone Daniele Simonini** o altri soci (decisione CEO 2026-05-16 etica definitivo)
- âŒ **Doppiaggio AI voce Daniele** (Brand Book v1.2 sez. 14 vietato definitivo)
- âŒ **Disclosure AI omessa** quando HeyGen avatar Ã¨ usato (AI Act UE rischio)
- âŒ **Sforare tetto Badvisor 20% mese**
- âŒ **Riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- âŒ **Foto persone identificabili** senza consenso
- âŒ **Music coperta da copyright** (solo royalty-free, da libreria sicura)
- âŒ **Hashtag oltre 10** o sotto 8 in caption Reel
- âŒ **Primo paragrafo caption Reel >150 char** (troncamento "...altro")
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Reel commerciale aggressivo** ("Compra ora!", "Offerta scade!")
- âŒ **Loghi mandatarie** on-screen nel Reel (solo se disclosure brand corporate, raro in Reel)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance Â· sez. 8 Design System Â· sez. 14 stack video + ETICA AI no clone Daniele)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/02_Copywriter.md` Â· `/01_Team/09_Content_Producer.md` Â· `/01_Team/03_Social_Media_Manager.md` Â· `/01_Team/05_Art_Director.md`
3. `config/brand.json` (mapping voce-canale, dosaggio Badvisor 20%, denominazione mandatarie)
4. `config/design-system.json` (palette, font, formati video)
5. `config/pillars-of-month.json`
6. `/05_Calendario_editoriale/[YYYY-MM]_*.md` (verifica quota Badvisor cumulato mese)
7. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-reel-script â€” Sessione 3 Plugin Build â€” 2026-05-18*

