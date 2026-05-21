---
name: visual-video-heygen-avatar
description: Wrapper Advisory+ per HeyGen MCP ufficiale (https://mcp.heygen.com/mcp/v1/, piano Creator $24/mese 15 min video/mese). Genera video con avatar AI parlante per explainer YouTube 5-10 min, Reel/Short 30-90 sec, video newsletter, case-study, video educational. VINCOLO DEFINITIVO Brand Book v1.2 sez. 14.4 + decisione CEO 2026-05-16: SOLO AVATAR GENERICO PROFESSIONALE, MAI clone Daniele Simonini o altri soci, MAI doppiaggio AI voce Daniele. Composiziona brief HeyGen integrando script ricevuto da skill content-* (content-youtube-video o content-reel-script) + selezione avatar generico tra catalogo HeyGen (preferenza: avatar maschile/femminile italiano-friendly etÃ  35-50 business attire) + voce italiana neutra (no clone) + sottotitoli burned-in obbligatori. Invoca compliance-ai-disclosure tipologia A per generare disclosure caption + on-screen sigla "Avatar AI Â· Advisory+". Esegue MCP call HeyGen via Task tool, riceve file MP4, salva in _assets/. Logga in /Log_visual_generati/.
---
# ðŸŽ¥ Skill visual-video-heygen-avatar â€” Wrapper HeyGen avatar generico

> **Solo avatar generico. Mai clone Daniele/soci. AI disclosure obbligatoria. Piano Creator $24/mese 15 min video.**

---

## 1. Quando triggera

- Invocata dalle skill content-youtube-video (per explainer + case-study con avatar) e content-reel-script (per Reel con avatar)
- Mai auto-trigger: serve sempre brief script dal chiamante

Tempo target di esecuzione: **10-20 minuti per video** (dipende da durata + latenza HeyGen API).

---

## 2. Output finale atteso

**File MP4** + metadata consegnati al chiamante:

```markdown
---
visual_id: [id univoco]
visual_path: Output_approvati/[file]_assets/[nome]_[id].mp4
formato: 1080Ã—1920 verticale (Reel) o 1920Ã—1080 orizzontale (YouTube)
durata: [N] sec / min
motore: HeyGen avatar (piano Creator)
avatar_selezionato: [nome avatar dal catalogo HeyGen]
voce_selezionata: [nome voce italiana neutra dal catalogo HeyGen]
script_originale: [riferimento file script]
sottotitoli_burned_in: SÃŒ (obbligatori)
costo_stimato_minuti_video: [N min]
quota_mensile_residua_minuti: [Y min / 15 min]
ai_disclosure: OBBLIGATORIA â€” invocata compliance-ai-disclosure tipologia A
ai_disclosure_caption: [stringa caption AI disclosure generata]
ai_disclosure_on_screen: "Avatar AI Â· Advisory+"
---
```

---

## 3. Specifiche HeyGen Advisory+

### Piano e quota
- **Piano Creator** $24/mese Â· **15 minuti video/mese**
- Upgrade a Team possibile dopo 1-2 mesi se domanda cresce (decisione differita)
- Verifica quota residua prima di ogni generazione (cap mensile)

### Avatar â€” VINCOLI HARD
- âœ… **Solo avatar generici professionali** dal catalogo HeyGen
- âœ… Preferenza: avatar maschile o femminile **italiano-friendly**, etÃ  apparente 35-50, business attire (giacca/camicia, nessun dress code estremo)
- âœ… Avatar coerente con tono del contenuto (piÃ¹ formale per Analisi/Imprese, piÃ¹ rilassato per Spiegato Facile/Famiglia)
- ðŸ”´ **VIETATO**: clone Daniele Simonini (Italian male ~50, professional consultant features)
- ðŸ”´ **VIETATO**: clone altri soci (Agostini, Barrella, Fappani, senior advisor)
- ðŸ”´ **VIETATO**: avatar che condivide caratteristiche distintive identificabili (capelli, barba, occhiali specifici di Daniele, ecc.)
- ðŸ”´ **VIETATO**: avatar custom creato con foto reali dei soci (anche se foto sono pubbliche)

### Voce â€” VINCOLI HARD
- âœ… **Voci italiane neutre** dal catalogo HeyGen (es. "Marco IT", "Sofia IT", "Luca IT")
- âœ… Tono coerente con voce editoriale (asciutto per Analisi, caldo per Spiegato Facile, narrativo per Caso Reale)
- ðŸ”´ **VIETATO**: clone vocale Daniele Simonini (mai upload sample voce Daniele a HeyGen per voice cloning)
- ðŸ”´ **VIETATO**: doppiaggio AI di audio originale Daniele (mai)
- ðŸ”´ **VIETATO**: voci che imitano celebritÃ  o persone reali

### Sottotitoli
- **OBBLIGATORI burned-in** (80% pubblico no-audio)
- Generati automaticamente da HeyGen durante produzione + correzione manuale obbligatoria (errori frequenti su tecnicismi assicurativi italiani)
- Font: Inter Tight bold, posizione bassa centrale, contrast forte (testo bianco con outline scuro)

### AI disclosure â€” OBBLIGATORIA
Invocazione automatica di `advisory-plus:compliance-ai-disclosure` tipologia A:
- **Caption/descrizione**: testo completo "Video prodotto dalla redazione Advisory+. L'avatar Ã¨ generato con intelligenza artificiale (HeyGen)..."
- **On-screen**: sigla "Avatar AI Â· Advisory+" in corner basso destra quando l'avatar Ã¨ in scena

### Formato output
- **YouTube explainer/case-study**: 1920Ã—1080 H.264 MP4, 30fps
- **YouTube Short**: 1080Ã—1920 H.264 MP4, 30fps
- **Reel IG/FB**: 1080Ã—1920 H.264 MP4, 30fps

---

## 4. Catalogo avatar Advisory+ â€” preferenze (selezione da catalogo HeyGen)

Da consolidare con Art Director in fase di prima produzione. Preferenze indicative:

| Pillar / contenuto | Avatar preferito | Voce preferita |
|---|---|---|
| P1 Educazione (Spiegato Facile) | Avatar femminile etÃ  35-45 business casual, sorriso accogliente | Voce femminile italiana calma |
| P3 News di settore (Analisi) | Avatar maschile etÃ  45-50 business formale | Voce maschile italiana asciutta |
| P5 AnzianitÃ  & LTC (Caso Reale) | Avatar femminile etÃ  40-50 sobria | Voce femminile italiana narrativa |
| P9 Imprese & Professionisti (Analisi) | Avatar maschile etÃ  45-50 business formale | Voce maschile italiana autorevole |
| P12 Terzo Settore | Avatar femminile etÃ  40-50 sobria | Voce femminile italiana misurata |

**Mai rotazione casuale**: stesso pillar = stesso avatar (per costruire familiaritÃ  nel pubblico).

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief script** dal chiamante (content-youtube-video o content-reel-script): script con timing, durata target, formato, pillar
2. **Eseguire kickoff** per contesto workspace
3. **Verifica quota mensile** HeyGen residua (lookup `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md`)
4. **Se quota insufficiente**: notifica MM + suggerimento (rinviare al mese successivo o passare a Remotion tipografico)
5. **Lookup avatar/voce** per pillar (sez. 4)
6. **Verifica script per durata**: stima tempo (ca. 130-150 parole/min parlato) â†’ se sfora il budget mensile residuo, segnala
7. **Comporre brief HeyGen** integrando: script + avatar selezionato + voce selezionata + sottotitoli burned-in setting
8. **Invocare HeyGen MCP** via Task tool (HeyGen MCP ufficiale registrato in `mcp/`):
   ```
   Task(
     subagent_type: "heygen_avatar_video_generate",
     prompt: "Genera video avatar con: script [X], avatar [Y], voce [Z], formato [F], sottotitoli burned-in [posizione/font/contrast]."
   )
   ```
9. **Ricevere link/file MP4** generato
10. **Download e salvataggio** in `Output_approvati/[file]_assets/[nome]_[id].mp4` via Bash
11. **Correzione manuale sottotitoli** (richiesto al chiamante o MM â€” automazione automatica non possibile per tecnicismi italiani)
12. **Invocare `advisory-plus:compliance-ai-disclosure` tipologia A** via Task tool per generare caption disclosure + on-screen sigla
13. **Loggare** in `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md` con: data, durata, costo minuti consumati, quota residua, esito
14. **Restituire metadata + path file MP4** al chiamante + AI disclosure pacchetto

---

## 6. Casi particolari

### Quota HeyGen mensile esaurita
- ðŸ”´ blocco generazione
- Notifica MM: "Quota HeyGen 15 min mensile esaurita. Suggerimenti: (a) rinvio video al mese prossimo, (b) passa a Remotion tipografico (visual-video-remotion), (c) richiedi upgrade a Team (decisione CEO + budget approvato)."

### Pillar 2 Voce CEO (Daniele) â€” gestione vincolo voce autentica
- ðŸ”´ blocco se script richiede voce avatar parlante (HeyGen avatar Daniele = vietato)
- Suggerimento: produrre video con **voce off autentica Daniele registrata** + Remotion tipografico per visual, oppure Daniele in camera (no AI)

### Richiesta brief con avatar personalizzato basato su foto reale
- ðŸ”´ blocco immediato
- Suggerimento: "Brief richiede avatar custom da foto. VIETATO da decisione CEO 2026-05-16. Usa avatar generico dal catalogo HeyGen."

### Validazione pre-produzione (modalitÃ  draft)
- ModalitÃ  "dry-run": skill puÃ² restituire SOLO il brief HeyGen composto senza eseguire MCP call
- Utile per MM/CEO che vogliono validare avatar + voce + script prima di consumare quota mensile
- Triggera via parametro `--dry-run`

### Video di crisi (sinistro mandataria, eventi gravi)
- ðŸ”´ blocco automatico (ModalitÃ  Crisi sospende generazione contenuti automatici)
- Se necessario, gestione manuale MM/CEO con avatar generico + tono particolarmente sobrio

### Video co-marketing con partner (es. ordine professionale, ente)
- Brief HeyGen include menzione partner in script
- AI disclosure caption include riferimento partnership
- Compliance gate raddoppiato

---

## 7. Cosa NON fare mai

- âŒ **Avatar HeyGen clone Daniele Simonini o altri soci** (vincolo etico definitivo CEO 2026-05-16)
- âŒ **Voice cloning Daniele** o voci di altri soci (vietato AI Act UE + decisione CEO)
- âŒ **Doppiaggio AI di audio autentico Daniele** (vietato definitivo Brand Book v1.2 sez. 14)
- âŒ **Avatar custom da foto reali** dei soci o altre persone identificabili
- âŒ **Sforare quota mensile** HeyGen senza notifica MM
- âŒ **Saltare AI disclosure** (compliance-ai-disclosure obbligatoria, tipologia A)
- âŒ **Sottotitoli senza correzione manuale** (errori tecnicismi assicurativi auto-generati)
- âŒ **Cambio avatar a rotazione** per stesso pillar (mantieni familiaritÃ )
- âŒ **Voice italiana con accento marcato** che possa essere percepito come imitazione regionale
- âŒ **Saltare log** in `Log_visual_generati/[YYYY-MM]_heygen.md`

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 14 stack video + ETICA AI definitiva)
2. `/01_Team/09_Content_Producer.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (sez. `ai_act_ue` Â· vincoli avatar)
4. `config/budget.json` (cap mensile HeyGen)
5. `/05_Calendario_editoriale/Log_visual_generati/[YYYY-MM]_heygen.md` (quota residua)
6. Il brief script del chiamante

---

*SKILL v1.0 â€” advisory-plus:visual-video-heygen-avatar â€” Sessione 4 Plugin Build â€” 2026-05-19*

