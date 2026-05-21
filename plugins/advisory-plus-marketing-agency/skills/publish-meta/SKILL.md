---
name: publish-meta
description: Pubblicazione automatica Instagram (@advisoryplus_) + Facebook (Pagina Advisory+) via Meta Graph API con token long-lived. Supporta tutti i formati: post statico Â· carosello 2-10 slide Â· Reel 30-60s Â· Stories set 3-5 slide. Cross-posting nativo IGâ†”FB quando appropriato (decisione MM). Doppio gate Compliance T-30min + AI disclosure obbligatoria se Reel con HeyGen avatar + denominazione mandatarie corretta + posizionamento nazionale. Asset visivi caricati da Cloudinary (Sessione 8 MCP) o `/04_Risorse/_log_screenshots/temp/` per upload diretto. Tutta la logica tecnica delegata a `scripts/publish-meta.sh` (Sessione 7 script). Screenshot post-publish via Chrome MCP + log permalink. Kill switch rispettato. Token Meta long-lived 60gg refresh proattivo a 7gg dalla scadenza.
---
# ðŸ“¸ Skill publish-meta â€” Pubblicazione Instagram + Facebook via Meta Graph API

> **IG + FB Â· 4 formati Â· cross-posting nativo Â· gate-doppio Â· AI disclosure se HeyGen Â· token long-lived.**

---

## 1. Quando triggera

- Schedulazione automatica T-30min da calendario editoriale per ogni contenuto IG/FB in stato `Programmato`
- Invocata da `advisory-plus:publish-scheduling` come step canale-specifico
- Invocata on-demand dal MM per pubblicazione ad-hoc
- Mai trigger se kill switch attivo o Crisis mode

Tempo target di esecuzione: **3-7 minuti** (piÃ¹ lungo per Reel video upload).

---

## 2. Formati supportati

| Formato | Canale primario | Cross-post | Asset | API endpoint Meta |
|---|---|---|---|---|
| Post statico | IG + FB | sÃ¬ (decisione MM) | 1080Ã—1080 o 1200Ã—630 | `/me/media` + `/me/media_publish` |
| Carosello 2-10 slide | IG primario Â· FB derivato | parziale (FB non ha carosello nativo identico) | 1080Ã—1080 Ã— N | `/me/media?media_type=CAROUSEL` |
| Reel 30-60s | IG primario Â· FB cross-nativo | sÃ¬ (Reel Meta unificati) | video 1080Ã—1920 9:16 | `/me/media?media_type=REELS` |
| Stories set 3-5 slide | IG + FB (gemelli) | sÃ¬ | 1080Ã—1920 9:16 Ã— N | `/me/stories` |

---

## 3. Output finale atteso

**Log entry** in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`:

```markdown
## Pubblicazione 2026-XX-XX HH:MM â€” [IG | FB | IG+FB cross-post]

- **Skill chiamante**: advisory-plus:publish-meta
- **Formato**: [Post statico | Carosello N slide | Reel | Stories set N slide]
- **Post source**: Output_approvati/03_Instagram_Facebook/[file].md
- **Pillar**: P[N] [Nome]
- **Voce**: [...]
- **Compliance check T-30min**: ðŸŸ¢
- **AI disclosure**: [presente caption + on-screen | n/a (no HeyGen) ]
- **Asset caricati**: [N asset Â· path/URL]
- **Permalink IG**: https://www.instagram.com/p/[shortcode]/
- **Permalink FB**: https://www.facebook.com/[page]/posts/[ID]
- **Screenshot IG**: 04_Risorse/_log_screenshots/IG_[YYYY-MM-DD]_HHMM.png
- **Screenshot FB**: 04_Risorse/_log_screenshots/FB_[YYYY-MM-DD]_HHMM.png
- **Stato calendario editoriale**: aggiornato â†’ `Pubblicato ðŸŸ¢`
- **Token Meta scadenza**: [Da rinnovare in N giorni Â· OK]
- **Eventuali avvisi**: [...]
```

---

## 4. Pre-publish check (T-30min)

### 4.1 Compliance drift check (gate-doppio)
- Disclaimer bio fa copertura su social (Brand Book v1.2 sez. 7) â€” non serve nel body
- Stories: esenti da disclaimer RUI per limite formato (Brand Book v1.2 sez. 7)
- AI disclosure OBBLIGATORIA su Reel con HeyGen avatar (caption "Avatar AI Â· Advisory+" + on-screen 1-2 sec) â€” AI Act UE artt. 50, 52
- Denominazione mandatarie corretta se citate
- NO loghi mandatarie nel body o cover (vincolo IVASS hard)
- NO claim ðŸ”´ vietati
- NO riferimenti territoriali (Versilia/Apuana/Toscana)

### 4.2 Brand Strategist coerenza check
- Pillar dichiarato vs contenuto
- Voce dichiarata vs voce effettiva
- Tetto Badvisor 20% mensile (Reel Badvisor entra nella quota)
- Frequenza canale rispettata (Brand Book v1.2 sez. 5: IG 3/sett Â· FB 2/sett)

### 4.3 Health check tecnico
- Token Meta valido (scadenza >7gg â†’ OK, â‰¤7gg â†’ refresh proattivo via API + notifica CEO)
- Quota API: Graph API ha limiti generosi (~200/h per app Â· ampiamente sufficiente)
- Asset caricabili (file size, formato, dimensioni)
- Caratteri caption (IG â‰¤2200, FB â‰¤63206)
- Hashtag (IG 8-12, FB 3-5 â€” Brand Book v1.2 sez. 5)

### 4.4 Format-specific check
- **Post statico**: 1 immagine 1080Ã—1080 o 1200Ã—630, alt text presente, caption â‰¤2200 char
- **Carosello**: 2-10 slide 1080Ã—1080, prima slide cover, ultima CTA, alt text per ogni slide
- **Reel**: video 9:16 1080Ã—1920, durata 30-60s, sottotitoli burned-in obbligatori (80% pubblico no-audio), hook in 3 sec verificato (Brand Book v1.2 sez. 4)
- **Stories**: 3-5 slide 9:16 1080Ã—1920, â‰¤10 parole per slide, sticker IG nativi (poll/question/countdown/link) opzionali

---

## 5. Cross-posting IG â†” FB (decisione MM)

### Quando cross-postare automaticamente
- **Reel IG â†’ FB**: sÃ¬ nativo (Meta li unifica). Caption puÃ² differire (FB tono piÃ¹ caldo, lunghezza differente).
- **Post statico IG â†’ FB**: sÃ¬ con riformulazione caption (FB Brand Book v1.2 sez. 5 voce Spiegato Facile prevalente).
- **Stories IG â†’ FB**: sÃ¬ gemello (formati uguali).

### Quando NON cross-postare
- **Carosello IG**: FB non ha carosello nativo identico, si converte in album foto multiplo. Decisione MM caso-per-caso (puÃ² essere meglio singolo post FB con la slide piÃ¹ impattante).
- **Voce Badvisor**: ammesso su IG (Brand Book v1.2 sez. 5), MAI su FB (registro mismatch â€” Brand Book v1.2 sez. 5). Cross-post bloccato automatico.
- **Voce Analisi tecnica**: ammessa su IG (caroselli didattici), MAI su FB pure tecnica (audience piÃ¹ adulta divulgativa).

### Riformulazione automatica caption
Skill puÃ² variare leggermente la caption per FB (es. accorciare hashtag a 3-5 vs 8-12 IG, riformulare apertura per pubblico FB piÃ¹ maturo). Il messaggio chiave resta identico.

---

## 6. AI disclosure (AI Act UE artt. 50, 52)

**OBBLIGATORIA quando**:
- Reel usa HeyGen avatar generico parlante
- Reel usa cc-nano-banana per immagini foto-realistiche

**Formato disclosure**:
- **Caption**: "Avatar AI Â· Advisory+" come prima riga della caption (alta visibilitÃ )
- **On-screen**: badge "Avatar AI" piccolo 1-2 sec nei primi 3 sec del video (non invasivo ma visibile)

**Eccezioni**:
- Remotion motion graphics (motion tipografico + voce umana = umano, NON AI Act UE) â†’ no disclosure
- Stories generici senza avatar AI â†’ no disclosure
- Post statico generato cc-nano-banana stile illustrativo (non foto-realistico) â†’ no disclosure

âš ï¸ **Pendenza pre-go-live**: validazione formulazione esatta disclosure con consulente privacy/legale esterno (target validazione prima del primo Reel HeyGen pubblicato â€” luglio 2026).

---

## 7. Logica di esecuzione â€” passo-passo

1. **Schedulazione T-30min** attiva pre-publish check
2. **Pre-publish check** (sez. 4): se ðŸ”´ â†’ blocco Â· se ðŸŸ¡ â†’ riformulazione max 1 iter
3. **Leggere post finale** da `Output_approvati/03_Instagram_Facebook/[file].md`
4. **Determinare formato** (post Â· carosello Â· Reel Â· Stories) + canale primario (IG Â· FB Â· IG+FB)
5. **Recuperare asset** da:
   - Cloudinary MCP (Sessione 8 wiring) via URL pubblico
   - Oppure `/04_Risorse/Brand_Visual/` per asset locali
   - Asset temp da `visual/image-static-nano-banana` o `visual/video-heygen-avatar` o `visual/video-remotion` (Sessione 4) generati ad-hoc
6. **Aggiungere UTM parameter** ai link nel post (per attribution model)
7. **Invocare script** `scripts/publish-meta.sh [formato] [canale] [payload-json] [asset-paths]` (Sessione 7 script)
8. **Ricevere response**: media_id IG Â· post_id FB Â· permalink
9. **Attesa T+2-5min** per visibilitÃ  pubblica
10. **Invocare script** `scripts/log-publish.sh [canale] [permalink]` per screenshot Chrome MCP
11. **Aggiornare log** + calendario editoriale
12. **Notificare MM** sintetico

---

## 8. Casi particolari

### Reel con HeyGen avatar (post-launch YouTube giugno-luglio 2026)
- AI disclosure obbligatoria (sez. 6)
- Caption opening: "Avatar AI Â· Advisory+ [resto della caption]"
- On-screen badge nei primi 3 sec
- Compliance gate-doppio ha giÃ  verificato in fase scrittura, drift check T-30min ri-verifica

### Stories con sticker link verso blog
- Link tracciato con UTM (`utm_source=instagram_stories&utm_medium=organic&utm_campaign=P[N]_[tema]`)
- Sticker nativo IG, non link in caption (le Stories supportano sticker link diretto solo se account verificato â€” Advisory+ verificato? caveat caso-per-caso)

### Cross-post IG â†’ FB con voce mismatch
- Skill rileva voce Badvisor â†’ blocco automatico cross-post FB â†’ solo IG
- Notifica MM con suggerimento "creare versione FB Spiegato Facile o saltare FB questa volta"

### Token Meta scaduto durante esecuzione
- Skill rileva 401 Unauthorized â†’ tenta refresh token automatico (se refresh_token valido)
- Se refresh fallisce â†’ blocco + email alert CEO entro 1h ("Token Meta scaduto, riconnetti app")
- Calendar resta `Programmato`, retry automatico ogni 4h fino a risoluzione

### Quota API esaurita
- Improbabile (limiti generosi) ma gestito: retry con backoff esponenziale (5min, 15min, 30min)
- Se persistente: notifica MM

### Big bet con OK CEO esplicito
- Stato `Approvato CEO âœ…` â†’ bypass del drift check Compliance (giÃ  OK CEO) ma mantiene health check + format check + kill switch

### Asset visivo non pronto
- Se asset Cloudinary URL 404 o asset locale assente â†’ blocco + handoff a `visual/*` per generazione + retry tra 15 min
- Se asset non recuperabile entro 2h â†’ blocco + notifica MM

---

## 9. KPI publish-meta (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Tasso di successo pubblicazione (no errori) | â‰¥99% |
| Latency tra timestamp programmato e pubblicazione | <3 min |
| Compliance drift check fallito (ðŸ”´) | <1% pubblicazioni |
| AI disclosure compliance | 100% Reel HeyGen |
| Cross-post IGâ†”FB success rate | â‰¥95% |
| Screenshot caricato entro T+5min | â‰¥98% |
| Token Meta refresh proattivo (>7gg scadenza) | 100% |

---

## 10. Compliance & sicurezza

âœ… **Doppio gate Compliance** (scrittura + drift T-30min)
âœ… **AI disclosure** AI Act UE su Reel HeyGen / cc-nano-banana foto-realistico
âœ… **Denominazione mandatarie corretta** se citate
âœ… **NO loghi mandatarie in body/cover** (IVASS hard)
âœ… **Posizionamento nazionale** (no Versilia/Apuana)
âœ… **No claim ðŸ”´** vietati
âœ… **Tetto Badvisor 20%** mensile verificato cumulato
âœ… **Frequenza canale** Brand Book v1.2 sez. 5
âœ… **UTM parameter** per attribution
âœ… **Screenshot + log** post-publish
âœ… **Token sicurezza** `config/email.env` gitignored
âœ… **Kill switch** rispettato

âŒ **Mai**:
- Cross-post Badvisor IG â†’ FB (registro mismatch FB)
- Pubblicazione Reel HeyGen senza AI disclosure
- Loghi mandatarie come asset principale
- Stories con disclaimer RUI (formato non lo supporta â€” bio fa copertura)
- Caption FB lunga uguale a IG (audience diversa, lunghezze diverse)
- Modifica payload tra approvazione e pubblicazione

---

## 11. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pubblicare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 5 strategia IG/FB Â· sez. 6 Pillar Map Â· sez. 7 Compliance + AI Act UE Â· sez. 8 Design System)
2. `/01_Team/03_Social_Media_Manager.md` + `/01_Team/04_Compliance_Officer.md` + `/01_Team/09_Content_Producer.md`
3. `config/brand.json` (IG handle, FB Page ID, mandatarie, AI disclosure regole)
4. `config/email.env` (META_LONG_LIVED_TOKEN, META_PAGE_ID, META_IG_BUSINESS_ID)
5. `config/AUTOMAZIONE_ATTIVA`
6. Post sorgente + asset visivi
7. Calendario editoriale + tetti cumulati

---

## 12. Cosa NON fare mai

- âŒ **Pubblicare senza pre-publish check**
- âŒ **Reel HeyGen senza AI disclosure** (AI Act UE violation)
- âŒ **Cross-post Badvisor su FB** (Brand Book v1.2 sez. 5)
- âŒ **Loghi mandatarie come asset** (IVASS hard)
- âŒ **Modifica payload mid-flight**
- âŒ **Bypass kill switch**
- âŒ **Skip screenshot**
- âŒ **Token refresh manuale** senza notifica CEO
- âŒ **Hashtag territoriali default** (Brand Book v1.2 sez. 2)
- âŒ **Reel <30s o >60s** (range IG/FB Reel ottimale)
- âŒ **Caption IG >2200 char** (troncamento + algoritmo penalizza)

---

*SKILL v1.0 â€” advisory-plus:publish-meta â€” Sessione 7 Plugin Build â€” 2026-05-22*

