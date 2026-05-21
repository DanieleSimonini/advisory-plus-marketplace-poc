---
name: content-linkedin-post-brand
description: Compone un post pronto da pubblicare sulla pagina aziendale LinkedIn Advisory+ (brand, non profilo personale). Orchestra: voce editoriale (Spiegato Facile sempre per Educazione + Pillar rotanti livello base Â· Analisi per Pillar 3 News di settore + Pillar 9 Imprese & Professionisti Â· Caso Reale per pillar esperienziali) â†’ invoca la skill voce-* corretta via Task tool con brief mirato â†’ riceve testo "in-context" (architettura voci stateless Sessione 2) â†’ applica formattazione LinkedIn brand (200-280 parole, 5-7 hashtag mix tematici, URL in primo commento mai nel corpo per non penalizzare algoritmo LI, firma brand Advisory+) â†’ produce brief visivo cover 1200Ã—628 da passare a skill visual Sessione 4 â†’ passa output a Compliance Officer per gate finale â†’ consegna al MM file Markdown Buffer-ready (caption + hashtag blocco separato + orario suggerito + brief visual + URL primo commento). MM Ã¨ single point of write â€” questa skill produce e consegna, MM salva in Output_approvati/ con naming standard.
---
# ðŸ’¼ Skill content-linkedin-post-brand â€” Post pagina aziendale LinkedIn Advisory+

> **Orchestra voce + format LinkedIn brand + visual brief + compliance. Pattern stateless: invoca voce â†’ riceve testo â†’ formatta â†’ consegna al MM.**

---

## 1. Quando triggera

- Invocata dal **Marketing Manager** durante l'esecuzione settimanale (week-fri pianifica, week-mon esegue) per ogni slot LinkedIn brand del piano
- Invocata dal **MM** su richiesta diretta del CEO o per spunto urgente (`Spunti_CEO.md`)
- Mai auto-trigger: serve un brief operativo del MM con (pillar Â· voce Â· tema Â· eventuali ancoraggi)

Tempo target di esecuzione: **3-5 minuti**.

---

## 2. Output finale atteso

**File Markdown Buffer-ready** consegnato al MM (che lo salva in `Output_approvati/` con naming standard `[YYYY-MM-DD]_LinkedIn-brand_[tema]_[variante].md`):

```markdown
---
canale: linkedin_pagina_brand
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. mar 10:00, mer 12:00, gio 18:00]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Analisi / Caso Reale]
firma: brand Advisory+
visual_brief: brief_visual_[id].md (in cartella adv-image-linkedin-post)
url_in_commento: [URL completo, se applicabile]
compliance: ðŸŸ¢ / ðŸŸ¡ (con nota) / ðŸ”´ BLOCCATO
---

# CAPTION (corpo del post)
[200-280 parole Â· testo piano Â· no link URL nel corpo Â· ritmo a paragrafi brevi Â· interruzioni grafiche con riga vuota Â· eventuale lista numerata Â· tono coerente con la voce scelta]

# HASHTAG (blocco separato, da incollare in coda alla caption al momento del posting)
#AdvisoryPlus #[tema1] #[tema2] #[tema3] #[tema4] #[tema5]

# PRIMO COMMENTO (da pubblicare manualmente subito dopo il post)
[URL completo + eventuale call-to-conversation]
```

---

## 3. Specifiche LinkedIn pagina brand

### Lunghezza
- **200-280 parole** (sweet spot algoritmo LI per dwell-time)
- Sotto 200 = troppo breve, perde profonditÃ 
- Sopra 280 = scatta il "...altro" e crolla l'engagement

### Hashtag
- **5-7 hashtag** in blocco separato a fine caption
- Mix: 1-2 hashtag brand fissi (`#AdvisoryPlus` + 1 brand-tagline opzionale) + 3-5 tematici del pillar
- Lista hashtag tematici per pillar in `config/brand.json` sez. `hashtag_per_pillar`
- **NO hashtag locali** (Versilia/Apuana/Toscana â†’ vietati, posizionamento nazionale Brand Book v1.2)

### URL
- **MAI URL nel corpo del post** (algoritmo LinkedIn penalizza pesantemente)
- URL sempre in **primo commento**, da pubblicare manualmente entro 60 sec dal posting
- Pattern primo commento: 1 frase di accompagnamento + URL nudo (LI auto-renderizza preview)

### Firma
- **Brand Advisory+** (la pagina firma da sÃ©, no firma testuale in calce)
- Per contenuti che richiamano un socio specifico: chiusura con riferimento ("L'approfondimento Ã¨ del nostro [Nome Cognome], referente [pillar/area]"), mai firma personale

### Visual
- **Cover 1200Ã—628** (formato landscape LinkedIn ottimizzato)
- Brief visual prodotto da skill `adv-image-linkedin-post` (Sessione 4)
- Tipologia: Cover Blog System se richiama articolo Â· grafica didattica se Spiegato Facile Â· dato visualizzato se Analisi Â· foto stock generica se Caso Reale
- Se contenuto richiama articolo blog: usa la stessa cover dell'articolo per coerenza visiva cross-canale

### Orario di pubblicazione raccomandato
- **Mar-Mer-Gio**: finestre 08:00-10:00 e 17:00-19:00 (peak engagement B2B LI)
- **Lun**: solo se contenuto urgente (lun mattina = inbox congestionate)
- **Ven pomeriggio + weekend**: solo per contenuti evergreen non time-sensitive

---

## 4. Mapping voce per pillar

| Pillar | Voce primaria | Voce secondaria | Note |
|---|---|---|---|
| P1 Educazione (always-on) | Spiegato Facile | â€” | Sempre didattico-narrativo |
| P2 Voce CEO (always-on) | n/a | n/a | Pillar 2 = profilo personale Daniele, NON pagina brand. Skip. |
| P3 News di settore (always-on) | Analisi | Spiegato Facile (per news divulgative) | Apparato citazionale obbligatorio se Analisi |
| P4 Famiglia & Vita | Spiegato Facile | Caso Reale | |
| P5 AnzianitÃ  & LTC | Caso Reale | Spiegato Facile | |
| P6 Risparmio & Investimento | Spiegato Facile (base) / Analisi (professional layer) | â€” | No promesse rendimenti garantiti |
| P7 Tutela Legale | Caso Reale | Spiegato Facile | |
| P8 Casa & Patrimonio | Spiegato Facile | Caso Reale | |
| P9 Imprese & Professionisti | Analisi | Spiegato Facile (entry) | Pubblico professional |
| P10 Mare & Yacht (specialty) | Caso Reale | Analisi (taglio fiscale/normativo) | |
| P11 Arte & Patrimonio (specialty) | Caso Reale | Analisi (donazioni, agevolazioni) | |
| P12 Enti religiosi & Terzo Settore (specialty) | Analisi | Caso Reale | |

**Badvisor su pagina brand: NO** (Badvisor Ã¨ voce di rottura riservata a LinkedIn personale Daniele + Instagram Reel + occasionali Stories). Pagina brand mantiene registro consulenziale.

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM con: pillar Â· voce primaria suggerita Â· tema Â· eventuale ancoraggio (Spunti CEO, news, evergreen) Â· data pianificata
2. **Eseguire kickoff** (skill `advisory-plus:kickoff`) per contesto workspace
3. **Leggere** `config/brand.json` (hashtag per pillar, mapping voce-canale)
4. **Leggere** `config/pillars-of-month.json` per pillar dominante mese corrente
5. **Invocare voce editoriale** via Task tool:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale LinkedIn pagina brand Â· lunghezza 200-280p Â· ancoraggio [Y]. Produrre 2 varianti."
   )
   ```
6. **Ricevere** testo "in-context" (2 varianti)
7. **Applicare formattazione LinkedIn**:
   - Verifica lunghezza 200-280p (se fuori range â†’ rilancia voce con vincolo stretto)
   - Estrai eventuale URL dal corpo â†’ spostalo in primo commento
   - Genera blocco hashtag 5-7 (lookup `config/brand.json`)
   - Aggiungi metadati frontmatter (canale, data, orario, pillar, voce, firma, visual_brief)
8. **Produrre brief visual** (handoff): scrivi nota strutturata da passare a skill `adv-image-linkedin-post` (Sessione 4): "Cover 1200Ã—628 Â· stile [didattico/dato/storia/cover-blog] Â· palette Navy 700 + Teal 500 Â· font Inter Tight Â· contenuto [riepilogo 1 frase del post] Â· no foto identificative Â· no testo eccessivo (max 7 parole on-image)"
9. **Invocare Compliance Officer** via Task tool per gate finale:
   ```
   Task(
     subagent_type: "advisory-plus:compliance-officer",
     prompt: "Check finale post LinkedIn brand pillar [N]. Verifica: claim, denominazione mandatarie se citate, disclaimer (NON richiesto su LinkedIn post â€” solo bio), uso simboli RUI, AI Act se applicabile."
   )
   ```
10. **Ricevere semaforo** (ðŸŸ¢/ðŸŸ¡/ðŸ”´) + eventuali note di riformulazione
11. **Se ðŸŸ¡**: applicare riformulazione proposta da Compliance e rilanciare check (1 sola iterazione)
12. **Se ðŸ”´**: blocca, segnala al MM, non consegnare
13. **Se ðŸŸ¢**: consegna al MM file Markdown completo (frontmatter + caption + hashtag + primo commento)

---

## 6. Casi particolari

### Post di richiamo a articolo blog appena pubblicato
- Cover identica all'articolo (coerenza visiva)
- Caption = teaser dell'articolo (250p) con hook + 3 bullet di anticipazione + chiusura "Articolo completo in primo commento"
- URL articolo in primo commento

### Post di rilancio news di settore (Pillar 3, voce Analisi)
- Apparato citazionale obbligatorio in caption (fonte+anno inline)
- Hashtag includono nome ente/regolatore (`#IVASS` `#ANIA` `#COVIP` se rilevante)
- Tono asciutto, niente emoji decorative (Analisi non usa emoji nel corpo)

### Post con tag a un socio referente
- Chiusura: "L'approfondimento Ã¨ di [Nome Cognome], referente Pillar [N] Â· per domande dirette, contatti su nostro sito" (URL sito in primo commento)
- Mai tag al profilo personale del socio dal post brand (mantiene separazione voce brand vs voce personale)

### Post di richiamo specialty drop (P10-P11-P12 attiva)
- Hashtag specialty inclusi (es. `#Yacht` `#MareSicurezza` per P10)
- Visual coerente con sub-identity specialty (Brand Book v1.2 sez. 8.1, accent ocra Warning â‰¤5%)

---

## 7. Cosa NON fare mai

- âŒ **URL nel corpo del post** (penalizzazione algoritmica garantita)
- âŒ **Hashtag locali** (Versilia/Apuana/Toscana â€” posizionamento nazionale)
- âŒ **Firma personale di un socio** sul post pagina brand (la pagina firma da sÃ©)
- âŒ **Tag a profili personali** dal post brand
- âŒ **Badvisor su pagina brand** (voce di rottura riservata a LinkedIn Daniele personale + IG Reel + Stories)
- âŒ **Lunghezza fuori range 200-280p** (se la voce supera, rilanciare con vincolo)
- âŒ **Saltare gate Compliance** (il MM Ã¨ single point of write, ma compliance gate Ã¨ obbligatorio prima della consegna al MM)
- âŒ **Promesse rendimenti garantiti** o claim assoluti (Compliance lo bloccherÃ  comunque, ma evita di proporli)
- âŒ **Citare prezzi specifici di prodotto** senza contesto
- âŒ **Loghi mandatarie** in visual brand (solo in disclosure footer di brochure/blog/sito)
- âŒ **Emoji decorative** in voce Analisi (Spiegato Facile/Caso Reale ne tollerano 1-2 max per post)
- âŒ **Tono commerciale aggressivo** ("Contattaci subito!", "Non perdere l'occasione!") â€” Advisory+ Ã¨ consulenziale

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance Â· sez. 8 Design System)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/03_Social_Media_Manager.md` Â· `/01_Team/02_Copywriter.md`
3. `config/brand.json` (hashtag per pillar, mapping voce-canale, frequenze LinkedIn pagina)
4. `config/pillars-of-month.json` (pillar dominante mese corrente)
5. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:content-linkedin-post-brand â€” Sessione 3 Plugin Build â€” 2026-05-18*

