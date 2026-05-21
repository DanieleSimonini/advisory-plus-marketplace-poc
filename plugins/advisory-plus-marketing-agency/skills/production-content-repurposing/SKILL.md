---
name: production-content-repurposing
description: Massimizza il ROI di ogni contenuto pillar evergreen scomponendolo in 6-8 contenuti derivati su 8 canali in 2-4 settimane. Pattern di riuso codificato â€” 1 articolo blog 2000p â†’ 1 newsletter highlight + 2 post LinkedIn pagina + 1 post LinkedIn Daniele + 1 carosello IG 6-8 slide + 1 Reel 30-60s + 1 YouTube Short 60-90s + Stories set 3-5 slide + WhatsApp utility se applicabile. Ogni derivato mantiene voce coerente (puÃ² cambiare voce tra derivati: blog Analisi â†’ newsletter Spiegato Facile + Reel Badvisor) ma stesso pillar + stesso messaggio chiave. Output Markdown brief multi-canale che invoca le 10 skill content-* (Sessione 3) in cascata. Compliance check su ogni derivato (riformulazione cross-canale puÃ² introdurre claim ðŸ”´). Brand Strategist verifica coerenza messaggio cross-canale.
---
# â™»ï¸ Skill production-content-repurposing â€” Pattern riuso 1 â†’ 6-8 derivati

> **1 pillar evergreen â†’ 6-8 contenuti su 8 canali in 2-4 settimane. Voce puÃ² variare, messaggio resta.**

---

## 1. Quando triggera

- Invocata dal MM quando un articolo blog evergreen Ã¨ approvato e pubblicato, e merita una declinazione multi-canale (default: ogni pillar dominante del mese genera almeno 1 ciclo di repurposing dal suo articolo blog flagship)
- Invocata da `advisory-plus:strategia-month-plan` come default su articolo pillar mensile
- Invocata da `advisory-plus:strategia-campaign-30-60-90` come componente di una campagna tematica
- Invocata on-demand dal MM per articoli short che hanno avuto performance ottima (insight da `data-monthly-performance-report` Top 3)
- Mai auto-trigger: brief MM obbligatorio

Tempo target di esecuzione: **30-60 minuti** per brief multi-canale completo, poi 2-4 settimane per esecuzione effettiva delle skill chiamate.

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/production/[YYYY-MM-DD]_repurposing_[slug-articolo-base].md` + brief separati per ogni derivato:

```markdown
---
data: YYYY-MM-DD
articolo_base: [Output_approvati/04_Blog_THE_ADVISOR/YYYY-MM-DD_titolo.md]
pillar: P[N] [Nome]
messaggio_chiave: [1 frase 15-25 parole]
target_segmenti: [N1, N2, N3]
durata_ciclo_repurposing: 2-4 settimane
n_derivati_pianificati: 6-8
compliance_check_per_derivato: obbligatorio
---

## Messaggio chiave (1 riga)

[La frase che deve sopravvivere in ogni derivato â€” anche con voci diverse]

## Pattern di riuso applicato (timing su 2-4 settimane)

| Settimana | Giorno | Canale | Formato | Voce | Skill chiamata | Stato |
|---|---|---|---|---|---|---|
| Sett 0 | Mar 09:00 | Blog | Articolo 2000p | Caso Reale/Spiegato Facile/Analisi | (giÃ  pubblicato) | ðŸŸ¢ |
| Sett 0 | Ven 17:00 | Newsletter | Highlight 150p | Spiegato Facile | content-newsletter | ðŸ“ |
| Sett 1 | Mar 09:00 | LinkedIn Pagina | Post 250p (parte 1) | Spiegato Facile | content-linkedin-post-brand | ðŸ“ |
| Sett 1 | Gio 09:00 | LinkedIn Pagina | Post 250p (parte 2) | Caso Reale o Analisi | content-linkedin-post-brand | ðŸ“ |
| Sett 1 | Sab 10:00 | LinkedIn Daniele | Post 300p autoriale | Voce CEO autoriale | content-linkedin-post-daniele | ðŸ“ |
| Sett 2 | Mar 11:00 | Instagram | Carosello 6-8 slide | Spiegato Facile (didattico) | content-instagram-caption | ðŸ“ |
| Sett 2 | Gio 11:00 | Instagram | Reel 30-60s | Badvisor o Spiegato Facile | content-reel-script | ðŸ“ |
| Sett 2 | Sab 10:00 | Instagram | Stories set 3-5 slide | Spiegato Facile | content-stories-set | ðŸ“ |
| Sett 3 | Mar 10:00 | YouTube | Short 60-90s | Analisi o Spiegato Facile | content-youtube-video | ðŸ“ |
| Sett 3 | (event) | WhatsApp | Utility se pertinente | n/a | (n/a) | opzionale |

## Brief per ogni derivato

### 1. Newsletter highlight
- Voce: Spiegato Facile
- Lunghezza: 150p (1 dei 3 highlight della newsletter mensile)
- Estratto: [3-4 punti chiave dell'articolo + link "Leggi l'articolo completo"]
- Skill da invocare: `advisory-plus:content-newsletter` (per la newsletter intera del mese, questo Ã¨ 1 highlight)

### 2-3. LinkedIn Pagina post (2 parti)
- Voce parte 1: Spiegato Facile (apertura concettuale)
- Voce parte 2: Caso Reale o Analisi (dettaglio pratico o dato)
- Lunghezza: 250p ciascuno
- Skill: `advisory-plus:content-linkedin-post-brand`

### 4. LinkedIn Daniele
- Voce: Voce CEO autoriale + opinione/riflessione personale
- Lunghezza: 300p
- Skill: `advisory-plus:content-linkedin-post-daniele` (verifica ratio 80/20 e tetto Badvisor cumulato)

### 5. Instagram carosello
- Voce: Spiegato Facile (didattico, perfetto per slide)
- 6-8 slide: 1 cover + 5-7 contenuto + 1 CTA
- Skill: `advisory-plus:content-instagram-caption` con flag carosello + Art Director per slide design

### 6. Instagram Reel
- Voce: Badvisor (se pillar lo regge â€” sez. 4 cosa NON fare) o Spiegato Facile alternativo
- 30-60s con hook in 3 sec
- Skill: `advisory-plus:content-reel-script` (verifica tetto Badvisor 20% cumulato)

### 7. Instagram Stories set
- Voce: Spiegato Facile
- 3-5 slide con sticker IG nativi (poll/question/link verso articolo)
- Skill: `advisory-plus:content-stories-set`

### 8. YouTube Short
- Voce: Analisi (canale professional) o Spiegato Facile
- 60-90s con HeyGen avatar generico + Remotion intro
- Skill: `advisory-plus:content-youtube-video` (variante Short)
- AI disclosure obbligatoria

### 9. (opzionale) Facebook
- Voce: Spiegato Facile (registro caldo)
- Lunghezza: 150-200p
- Riuso del LinkedIn Pagina parte 1 con leggera riformulazione
- Skill: `advisory-plus:content-facebook-post`

### 10. (opzionale) WhatsApp utility
- Solo se il tema ha implicazione utility per clienti esistenti (es. articolo su normativa nuova â†’ messaggio "novitÃ  che ti riguarda")
- Tono utility, mai promozionale
- Skill: (manuale, no skill content-* dedicata in v1.1 plugin)

## Variazioni di voce ammesse cross-canale

| Canale | Voce articolo base | Voce derivato canale | Razionale |
|---|---|---|---|
| Blog | Analisi (apparato citazionale) | â€” | â€” |
| Newsletter | â€” | Spiegato Facile | divulgazione highlight |
| LI Pagina | â€” | Spiegato Facile + Caso Reale | varietÃ  mista in 2 post |
| LI Daniele | â€” | Voce CEO autoriale | personal angle, opinione |
| IG carosello | â€” | Spiegato Facile | format visivo didattico |
| IG Reel | â€” | Badvisor (se compatibile) o Spiegato Facile | rompi-scroll |
| IG Stories | â€” | Spiegato Facile | rapid-fire highlight |
| YouTube Short | â€” | Analisi sintetico o Spiegato Facile | canale professional |
| Facebook | â€” | Spiegato Facile | pubblico piÃ¹ adulto |

âš ï¸ **Voci NON ammesse cross-canale**:
- Caso Reale dolente (Pillar 5 LTC, Pillar 7 Tutela legale famiglie) **non si riformula in Badvisor** (vietato Brand Book v1.2 sez. 4 â€” regola d'oro "paradosso vs sistema, mai vs lettore")
- Analisi tecnica **non si riformula in Facebook** (registro mismatch â€” Brand Book v1.2 sez. 4 + sez. 5)
- Badvisor su brochure corporate o YouTube principale (canale professional)

## Compliance check (su ogni derivato)

Ogni derivato passa il gate-doppio Compliance Officer + Brand Strategist:
- Disclaimer RUI applicato dove canale lo richiede
- Denominazione mandatarie corretta
- Tetto Badvisor cumulato verificato
- AI disclosure se HeyGen avatar usato (Reel Â· YouTube Short)
- "Caso reale, nomi di fantasia" se Caso Reale
- Apparato citazionale Analisi (fonte+anno)
- Posizionamento nazionale (no riferimenti territoriali)

## Brand Strategist check coerenza

- Messaggio chiave preservato in ogni derivato
- Pillar resta P[N] in tutti i canali (no drift)
- Voci coerenti con Mappa voceâ†”canale Brand Book v1.2 sez. 4
- Ratio firma 80/20 monitorato (LI Daniele aggiunge 1 post personale)
- Quota Badvisor mensile aggiornata
```

---

## 3. Le 6-8 declinazioni â€” pattern operativo

### 3.1 Newsletter highlight (estratto)
Estratto 150p dell'articolo blog, formato come 1 dei 3 highlight della newsletter mensile. Voce di solito Spiegato Facile (anche se articolo Ã¨ Analisi â†’ highlight semplifica). Link "Leggi l'articolo completo" CTA primaria.

### 3.2 LinkedIn Pagina Â· 2 post (apertura + approfondimento)
- **Post 1** (Sett 1 mar): apertura concettuale del tema, 250p, Spiegato Facile. Hook + 1 dato/affermazione + CTA "Approfondisci sul blog".
- **Post 2** (Sett 1 gio): caso reale o dato specifico, 250p, voce alternativa. Hook + storytelling/dato + link al blog (primo commento).

### 3.3 LinkedIn Daniele Â· 1 post autoriale
Voce CEO autoriale 300p. Daniele commenta in prima persona il tema, prendendo posizione/dando opinione. Tag @Advisory+ in chiusura. Pubblicazione semi-manuale (Daniele clicca personalmente, decisione CEO 2026-05-16).

### 3.4 Instagram carosello Â· 6-8 slide
Carosello didattico Spiegato Facile. 1 slide cover (titolo + hook) + 5-7 slide contenuto (1 concetto per slide, â‰¤30 parole) + 1 slide CTA "Vai al blog" o "Salva il post".

### 3.5 Instagram Reel Â· 30-60s
Reel con hook in 3 sec. Stack: Remotion tipografico (default) o HeyGen avatar (con AI disclosure). Sottotitoli burned-in. Voce Badvisor se tema lo regge, altrimenti Spiegato Facile.

### 3.6 Instagram Stories set Â· 3-5 slide
Set di 3-5 slide consecutive con sticker IG nativi (poll "lo sapevi?", question "ne vuoi sapere di piÃ¹?", link CTA "vai al blog"). Voce Spiegato Facile rapid-fire.

### 3.7 YouTube Short Â· 60-90s
Short verticale 9:16 con HeyGen avatar generico + Remotion intro/outro. Voce Analisi sintetica o Spiegato Facile. AI disclosure obbligatoria caption + on-screen. Sottotitoli auto + correzione manuale.

### 3.8 (opzionale) Facebook Â· 1 post
Riuso del LinkedIn Pagina post 1 con leggera riformulazione (tono piÃ¹ caldo, audience piÃ¹ adulta). 150-200p.

### 3.9 (opzionale) WhatsApp utility
Solo se il tema ha pertinenza utility per clienti esistenti (no broadcast newsletter â€” channel utility 1:1 in WA). Tono utility, mai promo.

---

## 4. Pattern di rotazione cadenza

### Pattern A â€” "Burst" (2 settimane intense)
- Sett 0: Blog + Newsletter highlight
- Sett 1: LI Pagina Ã— 2 + LI Daniele
- Sett 2: IG carosello + Reel + Stories
- Sett 3: YouTube Short (delay per render + AI disclosure compliance)

### Pattern B â€” "Slow burn" (4 settimane diluite)
- Sett 0: Blog
- Sett 1: Newsletter + LI Pagina post 1
- Sett 2: LI Pagina post 2 + LI Daniele
- Sett 3: IG carosello + Reel
- Sett 4: Stories + YouTube Short

### Decisione MM
Pattern A per pillar dominante del mese (massimo impact concentrato).
Pattern B per articoli short news o pillar background (diluito, no fatigue).

---

## 5. Anti-cannibalizzazione

âš ï¸ **Mai 2 derivati sullo stesso canale a meno di 24h di distanza** (rischio fatigue follower).
âš ï¸ **Newsletter highlight + LI Pagina post 1**: se entrambi escono stessa settimana, sfalsare di almeno 3 giorni (newsletter ven + LI mar).
âš ï¸ **Reel + Carosello IG**: mai stesso giorno (algoritmo IG penalizza).
âš ï¸ **YouTube Short se canale YouTube va in fase di calibrazione (mese 1-2)**: prioritÃ  ai video lunghi explainer, Short come complemento occasionale.

---

## 6. KPI repurposing (riferimento data-monthly-performance-report)

| KPI | Target a regime |
|---|---|
| ROI editoriale per ciclo (engagement totale derivati / engagement articolo base) | â‰¥3-5x |
| % articoli pillar che generano almeno 1 ciclo repurposing | 100% (default per pillar-of-month) |
| Cross-canale audience overlap | <30% (no eccesso di esposizione stessa audience) |
| Voce repurposing pertinente (Brand Strategist check) | 100% derivati passano check |
| Compliance check su derivati | 100% ðŸŸ¢ prima della pubblicazione |

---

## 7. Logica di esecuzione â€” passo-passo

1. **Ricevere brief MM** (articolo base + pillar + pattern A/B + canali da attivare)
2. **Cascata di contesto** (sez. 9)
3. **Lettura articolo base** in `Output_approvati/04_Blog_THE_ADVISOR/...`
4. **Estrarre messaggio chiave** (1 frase 15-25 parole che sopravvive in ogni derivato)
5. **Verificare tetti cumulati**:
   - Tetto Badvisor 20% mensile (se vogliamo Reel Badvisor, c'Ã¨ spazio?)
   - Ratio 80/20 firma Daniele (LI Daniele aggiungerÃ  1 post personale â€” quota rispettata?)
   - Frequenza per canale (Brand Book v1.2 sez. 5)
6. **Mappare derivati** secondo pattern scelto (A o B) + tabella canale Ã— giorno
7. **Comporre brief specifici** per ogni derivato (cosa dire Â· voce Â· CTA Â· lunghezza Â· hashtag Â· visual)
8. **Inserire derivati nel calendario** editoriale (handoff a `production-editorial-calendar`)
9. **Per ogni derivato in scadenza**: invoca skill `content-*` corrispondente via Task tool con brief specifico
10. **Compliance gate-doppio** su ogni derivato prima di Programmato
11. **Brand Strategist check coerenza** cross-canale (messaggio chiave preservato)
12. **Consegna al MM** del brief complessivo + tracking stato per derivato

---

## 8. Cosa NON fare mai

- âŒ **Riformulare Caso Reale dolente in Badvisor** (Pillar 5 LTC, Pillar 7 tutela legale famiglie â€” vietato Brand Book v1.2 sez. 4 regola d'oro)
- âŒ **Cambiare pillar tra derivati** (deve restare P[N] in tutti i canali)
- âŒ **Cambiare messaggio chiave** (voce puÃ² variare, messaggio no)
- âŒ **Pubblicare 2 derivati stesso canale <24h** (fatigue)
- âŒ **Saltare Compliance check su singoli derivati** (riformulazione cross-canale puÃ² introdurre claim ðŸ”´)
- âŒ **Sforare tetto Badvisor 20%** in ciclo repurposing (verifica cumulata)
- âŒ **Ratio 80/20 sballato** (se LI Daniele aggiunge 1, verifica quota mensile altri soci)
- âŒ **Analisi tecnica su Facebook** (registro mismatch)
- âŒ **Badvisor su YouTube principale o brochure** (canale professional)
- âŒ **Riferimenti territoriali** in qualsiasi derivato
- âŒ **Loghi mandatarie** in body (solo disclosure footer)
- âŒ **Copia-incolla letterale** dell'articolo base in altri canali (sempre adattamento canale-specifico)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pianificare il repurposing, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 5 strategia canali Â· sez. 6 Pillar Map Â· sez. 7 Compliance)
2. `/01_Team/00_Marketing_Manager.md` + `/01_Team/09_Content_Producer.md` + `/01_Team/01_Brand_Strategist.md`
3. `config/brand.json` (canali, voci, tetti, mapping voce-canale-pillar)
4. Articolo base in `Output_approvati/04_Blog_THE_ADVISOR/`
5. Calendario editoriale corrente `/05_Calendario_editoriale/[YYYY-MM]_calendario.md` (per slot disponibili + tetti cumulati)
6. `Output_approvati/production/` cicli repurposing precedenti (per pattern di successo)
7. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:production-content-repurposing â€” Sessione 6 Plugin Build â€” 2026-05-21*

