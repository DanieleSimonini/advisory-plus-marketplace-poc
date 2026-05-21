---
name: content-facebook-post
description: Compone un post pronto da pubblicare sulla pagina Facebook Advisory+ brand. Orchestra: voce editoriale (Spiegato Facile primaria + Caso Reale per storytelling + Specialty quando attiva â€” NO Analisi su FB perchÃ© registro tecnico non funziona, NO Badvisor su pagina FB) â†’ invoca skill voce-* via Task tool â†’ riceve testo in-context â†’ applica formattazione Facebook (150-200 parole piÃ¹ breve di LinkedIn, tono caldo accessibile, 3-5 hashtag che FB tollera poco, link in primo commento perchÃ© FB penalizza link nel corpo come LinkedIn, cover 1200Ã—630 formato landscape FB) â†’ produce brief visual â†’ Compliance gate â†’ consegna al MM. Supporta pattern cross-posting da Instagram (carosello â†’ singolo post + link, Reel â†’ cross-posting nativo Meta). Posizionamento NAZIONALE: zero riferimenti territoriali (Brand Book v1.2 sez. 2).
---
# ðŸ“˜ Skill content-facebook-post â€” Post pagina Facebook Advisory+

> **Voce piÃ¹ calda e accessibile di LinkedIn. PiÃ¹ breve. Tono familiare ma sempre consulenziale. Mai Badvisor, mai Analisi su FB.**

---

## 1. Quando triggera

- Invocata dal MM durante settimana per slot Facebook (frequenza standard: 3/sett ~12/mese)
- Invocata come cross-post da Instagram quando un contenuto IG ha buon engagement e merita ri-distribuzione su FB
- Mai auto-trigger

Tempo target: **3-5 minuti**.

---

## 2. Output finale atteso

**File Markdown Buffer-ready** consegnato al MM:

```markdown
---
canale: facebook_pagina_brand
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. mar 10:00, gio 15:00 â€” finestre demografiche FB 35+]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Caso Reale]
firma: brand Advisory+
visual_brief: brief_visual_[id].md
url_in_commento: [URL completo, se applicabile]
cross_post_origin: [Instagram post X | nessuno]
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

# CAPTION (corpo del post)
[150-200 parole Â· tono caldo Â· paragrafi brevi 2-3 frasi Â· emoji moderate 1-2 per post Â· interruzioni grafiche con riga vuota]

# HASHTAG (blocco separato â€” FB ne tollera pochi)
#AdvisoryPlus #[tema1] #[tema2] #[tema3]

# PRIMO COMMENTO (URL + frase di accompagnamento)
[Frase + URL]
```

---

## 3. Specifiche Facebook pagina brand

### Lunghezza
- **150-200 parole** (FB premia post piÃ¹ brevi di LinkedIn, demografica 35+ scrolla rapida)
- Sopra 200 = "Vedi altro" si attiva, engagement crolla
- Sotto 100 = troppo "shallow", non genera interazione

### Tono
- **Caldo, accessibile, conversazionale**
- PiÃ¹ familiare di LinkedIn ma **mai colloquiale-volgare**
- Domande aperte ai lettori funzionano bene ("Vi Ã¨ mai capitato?", "Cosa ne pensate?")
- **Posizionamento nazionale**: zero riferimenti territoriali (no "qui in Versilia", "noi della Toscana"), Brand Book v1.2 sez. 2

### Hashtag
- **3-5 hashtag** in blocco separato
- FB tollera pochi hashtag (sopra 5 = spammy)
- Mix: 1 brand (`#AdvisoryPlus`) + 2-4 tematici del pillar
- **NO hashtag locali**

### URL
- **MAI nel corpo** (penalizzazione come LinkedIn)
- URL in **primo commento** con frase di accompagnamento
- L'unica eccezione: link nativo a video FB giÃ  caricato, che genera autoplay (no link esterni nel corpo)

### Visual
- **Cover 1200Ã—630** (landscape FB, leggermente diversa dal 1200Ã—628 LinkedIn â€” puÃ² essere adattata dalla stessa)
- Brief visual prodotto da skill `adv-image-facebook-post` (Sessione 4)
- Tipologia: foto/illustrazione che inviti al click + min testo on-image (max 5 parole)

### Orario di pubblicazione raccomandato
- **Mar-Mer-Gio**: 10:00-11:00 (pausa caffÃ¨) e 15:00-17:00 (pausa pomeridiana)
- **Sab-Dom**: 09:00-11:00 (engagement weekend buono per voce Caso Reale storytelling)
- **Lun mattina + Ven pomeriggio**: evitare

---

## 4. Mapping voce per pillar su Facebook

| Pillar | Voce primaria | Note |
|---|---|---|
| P1 Educazione (always-on) | Spiegato Facile | Tono caldo, esempi domestici |
| P3 News di settore (always-on) | **Spiegato Facile** (NO Analisi) | Pubblico FB non ha appetito per Analisi tecnica â€” riformulare in spiegazione divulgativa |
| P4 Famiglia & Vita | Spiegato Facile / Caso Reale | Pubblico FB risuona molto con storie famiglia |
| P5 AnzianitÃ  & LTC | Caso Reale | Storytelling LTC funziona bene su FB |
| P6 Risparmio & Investimento | Spiegato Facile | Mai Analisi su FB |
| P7 Tutela Legale | Spiegato Facile / Caso Reale | |
| P8 Casa & Patrimonio | Spiegato Facile / Caso Reale | |
| P9 Imprese & Professionisti | Skip o raro | Pubblico FB non Ã¨ la demografica B2B â€” riservare a LinkedIn |
| P10-12 Specialty | Caso Reale | Storytelling specialty su FB con sub-identity visual |

**Mai su Facebook**: Badvisor (registro non funziona) Â· Analisi tecnica (riformulare in Spiegato Facile divulgativo).

---

## 5. Pattern cross-posting da Instagram

Quando un contenuto Instagram performa bene e merita cross-posting su Facebook:

### Carosello IG â†’ Post FB singolo
- Pick: 1-2 slide piÃ¹ rappresentative del carosello come immagine
- Caption FB: caption IG **riadattata** (piÃ¹ breve, meno emoji, hashtag ridotti a 3-5)
- Link al carosello IG originale nel primo commento (cross-traffic)

### Reel IG â†’ Reel FB nativo
- Cross-posting nativo via Meta Business Suite (non richiede skill aggiuntiva)
- Caption Reel FB = caption IG adattata (FB sopporta caption Reel un po' piÃ¹ lunga di IG)

### Stories IG â†’ NON cross-post automatico
- Stories sono effimere, cross-posting automatico le rende ridondanti
- Eccezione: highlight permanente cross-postato come post singolo FB con visual + testo riassuntivo

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (pillar, voce, tema, data, eventuale cross_post_origin Instagram)
2. **Eseguire kickoff**
3. **Verificare** se il pillar richiede skip (P9 Imprese â€” proporre rimando a LinkedIn) o riformulazione voce (P3 News con Analisi â†’ Spiegato Facile divulgativo)
4. **Se cross-post da IG**: leggere il post IG sorgente in `Output_approvati/`
5. **Invocare voce editoriale** via Task tool con brief mirato per Facebook:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale Facebook brand Â· lunghezza 150-200p Â· tono caldo conversazionale Â· zero riferimenti territoriali Â· 2 varianti."
   )
   ```
6. **Ricevere** testo (2 varianti)
7. **Applicare formattazione Facebook**:
   - Verifica lunghezza 150-200p (se fuori range â†’ rilancia)
   - Tono caldo verificato (se troppo asciutto â†’ richiedi riformulazione)
   - Zero riferimenti territoriali verificati (grep Versilia/Apuana/Toscana/Camaiore/Viareggio/Pietrasanta/Massa/Carrara)
   - Estrai URL dal corpo â†’ primo commento
   - 3-5 hashtag (lookup `config/brand.json`)
   - 1-2 emoji moderate
8. **Produrre brief visual** (handoff a skill `adv-image-facebook-post` Sessione 4)
9. **Invocare Compliance Officer** via Task tool per gate finale
10. **Se ðŸŸ¡**: applicare riformulazione, ri-check
11. **Se ðŸŸ¢**: consegna al MM

---

## 7. Casi particolari

### Post di rilancio articolo blog
- Cover articolo riadattata in formato FB (1200Ã—630)
- Caption = teaser 150p + chiusura "Articolo completo in primo commento"
- URL in primo commento

### Post specialty stagionale (es. P10 Mare in giugno)
- Visual coerente con sub-identity specialty (accent ocra Warning â‰¤5%, Brand Book v1.2 sez. 8.1)
- Tono Caso Reale storytelling adatto a FB

### Post di richiamo evento (es. webinar Advisory+)
- Visual hero con data + titolo evento
- Caption con chiamata all'azione "Iscriviti" + URL evento in primo commento
- Tag @ pagina partner se evento co-marketing

---

## 8. Cosa NON fare mai

- âŒ **URL nel corpo del post**
- âŒ **Riferimenti territoriali** (Versilia/Apuana/Toscana â€” posizionamento nazionale)
- âŒ **Badvisor su pagina FB** (registro non funziona su demografica FB)
- âŒ **Analisi tecnica con apparato citazionale fitto** (riformulare in Spiegato Facile divulgativo)
- âŒ **Hashtag oltre 5** (FB li interpreta come spam)
- âŒ **Emoji a cascata** (1-2 max per post, mai paragrafi di emoji)
- âŒ **Lunghezza oltre 200p** (engagement crolla)
- âŒ **Tono volgare/colloquiale-bar** (Advisory+ Ã¨ consulenziale anche su FB)
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Loghi mandatarie** nel visual del post (solo in disclosure)
- âŒ **Cross-posting automatico Stories** (rendono ridondante il feed)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento nazionale Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance Â· sez. 8 Design System)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/03_Social_Media_Manager.md` Â· `/01_Team/02_Copywriter.md`
3. `config/brand.json` (hashtag per pillar, mapping voce-canale, frequenze FB pagina)
4. `config/pillars-of-month.json`
5. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-facebook-post â€” Sessione 3 Plugin Build â€” 2026-05-18*

