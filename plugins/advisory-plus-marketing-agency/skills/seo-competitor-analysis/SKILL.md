---
name: seo-competitor-analysis
description: Analizza top 5-10 competitor SEO del settore assicurativo italiano (broker indipendenti di pari taglia + compagnie dirette principali + grandi comparatori). Esegue SERP analysis su keyword strategiche, analizza content angle dei competitor, identifica opportunitÃ  di differenziazione per Advisory+. Output Markdown con tabella positioning + content gap (handoff a seo-content-gap se opportuni nuovi temi emergono) + 3-5 differentiator concreti per Advisory+. NESSUN backlink API premium richiesto in v1.1 (analisi qualitativa basata su WebFetch). Compliance Officer obbligatorio prima della delivery (linguaggio descrittivo, MAI denigratorio â€” Brand Book v1.2 sez. 2).
---
# ðŸ” Skill seo-competitor-analysis â€” Analisi competitor SEO insurance Italia

> **Analisi qualitativa, descrittiva, MAI denigratoria. Output: positioning map + 3-5 differentiator Advisory+. Compliance check obbligatorio.**

---

## 1. Quando triggera

- Invocata trimestralmente in chat 01 Strategia (analisi panorama competitivo)
- Invocata da `advisory-plus:strategia-campaign-30-60-90` in fase di brief per nuova campagna su un pillar
- Invocata da `advisory-plus:seo-content-gap` come pre-step (se gap analysis ha bisogno di mapping competitor preciso)
- Invocata on-demand dal MM quando un competitor fa una mossa significativa (lancio nuova sezione, rebranding, campagna paid visibile)
- Mai auto-trigger: brief MM o skill chiamante obbligatori

Tempo target di esecuzione: **30-60 minuti** (dipende da numero competitor e profonditÃ ).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/seo/[YYYY-MM-DD]_competitor-analysis_[scope].md`:

```markdown
---
data: YYYY-MM-DD
scope: [trimestrale | pillar specifico | post-evento competitor]
competitor_analizzati: [lista 5-10 nomi]
keyword_strategiche_analizzate: [lista 3-8 keyword]
caveat_metodologico: [es. "WebFetch SERP google.it Â· qualitativo Â· validare con tool premium per backlink"]
compliance_check: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

## Executive Summary (5-7 righe)

[Sintesi: chi Ã¨ dove, dove c'Ã¨ spazio per noi, top 3 azioni di differenziazione raccomandate]

## Positioning map (competitor Ã— dimensioni)

| Competitor | Categoria | Pillar coperti | Voce dominante | Frequenza | Punti di forza | Punti di debolezza | Note posizionamento |
|---|---|---|---|---|---|---|---|
| [Nome] | Broker indip / Compagnia / Comparatore | P1, P4, P7... | Spiegato Facile / Corporate / SEO-driven | 1/sett | [...] | [...] | [...] |
| ... | ... | ... | ... | ... | ... | ... | ... |

## SERP analysis su keyword strategiche

### Keyword 1: "[keyword]"
- **Tipo SERP**: [pagine compagnie Â· blog informativi Â· comparatori Â· misto]
- **Top 3 risultati**: [chi, con quale taglio]
- **Featured snippet**: [presente / assente Â· chi lo occupa]
- **People Also Ask**: [3-5 domande PAA]
- **OpportunitÃ  per Advisory+**: [taglio differenziato proposto]

### Keyword 2: "[keyword]"
- [...]

### Keyword 3: "[keyword]"
- [...]

## Content angle competitor (cosa fanno bene Â· cosa non fanno)

### Tema A â€” [pillar]
- **Competitor 1** fa: [taglio Â· profonditÃ  Â· voce]
- **Competitor 2** fa: [taglio Â· profonditÃ  Â· voce]
- **Cosa nessuno fa bene**: [opportunitÃ  Advisory+]

### Tema B â€” [pillar]
- [...]

## Differentiator Advisory+ raccomandati (3-5)

1. **[Differentiator]** â€” Razionale: [...] â€” Pillar match: P[N] â€” Voce: [...]
2. [...]

## Handoff a seo-content-gap (se emerge opportunitÃ  nuovi temi)

[Lista 3-5 temi da approfondire con gap analysis dedicata]

## Caveat metodologico

[Analisi qualitativa basata su WebFetch SERP google.it + ispezione siti competitor. Nessun dato backlink (no Ahrefs/Semrush wired in v1.1). Validare profili dominio e share di voce con strumenti premium per decisioni di budget.]
```

---

## 3. Categorie competitor e selezione

### Categoria A â€” Broker indipendenti di pari taglia (3-4)
Studi medio-piccoli con blog editoriale, posizionamento nazionale o multi-regionale. Concorrenti diretti su clienti retail + PMI.

### Categoria B â€” Compagnie dirette principali (2-3)
Compagnie con presenza editoriale strutturata (es. Allianz, Generali con suo blog corporate distinto dalle nostre mandanti, Unipol, Reale Mutua, ConTe, Genertel). Hanno budget alto, contenuti deep ma corporate.

### Categoria C â€” Grandi comparatori (1-2)
Facile.it, Segugio.it, Prima.it. SEO-driven, volume keyword altissimo ma poco autoriale.

### Categoria D â€” Voce autoriale settore (1, opzionale)
Plus24, IlSole24Ore Insurance, Insurance Trade, AssicurazioniIndipendenti. PiÃ¹ giornalismo settoriale, opportunitÃ  di benchmark voce Analisi.

**Mai includere come competitor:**
- Compagnie mandatarie nostre (Generali Italia â€“ Cattolica Â· DAS Â· UCA Â· Europ Assistance) in modalitÃ  di confronto (sono mandanti)
- Studi locali Versilia/Apuana in modalitÃ  "li battiamo perchÃ© siamo nazionali" (posizionamento Brand Book v1.2 sez. 2 â€” descrittivo, no denigratorio)

---

## 4. Dimensioni di analisi (positioning map)

Ogni competitor valutato su:

### 4.1 Pillar coperti
Quali dei 12 pillar Brand Book v1.2 sono trattati nel loro editoriale?

### 4.2 Voce dominante
- Spiegato Facile / didattico-divulgativo
- Corporate (compagnie dirette)
- Analisi tecnica
- SEO-driven (comparatori)
- Caso Reale / storytelling

### 4.3 Frequenza pubblicazione
- Quotidiana / 2-3 sett / Settimanale / Mensile / Sporadica

### 4.4 Punti di forza (descrittivi)
- Es. "Approfondimento tecnico LTC con apparato citazionale solido"
- Es. "Volume blog alto + struttura silos SEO ben fatta"
- Es. "Presenza LinkedIn pagina costante con tono autoriale"

### 4.5 Punti di debolezza (descrittivi, MAI denigratori)
- Es. "Comunicazione corporate distante dal cliente finale"
- Es. "Tone of voice piatto, no differenziazione voce"
- Es. "Nessuna voce autoriale identificabile"

âš ï¸ **NO formulazioni denigratorie**: vietato "[competitor X] fa schifo" / "[competitor Y] truffa i clienti" / "[competitor Z] Ã¨ obsoleto". Sempre descrittivo, mai valutativo.

### 4.6 Note posizionamento
- Target dichiarato (retail / PMI / corporate)
- Geografia operativa (nazionale / multi-regionale / locale)
- Specializzazioni dichiarate (LTC / Tutela legale / Cyber / ecc.)

---

## 5. Logica di esecuzione â€” 6 fasi

### Fase 1 â€” Brief + selezione competitor
- Scope (trimestrale / pillar specifico / evento competitor)
- 5-10 competitor selezionati dalle 4 categorie
- 3-8 keyword strategiche selezionate (dal pillar di mese o dalla pipeline blog)

### Fase 2 â€” Recon competitor
Per ogni competitor: WebFetch homepage + sezione blog/insights + 1-2 pagine servizio. Estrarre:
- Categorie editoriali / tag visibili
- 10-15 titoli articoli recenti
- Voce e taglio dominante (lettura qualitativa)
- Frequenza approssimativa (date pubblicazione)

### Fase 3 â€” SERP analysis
Per ogni keyword strategica: WebFetch `google.it/search?q=[keyword]&hl=it` (o equivalente). Estrarre:
- Top 5-10 risultati organici (chi, titolo, snippet)
- Featured snippet se presente
- People Also Ask (3-5 domande)
- Risultati video (YouTube) se presenti

### Fase 4 â€” Cross-mapping
Confrontare:
- Pillar coperti dai competitor vs nostri pillar attivi
- Voci competitor vs nostre 4 voci editoriali
- Frequenza competitor vs nostra (Brand Book v1.2 sez. 5)
- Keyword strategiche: chi le occupa, con quale taglio

### Fase 5 â€” Identificazione differentiator
Cercare:
- Pillar Advisory+ con copertura competitor debole o assente
- Voci Advisory+ assenti nei competitor (es. Caso Reale storytelling, Badvisor ironico â€” quasi nessun competitor li usa con la nostra disciplina)
- Specialty (P10/P11/P12) sotto-coperte
- Apparato citazionale Analisi (poche aziende italiane lo fanno con rigore)

### Fase 6 â€” Output + handoff
- Compilazione report Markdown
- Raccomandazione 3-5 differentiator concreti
- Handoff a `advisory-plus:seo-content-gap` se emergono opportunitÃ  di nuovi temi
- Compliance Officer check OBBLIGATORIO prima di delivery

---

## 6. Differentiator tipici di Advisory+ (riferimento)

Brand Book v1.2 sez. 2 â€” 5 pilastri di differenziazione:
1. Approccio consulenziale, non commerciale
2. Mandati diretti con compagnie primarie italiane ed europee
3. Specializzazione tutela legale (UCA + DAS)
4. Competenza specialty su ambiti verticali ad alto valore
5. ContinuitÃ  relazionale

Dimensioni editoriali in cui questi pilastri si traducono:
- **Voce Caso Reale** raramente usata dai competitor con la nostra disciplina narrativa
- **Voce Analisi** con apparato citazionale fonti+anno raramente competitor
- **Pillar 2 â€” IdentitÃ  del consulente** (Voce CEO autoriale Daniele) Ã¨ asset distintivo: nessun competitor ha figura autoriale identificabile costante
- **Pillar 12 â€” Terzo Settore & Enti religiosi** specialty rara
- **Pillar 7 â€” Tutela Legale** (doppio mandato UCA + DAS) Ã¨ unicum di mercato

---

## 7. Casi particolari

### Competitor "ha fatto una mossa" (rebranding Â· nuova campagna paid Â· lancio sezione)
- Audit mirato su quella specifica mossa
- Tempistica rapida (3-7 giorni)
- Output: nota sintetica + raccomandazione (rispondere o ignorare)

### Analisi pre-campagna pillar
- 3-5 competitor focalizzati sul pillar
- 3-4 keyword chiave del pillar
- Output: positioning map + content angle differenziato

### Analisi panorama trimestrale
- 8-10 competitor
- 5-8 keyword strategiche distribuite sui pillar
- Output completo con sezione SERP per ogni keyword

---

## 8. Cosa NON fare mai

- âŒ **Linguaggio denigratorio** verso competitor ("fanno schifo", "obsoleti", "truffaldini") â€” Brand Book v1.2 sez. 7 vieta confronti denigratori
- âŒ **Citare prezzi specifici** dei competitor anche se trovati in WebFetch (vietato per noi â†’ meglio evitarlo come riferimento)
- âŒ **Promettere "li battiamo"** in 3 mesi â€” il SEO Ã¨ probabilistico
- âŒ **Includere compagnie mandatarie nostre** nella lista competitor (sono mandanti, non concorrenti â€” Brand Book v1.2 sez. 7)
- âŒ **Citare backlink data** se non si ha tool premium â€” caveat esplicito sempre
- âŒ **Affidamento WebFetch sul singolo run** â€” alcuni siti hanno JS-rendering, WebFetch puÃ² non vedere tutto. Caveat
- âŒ **Suggerire azioni che richiederebbero claim ðŸ”´ vietati** (rendimenti garantiti, comparazioni denigratorie) anche se "il competitor lo fa"

---

## 9. Compliance hooks (OBBLIGATORI prima di delivery)

Invoca SEMPRE in chiusura `advisory-plus:compliance-mandatarie-check` per verificare:
- Denominazione mandanti corretta dove citate
- No comparazioni denigratorie con compagnie non mandatarie
- No citazione prezzi specifici di competitor
- Linguaggio descrittivo e non valutativo

Se Compliance restituisce ðŸŸ¡ o ðŸ”´: riformulazione obbligatoria prima di delivery.

Brand Strategist verifica la coerenza dei differentiator proposti con i 5 pilastri Brand Book.

---

## 10. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di analizzare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 1 identitÃ  Â· sez. 2 posizionamento + 5 pilastri Â· sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance)
2. `/01_Team/06_SEO_Specialist.md` + `/01_Team/01_Brand_Strategist.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (pilastri differenziazione, voci, mandanti, claim ammessi/vietati)
4. `Output_approvati/seo/` competitor-analysis precedenti (per trend)
5. `Output_approvati/` blog precedenti (mappa copertura nostra)
6. Il brief operativo del MM

---

*SKILL v1.0 â€” advisory-plus:seo-competitor-analysis â€” Sessione 5 Plugin Build â€” 2026-05-20*

