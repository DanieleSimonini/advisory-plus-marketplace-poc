---
name: content-instagram-caption
description: Compone una caption Instagram pronta da pubblicare insieme a post singolo, carosello o Reel sulla pagina Instagram Advisory+ brand. Orchestra: voce editoriale (tutte e 4 secondo pillar â€” Spiegato Facile prevalente, Badvisor moderato con tetto 20% mese, Caso Reale per storytelling visivi, Analisi solo per contenuti tecnici come Pillar 3 News quando ha agganci visivi forti) â†’ invoca skill voce-* via Task tool â†’ riceve testo in-context â†’ applica formattazione Instagram (200-300 parole, primo paragrafo entro 150 caratteri anti-troncamento "...altro" IG, 8-12 hashtag mix tematici, NO hashtag locali Brand Book v1.2 nazionale, link in bio non in caption perchÃ© IG non clicca link in caption, emoji moderato 1-3 per paragrafo) â†’ produce brief visual associato (post 1080Ã—1080 o carosello 1080Ã—1080 multi-slide) â†’ Compliance gate â†’ consegna al MM.
---
# ðŸ“· Skill content-instagram-caption â€” Caption Instagram pagina Advisory+

> **Tono accessibile e visivo. Primo paragrafo cruciale (vincolo "...altro" IG). Hashtag generosi 8-12. Link in bio, mai in caption.**

---

## 1. Quando triggera

- Invocata dal MM durante settimana per slot Instagram (frequenza standard: 3-4/sett ~14/mese, mix post singoli + caroselli + Reel)
- Invocata per accompagnare un Reel (caption Reel ha specifiche proprie â€” vedi skill `content-reel-script`)
- Invocata per accompagnare uno Stories set (per cross-post di una Storia in post permanente â€” vedi skill `content-stories-set`)
- Mai auto-trigger

Tempo target: **4-6 minuti**.

---

## 2. Output finale atteso

**File Markdown Buffer-ready** consegnato al MM:

```markdown
---
canale: instagram_pagina_brand
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. mer 19:00, ven 12:00 â€” finestre IG engagement]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Badvisor / Caso Reale / Analisi]
formato: [post_singolo / carosello_X_slide / reel â€” se reel rimanda a content-reel-script]
firma: brand Advisory+
visual_brief: brief_visual_[id].md (1080Ã—1080 singolo o carosello)
link_in_bio_update: [URL da settare in bio Linktree/equivalente, se applicabile]
quota_mensile_badvisor: [X% â€” tetto hard 20%]
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

# CAPTION (corpo)
[PRIMO PARAGRAFO â‰¤ 150 caratteri â€” Ã¨ ciÃ² che si legge prima di "...altro"]

[Sviluppo: 200-300 parole totali Â· paragrafi brevi Â· 1-3 emoji per paragrafo Â· interruzioni grafiche con riga vuota]

[Chiusura: invito conversazione + "Link in bio per approfondire" se applicabile]

# HASHTAG (in coda alla caption o nel primo commento â€” pattern brand Advisory+: in coda separati da riga bianca)
#AdvisoryPlus #ConsulenzaAssicurativa #[tema1] #[tema2] #[tema3] #[tema4] #[tema5] #[tema6] #[tema7] #[tema8]

# LINK IN BIO (azione MM)
Aggiornare Linktree/equivalente con URL: [URL] Â· etichetta: [es. "Articolo TCM giovani genitori"]
```

---

## 3. Specifiche Instagram pagina brand

### Lunghezza
- **200-300 parole** totali nella caption
- Sweet spot algoritmico per IG: dwell-time premiato
- Sopra 300p = "...altro" scatta presto, ma Ã¨ ok per voce Caso Reale narrativa

### Primo paragrafo â€” vincolo critico
- **â‰¤ 150 caratteri** (NB: caratteri, non parole)
- Ãˆ ciÃ² che si legge nel feed prima di "...altro" che taglia il resto
- DEVE contenere l'hook completo del post (paradosso, domanda, apertura Caso Reale, tesi Analisi)
- Esempi:
  - Spiegato Facile: "Cos'Ã¨ davvero la franchigia? Te la spiego con il frigorifero rotto." (84 char âœ“)
  - Caso Reale: "Marta, 52 anni. Sua madre Ada, 81, Ã¨ caduta in bagno. Ecco cosa Ã¨ successo dopo." (95 char âœ“)
  - Badvisor: "Hai un piano per le ferie. Per tua madre quando non riuscirÃ  piÃ¹ a farsi la doccia, l'hai?" (92 char âœ“)
  - Analisi: "ANIA 2025: ramo vita -12%. Cosa sta succedendo davvero." (62 char âœ“)

### Hashtag
- **8-12 hashtag** in blocco a fine caption (pattern brand Advisory+: in coda, separati da riga bianca dalla caption)
- Mix: 2 brand (`#AdvisoryPlus` + `#ConsulenzaAssicurativa`) + 6-10 tematici del pillar
- IG tollera generosamente gli hashtag (a differenza di FB)
- **NO hashtag locali** (Versilia/Apuana/Toscana â€” posizionamento nazionale Brand Book v1.2)
- **NO hashtag #money #investing in inglese** (pubblico IT, hashtag IT)

### Link
- **MAI in caption** (Instagram non rende cliccabili i link in caption)
- **Link in bio** (Linktree o equivalente): la skill segnala al MM se l'URL del post va aggiornato in bio
- Se serve un solo URL stabile (sito): lasciare quello fisso in bio, non cambiarlo per ogni post

### Emoji
- **1-3 emoji per paragrafo** (moderato)
- Emoji devono **aggiungere significato**, non decorare
- âœ… "ðŸ’¡ Ecco il punto:" (l'emoji introduce un'illuminazione)
- âŒ "ðŸŒŸâœ¨ðŸŽ‰ Buongiorno! ðŸ’•ðŸ”¥" (decorazione vuota)
- Voce **Analisi** evita emoji nel corpo (registro asciutto)

### Visual
- **Post singolo 1080Ã—1080** (formato quadrato standard IG)
- **Carosello 1080Ã—1080 Ã— N slide** (max 10 slide â€” IG limite)
- Carosello consigliato per: Spiegato Facile a passi numerati Â· Caso Reale a episodi Â· Analisi a dati visualizzati
- Brief visual prodotto da skill `adv-image-instagram-post` o `adv-image-instagram-carousel` (Sessione 4)
- Per Reel: vedi skill `content-reel-script`

### Orario di pubblicazione raccomandato
- **Mer-Gio-Ven**: 12:00-13:00 (pausa pranzo) e 19:00-21:00 (sera)
- **Sab-Dom**: 11:00-13:00
- **Lun mattina + Ven sera**: evitare

---

## 4. Mapping voce per pillar su Instagram

| Pillar | Voce primaria | Voce secondaria | Note IG |
|---|---|---|---|
| P1 Educazione (always-on) | Spiegato Facile | Badvisor occasionale Reel | |
| P3 News di settore (always-on) | Spiegato Facile (divulgativo) | Analisi (raro, solo con visual forte) | Apparato citazionale comprimibile in caption breve |
| P4 Famiglia & Vita | Spiegato Facile | Caso Reale | |
| P5 AnzianitÃ  & LTC | Caso Reale | Badvisor (tetto) | LTC Ã¨ tema centrale, storytelling potente su IG |
| P6 Risparmio & Investimento | Spiegato Facile | Analisi (raro) | |
| P7 Tutela Legale | Caso Reale | Spiegato Facile | |
| P8 Casa & Patrimonio | Spiegato Facile | Caso Reale | |
| P9 Imprese & Professionisti | Skip o raro | â€” | Pubblico IG retail-skewed, B2B su LinkedIn |
| P10 Mare & Yacht | Caso Reale | Spiegato Facile (lifestyle) | Visual specialty forte |
| P11 Arte & Patrimonio | Caso Reale | Analisi | Visual specialty forte |
| P12 Terzo Settore | Caso Reale | Analisi | |

### Tetto Badvisor 20% â€” verifica obbligatoria pre-invocazione
Come per `content-linkedin-post-daniele`, prima di invocare `advisory-plus:voce-badvisor`, verificare quota mensile cumulata (tutti i canali) e bloccare/segnalare se â‰¥20%.

---

## 5. Pattern per formato

### Pattern post singolo
- Caption 200-280 parole
- Hook in primo paragrafo â‰¤150 char
- 8-10 hashtag in coda
- Visual: 1080Ã—1080 con max 5-7 parole on-image

### Pattern carosello (3-10 slide)
- Caption 250-350 parole (carosello tollera caption piÃ¹ lunga)
- Hook in primo paragrafo â‰¤150 char + "Scorri per vedere tutti i [N] passaggi"
- 10-12 hashtag in coda
- Visual: 1080Ã—1080 Ã— N slide
  - Slide 1 = cover/hook visivo (deve fermare lo scroll)
  - Slide 2-(N-1) = contenuto a passi (un'idea per slide)
  - Slide N = CTA + "Link in bio per approfondire"
- Carosello Ã¨ il formato a maggior dwell-time â†’ premiato dall'algoritmo

### Pattern caption per Reel (delega a content-reel-script)
- Caption Reel = 100-150 parole (piÃ¹ breve del post)
- 8-10 hashtag
- Vedi skill `content-reel-script` per script e storyboard

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (pillar, voce, formato post/carosello, tema, data)
2. **Eseguire kickoff**
3. **Se voce Ã¨ Badvisor**: verificare quota 20% mese
4. **Invocare voce editoriale** via Task tool con brief mirato Instagram:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale Instagram caption Â· formato [post_singolo/carosello_X_slide] Â· lunghezza 200-300p (350p se carosello) Â· primo paragrafo OBBLIGATORIAMENTE â‰¤150 char Â· 2 varianti."
   )
   ```
5. **Ricevere** testo (2 varianti)
6. **Verifica vincoli critici**:
   - Lunghezza 200-300p (350p tollerato solo per carosello)
   - **Primo paragrafo â‰¤150 caratteri** (counter rigoroso â€” se sfora, rilancia voce)
   - Zero riferimenti territoriali
   - Quota Badvisor rispettata
7. **Produrre blocco hashtag** 8-12 da `config/brand.json`
8. **Produrre brief visual** (post singolo o carosello, handoff a skill visual Sessione 4)
9. **Compliance Officer gate** via Task tool
10. **Se ðŸŸ¡/ðŸ”´**: riformulazione, ri-check
11. **Se ðŸŸ¢**: consegna al MM con eventuale segnalazione aggiornamento link in bio

---

## 7. Casi particolari

### Post di rilancio articolo blog
- Caption teaser con hook + 3 punti chiave
- "Link in bio" verso articolo (segnalazione aggiornamento Linktree)
- Carosello consigliato (3-5 slide con punti chiave)

### Specialty drop stagionale (P10 Mare in giugno)
- Visual sub-identity specialty (accent ocra Warning â‰¤5%, Brand Book v1.2 sez. 8.1)
- Hashtag specialty (#Yacht, #Specialty, #Mare)
- Carosello storytelling Caso Reale

### Post tematico in serie (es. 5 puntate Pillar 5 LTC)
- Hashtag serie dedicato (es. `#SerieAdvisoryLTC`) per facilitare ritrovabilitÃ 
- Caption con riferimento "Puntata X/5"
- Visual coordinato (stessa palette/template per tutte le 5 puntate)

### Post di reazione a evento di settore
- Voce Analisi compressa in caption breve + carosello con dati visualizzati
- Apparato citazionale comprimibile (fonte+anno inline nel testo + sintesi visual su slide)

---

## 8. Cosa NON fare mai

- âŒ **Primo paragrafo > 150 caratteri** (vincolo critico anti-troncamento)
- âŒ **Link cliccabile in caption** (IG non rende cliccabili â†’ frustrazione utente)
- âŒ **Riferimenti territoriali** (Versilia/Apuana/Toscana)
- âŒ **Hashtag oltre 12** o sotto 8 (sweet spot algoritmico)
- âŒ **Hashtag locali**
- âŒ **Emoji a cascata** (max 1-3 per paragrafo, mai paragrafi di emoji)
- âŒ **Sforare tetto Badvisor 20% mese** senza segnalazione MM
- âŒ **Pillar 9 Imprese su IG** (demografica sbagliata, riservare a LinkedIn)
- âŒ **Apparato citazionale tecnico fitto** in caption breve (semmai Analisi in carosello con dati visualizzati)
- âŒ **Tono commerciale aggressivo** ("Compra subito!", "Offerta limitata!")
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Loghi mandatarie** nel visual (solo in disclosure)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento nazionale Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance Â· sez. 8 Design System)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/03_Social_Media_Manager.md` Â· `/01_Team/02_Copywriter.md`
3. `config/brand.json` (hashtag per pillar, mapping voce-canale, frequenze IG, dosaggio Badvisor 20%)
4. `config/pillars-of-month.json`
5. `/05_Calendario_editoriale/[YYYY-MM]_*.md` (verifica quota Badvisor cumulato mese)
6. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-instagram-caption â€” Sessione 3 Plugin Build â€” 2026-05-18*

