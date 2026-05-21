---
name: seo-content-gap
description: Identifica gap di copertura SEO del blog THE ADVISOR rispetto ai competitor italiani del settore assicurativo (broker indipendenti di pari taglia + compagnie dirette + grandi comparatori). Restituisce 10-20 opportunitÃ  di nuovi articoli/pillar non ancora coperti dal nostro blog ma con volume keyword interessante e match con un pillar Brand Book v1.2. Usa WebFetch per consultare SERP italiane e leggere indice contenuti dei competitor. Ogni gap proposto deve agganciare almeno un pillar (no temi orfani). Trigger: invocata mensilmente da month-plan in fase di pillar-of-month setup, o on-demand dal MM per planning trimestrale.
---
# ðŸ” Skill seo-content-gap â€” Gap analysis vs competitor SEO

> **Identifica cosa scrivono i competitor che noi non copriamo. Ogni gap aggancia un pillar Brand Book v1.2. Output: lista priorizzata 10-20 opportunitÃ .**

---

## 1. Quando triggera

- Invocata mensilmente da `advisory-plus:strategia-pillar-of-month-setup` per integrare il piano editoriale del mese
- Invocata trimestralmente in chat 01 Strategia come supporto a planning lungo
- Invocata on-demand dal MM quando un pillar appare "saturo" sul nostro blog e serve nuova materia
- Mai auto-trigger: brief MM o skill chiamante obbligatori

Tempo target di esecuzione: **15-30 minuti** (piÃ¹ lungo se WebFetch su 5+ competitor).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/seo/[YYYY-MM-DD]_content-gap_[scope].md`:

```markdown
---
data: YYYY-MM-DD
scope: [mese | trimestre | pillar specifico | tutto blog]
competitor_analizzati: [lista 3-5 competitor]
caveat_metodologico: [es. "WebFetch su SERP google.it Â· validare volume con strumento reale"]
---

## Executive Summary (3-5 righe)

[Sintesi panorama gap + top 3 prioritÃ  + caveat]

## Top 10-20 opportunitÃ  di content gap

| # | Tema proposto | Pillar match | Voce primaria suggerita | Lunghezza | PrioritÃ  | Razionale | Competitor che lo copre |
|---|---|---|---|---|---|---|---|
| 1 | [...] | P[N] | Spiegato Facile / Analisi / Caso Reale | 1500p | ðŸ”¥ Alta | [perchÃ© vale la pena] | [competitor1, competitor2] |
| ... | ... | ... | ... | ... | ... | ... | ... |

## Cluster proposti (topic hub)

**Cluster A:** [nome]
- Pillar: P[N]
- Hub: [titolo pillar]
- Spoke: [3-5 articoli satellite]
- Razionale: [perchÃ© cluster utile]

**Cluster B:** [nome]
- [...]

## Quick win (24-48h preparazione)

[1-3 articoli short news/Analisi reattivi a normativa o sentenza recente con poca copertura competitor]

## Strategic plays (3-6 mesi)

[1-2 cluster pillar evergreen che richiedono investimento ma posizionano Advisory+ come autoritÃ  su una nicchia]

## Caveat metodologico

[Analisi qualitativa basata su WebFetch SERP italiane + ispezione menu/categorie competitor. Volumi keyword stimati, validare con Ahrefs/Semrush prima di investimento SEO importante.]
```

---

## 3. Competitor di riferimento

### Categoria A â€” Broker indipendenti di pari taglia (3-4)
Studi medio-piccoli con blog attivo, copertura nazionale o multi-regionale. Esempi tipici (verifica WebFetch ad ogni run):
- Broker indipendenti con blog editoriale strutturato
- Studi con presenza LinkedIn pagina attiva
- Studi con specializzazione tutela legale o LTC (concorrenza diretta nostra)

### Categoria B â€” Compagnie dirette principali (2-3)
Compagnie con blog/sezione editoriale (Generali, Cattolica, Allianz, Unipol, Reale Mutua, Genertel, ConTe, ecc.). Hanno budget editoriale alto, contenuti deep ma corporate.

### Categoria C â€” Grandi comparatori (1-2)
Facile.it, Segugio.it, Prima.it. Volume keyword altissimo, contenuti SEO-driven ma poco autoriali. Difficile competere su keyword broad, ma opportunitÃ  su long-tail editoriale.

### Categoria D â€” Voce autoriale settore (1-2, opzionale)
Blog/newsletter di consulenti/analisti indipendenti (es. Plus24, IlSole24Ore Insurance, Insurance Trade). PiÃ¹ giornalismo settoriale, opportunitÃ  di citazione/repurposing nostra voce Analisi.

**Mai includere come competitor:**
- Compagnie mandatarie nostre (Generali Italia â€“ Cattolica Â· DAS Â· UCA Â· Europ) in modo denigratorio
- Studi locali Versilia/Apuana in posizionamento territoriale (nazionale)

---

## 4. Logica di esecuzione â€” 6 fasi

### Fase 1 â€” Selezione competitor
Brief MM definisce scope (mese Â· trimestre Â· pillar specifico).
- Default: 3 broker indipendenti + 2 compagnie dirette + 1 comparatore
- Per pillar specifico: aggiungere 1 specialista del pillar (es. P5 LTC â†’ blog focus LTC; P12 Terzo Settore â†’ portali ETS)

### Fase 2 â€” Ricognizione contenuti competitor (WebFetch)
Per ogni competitor:
- Fetch homepage e sezione blog/insights
- Estrarre lista categorie/tag editoriali
- Estrarre 10-20 titoli articoli piÃ¹ recenti o piÃ¹ visibili
- Annotare keyword apparenti dai titoli (no inferenza fantasiosa)

### Fase 3 â€” Mapping copertura nostra
- Leggere `Output_approvati/` blog precedenti
- Estrarre keyword primarie giÃ  coperte
- Costruire mappa "pillar Ã— tema coperto" del nostro blog

### Fase 4 â€” Identificazione gap
Per ogni tema competitor:
- Match con pillar Brand Book v1.2 (1-12) â†’ se nessun pillar matcha, SCARTARE (no temi orfani)
- Verificare se giÃ  coperto da noi â†’ se sÃ¬, SCARTARE
- Verificare se compliance OK (no rendimenti garantiti, no claim ðŸ”´) â†’ se no, SCARTARE
- Verificare se in linea con posizionamento nazionale â†’ se territoriale, SCARTARE
- Se passa i 4 filtri: aggiungere alla shortlist gap

### Fase 5 â€” Priorizzazione
Ogni gap valutato su 3 dimensioni:
- **Volume opportunitÃ ** (qualitativo: Bassa / Media / Alta) â†’ basato su quanti competitor lo coprono
- **Coerenza brand** (qualitativo: Bassa / Media / Alta) â†’ aderenza pillar + voce + posizionamento
- **DifficoltÃ  esecuzione** (qualitativo: Bassa / Media / Alta) â†’ tempo redazione + apparato citazionale + visual

PrioritÃ  composita:
- ðŸ”¥ **Alta** = (Volume Alto OR Coerenza Alta) AND DifficoltÃ  â‰¤ Media
- ðŸŸ¢ **Media** = Volume Media + Coerenza Media + DifficoltÃ  variabile
- ðŸ”µ **Bassa** = Volume Bassa OR DifficoltÃ  Alta (parking, riprendere se altro priorita esaurito)

### Fase 6 â€” Clustering e delivery
Raggruppare gap in cluster topic hub dove possibile (vedi seo-keyword-research per pattern hub+spoke). Distinguere quick win (24-48h) da strategic plays (3-6 mesi). Caveat metodologico esplicito.

---

## 5. Filtri obbligatori (pre-inclusione di un gap nella shortlist)

âœ… **Aggancio pillar obbligatorio** â†’ ogni gap deve mappare almeno 1 dei 12 pillar Brand Book v1.2 sez. 6.
âœ… **Posizionamento nazionale** â†’ no temi territoriali.
âœ… **Compliance baseline** â†’ no temi che richiedono claim ðŸ”´ vietati (rendimenti garantiti, comparazioni denigratorie con compagnie non mandatarie, prezzi specifici senza contesto).
âœ… **Non giÃ  coperto** â†’ verifica `Output_approvati/` blog.
âœ… **Coerenza voce** â†’ almeno una delle 4 voci editoriali deve essere applicabile al tema.

---

## 6. Casi particolari

### Gap su normativa/sentenza fresca (quick win)
- Voce primaria: Analisi
- Tempistica: 48h dalla pubblicazione evento
- Apparato citazionale obbligatorio
- PrioritÃ : ðŸ”¥ Alta (poca competizione, valore autorevolezza)

### Gap su pillar specialty (P10 Mare/P11 Arte/P12 Terzo Settore)
- Volume tipicamente piÃ¹ basso
- Coerenza brand altissima (differenziazione)
- PrioritÃ : ðŸŸ¢ Media o ðŸ”¥ Alta se cluster intero Ã¨ scoperto

### Gap "tema saturo competitor"
- Se 5+ competitor lo coprono ma noi no, valutare se aggiungere valore diverso (es. taglio Caso Reale dove gli altri fanno Spiegato Facile, o taglio Analisi tecnica dove gli altri sono divulgativi)
- PrioritÃ : ðŸŸ¢ Media se differenziazione chiara, ðŸ”µ Bassa se solo "me too"

### Gap orfano (no pillar match)
- SCARTARE
- Documentare nella sezione "Gap scartati per assenza pillar" del report con razionale â†’ puÃ² alimentare revisione Pillar Map in futura sessione Brand Identity

---

## 7. Compliance hooks

Quando un gap proposto include riferimento a compagnie mandatarie nostre o concorrenti, invoca `advisory-plus:compliance-mandatarie-check` per verifica denominazione corretta.

Quando un gap proposto Ã¨ su voce Analisi (normativa/sentenza), invoca `advisory-plus:compliance-citazioni-check` per validare la disponibilitÃ  di apparato citazionale fonti+anno.

Il Brand Strategist deve verificare il match pillar a 4 occhi prima di inclusione nel piano editoriale del mese.

---

## 8. Cosa NON fare mai

- âŒ **Proporre gap senza pillar match** (regola di posizionamento Brand Book v1.2 sez. 6)
- âŒ **Proporre temi territoriali** (scope nazionale)
- âŒ **Copiare titoli competitor parola per parola** â€” il gap Ã¨ ispirazione, l'articolo Ã¨ originale
- âŒ **Denigrare i competitor** nel report ("[competitor X] fa schifo, lo facciamo meglio") â€” descrittivo, non valutativo
- âŒ **Inventare volumi keyword** â€” sempre flag "qualitativo, validare con strumento"
- âŒ **Citare compagnie mandatarie nostre** come competitor (sono mandanti, non concorrenti)
- âŒ **Suggerire gap che richiedono claim ðŸ”´ vietati** (rendimenti garantiti, ecc.)
- âŒ **Affidamento WebFetch sul singolo run** â€” alcuni siti hanno JS-rendering, WebFetch puÃ² non vedere tutto. Caveat esplicito.

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire la gap analysis, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento Â· sez. 3 segmenti Â· sez. 6 Pillar Map 12 Â· sez. 7 Compliance)
2. `/01_Team/06_SEO_Specialist.md` + `/01_Team/01_Brand_Strategist.md`
3. `config/brand.json` (pillar attivi, voci, dosaggio)
4. `Output_approvati/` blog precedenti (mappa copertura nostra)
5. Il brief operativo del MM (scope mese/trimestre/pillar specifico)

---

*SKILL v1.0 â€” advisory-plus:seo-content-gap â€” Sessione 5 Plugin Build â€” 2026-05-20*

