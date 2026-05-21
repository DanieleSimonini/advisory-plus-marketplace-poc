---
name: content-stories-set
description: Compone un set di Stories Instagram/Facebook (3-5 slide consecutive) pronto da pubblicare. Orchestra: voce editoriale (qualunque voce ridotta a 5-10 parole per slide â€” Spiegato Facile didattico micro-passi, Badvisor sequenza punch ridotta con tetto 20% mese, Caso Reale snippet narrativo, Analisi micro-dato citato) â†’ invoca skill voce-* via Task tool con vincolo "stories micro-format" â†’ riceve testo essenziale â†’ applica formattazione Stories (5-10 parole per slide, sticker IG nativi poll/question/countdown/link, struttura tipo hook â†’ contenuto centrale â†’ CTA sticker link o link-in-bio fallback, visual 1080Ã—1920 per ogni slide, opzione highlight permanente) â†’ Compliance gate (NB: Stories NON portano disclaimer RUI per limiti formato, Brand Book v1.2 sez. 7) â†’ consegna al MM.
---
# ðŸ“± Skill content-stories-set â€” Set Stories Instagram + Facebook

> **Micro-format. 5-10 parole per slide. Sticker IG nativi. Sequenza 3-5 slide. Highlight opzionale.**

---

## 1. Quando triggera

- Invocata dal MM per quotidianitÃ  Stories (frequenza standard: ~28/mese, mix free-form, voci editoriali snelle)
- Invocata per accompagnare un post permanente con teaser Stories (rilancio organico)
- Invocata per Stories tematiche serie (es. 5 Stories "Cosa c'Ã¨ nella tua polizza casa?")
- Mai auto-trigger

Tempo target: **3-4 minuti** (le Stories sono il formato piÃ¹ rapido).

---

## 2. Output finale atteso

**File Markdown Stories-ready** consegnato al MM:

```markdown
---
canale: [instagram_stories | facebook_stories | entrambi (cross-post)]
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. ogni giorno fascia 09:00-11:00 o 18:00-21:00]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Badvisor / Caso Reale / Analisi]
formato: stories_set_[N]_slide
firma: brand Advisory+
visual_briefs: brief_visual_[id]_slide_1.md, ..., brief_visual_[id]_slide_N.md (1080Ã—1920)
sticker_attivi: [poll / question / countdown / link / mix]
highlight_permanente: [aggiungi a highlight "[nome]" / no]
link_in_bio_update: [URL se sticker link non disponibile]
quota_mensile_badvisor: [X% â€” tetto hard 20%]
compliance: ðŸŸ¢ / ðŸŸ¡ (NB: Stories non portano disclaimer RUI per limite formato â€” Brand Book v1.2 sez. 7)
---

# SLIDE 1 â€” HOOK (apertura)
Testo on-image: [max 5-10 parole]
Sticker: [es. poll "Hai una polizza X?" SÃŒ/NO]
Visual brief: [stile Â· palette Â· elementi]

# SLIDE 2 â€” CONTENUTO 1
Testo on-image: [max 5-10 parole]
Sticker: [es. nessuno, o emoji slider]
Visual brief: [...]

# SLIDE 3 â€” CONTENUTO 2 (opzionale)
[...]

# SLIDE 4 â€” CONTENUTO 3 (opzionale)
[...]

# SLIDE 5 â€” CTA (chiusura)
Testo on-image: [max 5-10 parole â€” es. "Scopri di piÃ¹"]
Sticker: [es. link sticker con URL Â· OPPURE "Link in bio" se sticker link non attivo sull'account]
Visual brief: [...]

# NOTE PUBBLICAZIONE
[Highlight da aggiornare: "[nome]" / pubblicazione singola]
[Cross-post FB: sÃ¬ / no]
```

---

## 3. Specifiche Stories Instagram + Facebook

### Set e sequenza
- **3-5 slide consecutive** (sotto 3 = troppo poco, sopra 5 = drop-off pesante)
- Sequenza tipo: **hook** (slide 1) â†’ **contenuto centrale 1-3** (slide 2-4) â†’ **CTA** (slide finale)
- Le Stories sono lette **una di seguito all'altra**: ogni slide deve incentivare il tap-next, non perdere il lettore

### Testo on-image
- **5-10 parole MAX per slide** (piÃ¹ tolerati su carosello stories di slide tecniche, ma resta short)
- Font grande, contrast forte (chiaro su scuro o viceversa, palette Design System)
- Mai paragrafi su Stories (errore tipico: testo affollato che nessuno legge)
- Se serve testo lungo â†’ riformula come post permanente, non come Stories

### Sticker IG nativi
- **Poll** (SÃŒ/NO o opzioni binarie): efficace per coinvolgimento â†’ "Hai una tutela legale? SÃŒ/NO"
- **Question** (domanda aperta a risposta libera): efficace per raccolta spunti â†’ "Qual Ã¨ la tua domanda assicurativa piÃ¹ frequente?"
- **Countdown** (timer evento): efficace per webinar/eventi â†’ "Countdown al webinar TCM"
- **Quiz** (multiple choice con risposta giusta): efficace per Pillar 1 Educazione â†’ "Cosa significa franchigia? A) X B) Y C) Z"
- **Emoji slider**: leggero, divertente
- **Link sticker**: solo se feature attiva sull'account (Ã¨ attiva su account business con >10K followers o sempre se account verificato); altrimenti fallback "Link in bio"

### Visual
- **1080Ã—1920 verticale** (formato Stories nativo)
- Brief visual per OGNI slide (5 brief separati per stories set di 5)
- Palette Design System (Navy 700/800 background, Teal 500 accent, Mist/Ink contrast)
- Font Inter Tight grande per testo on-image
- **Mai immagini di persone identificabili** senza consenso scritto (compliance privacy)

### Cross-post Facebook Stories
- Possibile via Meta Business Suite (toggle "Pubblica anche su Facebook" durante upload)
- Le caption/sticker sono adattati automaticamente
- **NON** Ã¨ auto-trigger della skill: il MM decide manualmente in fase di pubblicazione se cross-postare o no

### Highlight permanente
- Le Stories spariscono dopo 24h
- Opzione "Aggiungi a highlight permanente [nome]" per renderle stabili
- Highlight tipici Advisory+ (proposta â€” da finalizzare con Art Director Sessione 4):
  - "Chi siamo" (presentazione + soci)
  - "FAQ Educazione" (rispondere alle domande ricorrenti)
  - "Casi Reali" (best of Caso Reale)
  - "Pillar di stagione" (specialty attiva)
  - "Eventi" (recap webinar, fiere)
- Skill consiglia l'highlight applicabile in fase di consegna; MM decide se aggiungere

---

## 4. Mapping voce su Stories

| Voce | Adattamento Stories |
|---|---|
| Spiegato Facile | Sequenza didattica micro-passi (1 concetto per slide, esempio quotidiano) |
| Badvisor (tetto 20%) | Sequenza punch ridotta: hook paradosso â†’ 2-3 slide asimmetria â†’ CTA sarcastica |
| Caso Reale | Snippet narrativo (apertura personaggio in slide 1, evento in slide 2-3, esito implicito in slide 4-5) + disclaimer "Caso reale, nomi di fantasia" in slide finale (anche se ridotto) |
| Analisi | Micro-dato citato (slide 1: tesi Â· slide 2: dato + fonte+anno Â· slide 3-4: implicazione Â· slide 5: CTA approfondimento link/bio) |

### Tetto Badvisor 20% â€” verifica obbligatoria pre-invocazione
Come per altre skill social: verifica quota mensile prima di invocare voce Badvisor.

---

## 5. Disclaimer RUI su Stories â€” Brand Book v1.2 sez. 7

**Stories NON portano disclaimer RUI completo** per limite di formato (testo on-image 5-10 parole non lo consente).

Compensazione:
- **Bio profilo IG Advisory+** deve contenere disclaimer RUI (sempre attivo)
- **Per Stories che parlano di prodotti specifici o invitano alla sottoscrizione**: CTA sticker link verso pagina che contiene disclaimer RUI completo
- **Per Stories educational generiche**: nessun disclaimer in slide, bio fa da copertura
- Se la singola slide cita "Generali Italia â€“ Cattolica Assicurazioni", "DAS Difesa Legale", "UCA Tutela Legale e Peritale", "Europ Assistance" â†’ denominazione corretta sempre, anche su Stories

Compliance Officer gate verifica:
- Bio in regola (check periodico)
- Nessuna promessa rendimento garantito
- Nessun claim assoluto
- Denominazione corretta mandatarie se citate
- Caso Reale ha disclaimer ridotto in slide finale ("Caso reale, nomi fantasia")

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (pillar, voce, tema, numero slide preferito, data)
2. **Eseguire kickoff**
3. **Se voce Ã¨ Badvisor**: verifica quota 20%
4. **Invocare voce editoriale** via Task tool con brief mirato Stories micro-format:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale Stories set [3-5] slide Â· MAX 5-10 parole on-image per slide Â· struttura hook â†’ contenuto â†’ CTA Â· 1 sola variante (Stories sono brevi)."
   )
   ```
5. **Ricevere** testo essenziale per ciascuna slide
6. **Verifica vincoli**:
   - 5-10 parole per slide rispettato (se sfora, rielabora)
   - Sequenza hookâ†’contenutoâ†’CTA verificata
   - Voce coerente con pillar
7. **Suggerire sticker** appropriato per slide 1 (poll/question) e slide finale (link/CTA)
8. **Produrre brief visual** per ciascuna slide (handoff a skill `adv-image-stories` Sessione 4)
9. **Compliance Officer gate**: check bio + denominazione mandatarie + Caso Reale disclaimer ridotto se applicabile
10. **Suggerire highlight permanente** se pertinente
11. **Consegna al MM** con metadati completi

---

## 7. Casi particolari

### Stories serie tematica (es. 5 Stories settimana "Tutela Legale per chi?")
- 1 set/giorno per 5 giorni
- Stessa palette/template coordinati
- Hashtag serie in bio aggiornato
- Highlight permanente "Tutela Legale" alimentato

### Stories di rilancio Reel/post permanente
- Set di 2-3 slide: teaser visivo + frase + sticker link al post permanente
- Fallback se sticker link non attivo: "Link in bio"

### Stories di countdown evento (webinar Advisory+)
- Set di 3-4 slide: hook evento + dettagli + countdown sticker + RSVP CTA
- Stories ripetute con countdown aggiornato (3 giorni prima, 1 giorno prima, 1 ora prima)

### Stories Q&A (raccolta domande pubblico)
- Set di 2 slide: sticker question "Qual Ã¨ la tua domanda assicurativa?" + frase invito
- Risposte raccolte â†’ poi materiale per FAQ Educazione (Pillar 1) successive

### Stories di crisi (gestione comunicazione delicata)
- Voce Spiegato Facile o Caso Reale empatico (mai Badvisor in crisi)
- Compliance gate raddoppiato
- Eventuale skip se crisi Ã¨ troppo fresca (attesa onda mediatica)

---

## 8. Cosa NON fare mai

- âŒ **Paragrafi di testo on-image** (Stories sono micro-format, max 5-10 parole)
- âŒ **Set sopra 5 slide** (drop-off pesante)
- âŒ **Set sotto 3 slide** (non costruisce sequenza)
- âŒ **Riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- âŒ **Sforare tetto Badvisor 20%** senza segnalazione MM
- âŒ **Immagini di persone identificabili** senza consenso scritto
- âŒ **Loghi mandatarie** nel visual (solo in disclosure â†’ ma Stories non hanno disclosure, quindi mai)
- âŒ **Cross-post Stories da IG a FB automatico** se MM non lo specifica
- âŒ **Disclaimer RUI completo** in slide (limite formato â€” la bio fa copertura)
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Sticker link a URL non sicuri** (verificare sempre destinazione)
- âŒ **Highlight permanente per Stories effimere** (es. countdown evento finito) â€” gli highlight sono per contenuti evergreen

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance â€” paragrafo Stories e disclaimer Â· sez. 8 Design System)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/03_Social_Media_Manager.md` Â· `/01_Team/05_Art_Director.md`
3. `config/brand.json` (mapping voce-canale, dosaggio Badvisor 20%)
4. `config/design-system.json` (palette per Stories on-image)
5. `config/pillars-of-month.json`
6. `/05_Calendario_editoriale/[YYYY-MM]_*.md` (verifica quota Badvisor cumulato mese)
7. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-stories-set â€” Sessione 3 Plugin Build â€” 2026-05-18*

