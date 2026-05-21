---
name: seo-keyword-research
description: Esegue ricerca keyword per il settore assicurativo italiano (scope NAZIONALE, no piÃ¹ territoriale) lungo tutti i 12 pillar del Brand Book v1.2. Restituisce 1 keyword primaria + 5-10 secondarie con intent classificato (informazionale/navigazionale/commerciale/transazionale), difficulty scoring qualitativo, cluster in topic hub. Triggera quando una skill content-blog-article (o on-demand) chiede keyword pre-redazione. Output Markdown strutturato con executive summary + tabella keyword + cluster mappato a pillar. Senza tool keyword premium (Ahrefs/Semrush) lavora su buone pratiche + benchmark settore italiano + indicazione esplicita "validare con strumento reale" â€” il plugin v1.1 NON ha API premium wired.
---
# ðŸ” Skill seo-keyword-research â€” Ricerca keyword per il blog THE ADVISOR + sito advisoryplus.it

> **Settore assicurativo italiano Â· scope nazionale Â· 12 pillar Brand Book v1.2 Â· output deliverable Markdown.**

---

## 1. Quando triggera

- Invocata da `advisory-plus:content-blog-article` (Sessione 3) come step 4 della logica di esecuzione (ricerca keyword prima della redazione)
- Invocata on-demand dal MM per pianificazione pipeline blog (es. month-plan in fase di setup pillar-of-month)
- Invocata da `advisory-plus:seo-content-gap` come sotto-routine quando emerge un'opportunitÃ  da validare
- Invocata occasionalmente per nuove pagine del sito (sito advisoryplus.it, sezioni servizi/prodotti)
- Mai auto-trigger: brief MM o skill chiamante obbligatori

Tempo target di esecuzione: **5-15 minuti** (piÃ¹ lungo se 12 pillar coperti in modalitÃ  setup mensile).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/seo/[YYYY-MM-DD]_keyword-research_[tema].md` oppure delivery in-context alla skill chiamante:

```markdown
---
data: YYYY-MM-DD
tema: [tema/argomento di ricerca]
pillar: P[N] [Nome]
canale_target: [Blog THE ADVISOR | Sito | Multi-canale]
pubblico: [retail | professional | misto]
note_metodologiche: [es. "buone pratiche + benchmark, validare con strumento reale"]
---

## Executive Summary (3-5 righe)

[Sintesi della keyword raccomandata + intent + opportunitÃ  di posizionamento + caveat metodologico]

## Keyword raccomandata (primaria)

- **Keyword:** [...]
- **Intent:** [Informazionale / Navigazionale / Commerciale / Transazionale]
- **Difficulty stimata (qualitativa):** [Bassa / Media / Alta]
- **Volume stimato (qualitativo):** [Nicchia / Medio / Alto]
- **Match con pillar:** P[N]
- **Razionale:** [2-3 righe perchÃ© questa keyword]

## Keyword secondarie (5-10)

| Keyword | Intent | Difficulty | Volume stimato | Match pillar | Note |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

## Cluster (topic hub)

**Cluster name:** [...]
**Articolo pillar (hub):** [titolo + URL futuro]
**Articoli satellite (spoke):** [3-5 sotto-temi raccomandati]
**Cross-link pattern:** [hub linka tutti gli spoke, ogni spoke linka hub]

## Long-tail opportunities (3-5)

[Frasi a coda lunga 4-7 parole con intent specifico, bassa concorrenza, utili per ranking veloce]

## SERP snapshot (qualitativa)

[Cosa appare oggi nella SERP per la keyword primaria â€” fonte: WebFetch su google.it/search?q=... oppure "non verificato in questa sessione"]
- Tipo risultati dominanti: [pagine compagnie Â· blog informativi Â· siti broker Â· comparatori Â· forum]
- Featured snippet presente: [sÃ¬/no/non verificato]
- People Also Ask: [3-5 domande PAA viste]
- Risultati video YouTube: [sÃ¬/no]
- DifficoltÃ  presumibile vs noi: [bassa/media/alta]

## Caveat metodologico

[Lavorato su buone pratiche + benchmark settore IT, senza tool keyword premium. Validare volume effettivo e CPC con Ahrefs/Semrush/Google Keyword Planner prima di pianificare campagne paid o investimenti SEO importanti.]
```

---

## 3. Le 8 fasi della ricerca

### Fase 1 â€” Scope
- Pillar di riferimento (1-12 secondo Brand Book v1.2 sez. 6)
- Pubblico (retail consumer Â· professional B2B Â· misto)
- Canale primario (blog Â· sito Â· supporto a campagna multi-canale)
- Eventuale ancoraggio temporale (news del giorno, sentenza, normativa)

### Fase 2 â€” Seed terms
Partenza da 3-5 termini "seed" derivati dal tema:
- **Tecnico** (es. "long term care", "polizza non autosufficienza")
- **Colloquiale/Spiegato Facile** (es. "assicurazione per anziani", "polizza per quando si invecchia")
- **Problem-aware** (es. "costi RSA Italia", "chi paga la badante")
- **Solution-aware** (es. "rendita vitalizia anzianitÃ ", "polizza LTC quanto costa")
- **Brand/Mandante** dove pertinente (es. "Generali LTC", "DAS tutela legale famiglia") â€” usare solo per pagine prodotto, mai per blog editoriale

### Fase 3 â€” Variations expansion
Per ogni seed term, espansione su:
- Sinonimi (LTC = non autosufficienza = perdita autosufficienza)
- Modificatori geografici quando esplicitamente richiesto (es. "Italia", "2026") â€” **mai modificatori regionali** (scope nazionale Brand Book v1.2 sez. 2)
- Modificatori demografici (giovani Â· genitori Â· pensionati Â· imprese)
- Modificatori di intent (cos'Ã¨ Â· come funziona Â· quanto costa Â· conviene Â· esempio Â· guida Â· vs)
- Variazioni long-tail (4-7 parole con domanda esplicita: "quanto costa polizza LTC anziani", "come funziona TCM mutuo")

### Fase 4 â€” Intent classification
Ogni keyword classificata in:
- **Informazionale**: l'utente vuole capire (es. "cos'Ã¨ la polizza LTC") â†’ blog Spiegato Facile / Analisi
- **Navigazionale**: l'utente cerca uno specifico brand/sito (es. "advisory plus blog") â†’ poche, rilevanti per branding
- **Commerciale**: l'utente confronta soluzioni (es. "polizza LTC migliore 2026", "TCM vs vita intera") â†’ blog Analisi + pagina servizio
- **Transazionale**: l'utente vuole agire (es. "preventivo polizza LTC", "chiama broker assicurativo") â†’ landing/contatti

### Fase 5 â€” Difficulty scoring qualitativo (in assenza di tool premium)
Stima euristica:
- **Bassa**: keyword long-tail specifica (4+ parole), pubblico ristretto, SERP dominata da blog di nicchia
- **Media**: 2-3 parole, alcune compagnie/comparatori in SERP, opportunitÃ  di rank con contenuto autoriale
- **Alta**: 1-2 parole high-volume ("assicurazione vita", "RC professionale"), SERP dominata da compagnie nazionali e comparatori

### Fase 6 â€” GEO-checking (quando applicabile)
**Default Advisory+ = scope nazionale** (Brand Book v1.2 sez. 2, rimossi tutti i riferimenti territoriali).

GEO-checking attivato SOLO se:
- Evento territoriale esplicito (fiera, convegno, sponsorizzazione in una cittÃ )
- Pagina dedicata a una sede (es. "consulente assicurativo Viareggio" per pagina sede)

Quando attivato, modificatori geo ammessi: nome cittÃ /provincia. **Mai** "Versilia" / "Apuana" / "Toscana" come default editoriale.

### Fase 7 â€” Clustering in topic hub
Le keyword raccomandate vengono raggruppate in **topic hub**:
- 1 **keyword pillar** (hub) â†’ articolo pillar evergreen 1500-2500p
- 3-5 **keyword satellite** (spoke) â†’ articoli sotto-tema 800-1500p
- Cross-link pattern: hub linka tutti gli spoke, ogni spoke linka hub + 1-2 altri spoke

Esempio LTC:
- Hub: "polizza long term care" â†’ articolo pillar 2000p
- Spoke 1: "costi RSA Italia 2026" â†’ articolo Analisi 1200p
- Spoke 2: "differenza LTC e dopo di noi" â†’ articolo Spiegato Facile 1000p
- Spoke 3: "polizza LTC giovani genitori carico anziani" â†’ articolo Caso Reale 1500p

### Fase 8 â€” Delivery
Executive summary in cima, tabella keyword strutturata, cluster mappato, caveat metodologico.

---

## 4. Mapping pillar â†’ keyword tematiche (riferimento operativo)

| Pillar | Keyword core | Long-tail tipiche |
|---|---|---|
| P1 Educazione | "polizza", "assicurazione", "consulente assicurativo" | "differenza tra X e Y", "come funziona [prodotto]" |
| P3 News di settore | "IVASS [tema]", "Reg. IVASS [N]", "ANIA dati [anno]" | "novitÃ  normative assicurazioni [anno]" |
| P4 Famiglia & Vita | "TCM", "polizza vita famiglia", "assicurazione mutuo" | "TCM giovani genitori", "polizza vita per chi ha figli" |
| P5 AnzianitÃ  & LTC | "polizza LTC", "non autosufficienza", "dopo di noi" | "costi RSA Italia", "polizza LTC genitori anziani" |
| P6 Risparmio & Investimento | "previdenza integrativa", "fondo pensione", "PAC assicurativo" | "polizza rivalutabile rendimento", "unit linked consulenziale" |
| P7 Tutela Legale | "tutela legale", "polizza tutela legale famiglia", "spese legali" | "tutela legale lavoratore", "tutela legale vicini casa" |
| P8 Casa & Patrimonio | "RC casa", "polizza alluvione", "assicurazione casa" | "polizza eventi climatici Italia", "assicurazione patrimonio donazione" |
| P9 Imprese & Professionisti | "RC professionale", "D&O", "cyber polizza imprese" | "polizza key man PMI", "welfare aziendale collettiva" |
| P10 Mare & Yacht | "polizza yacht", "RC armatore", "assicurazione barca" | "polizza yacht charter Mediterraneo" |
| P11 Arte & Patrimonio culturale | "polizza arte", "all risks opere d'arte" | "assicurazione collezione privata", "polizza trasporto opere arte" |
| P12 Terzo Settore & Enti religiosi | "polizza terzo settore", "D&O ETS", "RC volontari" | "polizza ente religioso parrocchia", "RC volontari onlus" |

---

## 5. Casi particolari

### Articolo Analisi reattivo a normativa/sentenza
- Keyword include riferimento normativo specifico (es. "Reg. IVASS 40/2018 art. 56")
- Long-tail con "cosa cambia", "implicazioni", "guida"
- Tempistica rapida â†’ caveat "verificare volume effettivo dopo trend di ricerca"

### Articolo pillar evergreen
- Hub keyword broad (2-3 parole)
- 5-7 spoke long-tail
- Investimento SEO a lungo termine (6-12 mesi per ranking)

### Pagina servizio sito (non blog)
- Keyword piÃ¹ transazionali ("consulenza assicurativa Italia", "broker indipendente assicurazioni")
- Modificatori "preventivo", "contatti", "studio"
- Disclaimer RUI giÃ  presente nel footer del sito

### Specialty (P10/P11/P12)
- Volume di ricerca tipicamente piÃ¹ basso â†’ puntare su long-tail e autorevolezza
- Keyword piÃ¹ tecniche (audience B2B/professional)
- OpportunitÃ  feature snippet alta (poca competition)

---

## 6. Cosa NON fare mai

- âŒ **Inventare numeri di volume** o "search volume 1.500/mese" senza fonte verificata (regola d'oro Brand Book v1.2 sez. 7 â€” mai inventare dati)
- âŒ **Promettere ranking specifico** ("ti faccio rankare primo") â€” il SEO Ã¨ probabilistico, mai garantito
- âŒ **Modificatori regionali** (Versilia, Apuana, Toscana) come default â€” scope nazionale
- âŒ **Keyword denigratorie** vs concorrenti ("[competitor] truffa", "broker scam") â€” vietato Brand Book v1.2 sez. 7
- âŒ **Keyword su rendimenti garantiti** ("polizza con rendimento garantito 5%") â€” vietato Brand Book v1.2 sez. 7
- âŒ **Keyword stuffing** (>2-3% densitÃ ) â€” penalizzazione Google
- âŒ **Keyword in lingua non italiana** per il mercato italiano (a meno di richiesta specifica B2B internazionale)
- âŒ **Affidamento cieco a tool gratuiti** non validati â€” sempre flaggare "validare con strumento reale"

---

## 7. Compliance hooks

Prima di consegnare al MM, invoca `advisory-plus:compliance-mandatarie-check` se nelle keyword raccomandate compaiono nominalmente compagnie mandatarie (Generali, Cattolica, DAS, UCA, Europ Assistance). Verifica denominazione corretta e uso limitato alla disclosure.

Per voce Analisi (keyword tecniche): invoca `advisory-plus:compliance-citazioni-check` se la keyword include riferimento a sentenza o regolamento (fonte+anno obbligatori).

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire la ricerca, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 2 posizionamento nazionale Â· sez. 3 segmenti target Â· sez. 6 Pillar Map 12 Â· sez. 7 Compliance)
2. `/01_Team/06_SEO_Specialist.md` (persona specialista)
3. `config/brand.json` (pillar attivi, voci, dosaggio, posizionamento nazionale)
4. `config/pillars-of-month.json` (pillar dominante del mese corrente)
5. Articoli blog precedenti in `Output_approvati/` per evitare canibalizzazione keyword (piÃ¹ articoli stesso intent confliggono)
6. Il brief operativo del MM (o della skill chiamante)

---

*SKILL v1.0 â€” advisory-plus:seo-keyword-research â€” Sessione 5 Plugin Build â€” 2026-05-20*

