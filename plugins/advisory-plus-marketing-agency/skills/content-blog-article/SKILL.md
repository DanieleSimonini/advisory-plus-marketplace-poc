---
name: content-blog-article
description: Compone un articolo completo per il blog THE ADVISOR (advisoryplus.it/the-advisor) pronto per pubblicazione WordPress. Orchestra: voce editoriale (a scelta MM secondo taglio: Spiegato Facile = didattico, Caso Reale = narrativo, Analisi = tecnico con apparato citazionale, Badvisor = opinione/critica con tetto 20% mese) â†’ invoca voce-* via Task tool con brief blog â†’ riceve testo lungo (1000-2500p evergreen o 600-1000p short) â†’ applica formattazione blog (struttura H1 unico + H2 5-8 sezioni + H3 dove serve, internal linking 2-4 link a contenuti correlati esistenti, paragrafi brevi 60-100p per leggibilitÃ  mobile) â†’ invoca skill adv-seo-keyword-research (Sessione 5) per keyword primaria + 5 secondarie â†’ genera meta title â‰¤60 char + meta description â‰¤155 char â†’ produce brief cover blog 1200Ã—630 (template Cover Blog System Brand Book v1.2 sez. 8.1, con consolidamento categoria ðŸ“Š Analisi pendente Art Director) â†’ inserisce disclaimer RUI completo in fondo (blog lo consente â€” Brand Book v1.2 sez. 7) â†’ Compliance gate â†’ consegna al MM Markdown WordPress-ready.
---
# ðŸ“° Skill content-blog-article â€” Articolo blog THE ADVISOR

> **Long-form evergreen. SEO-ottimizzato. Disclaimer RUI completo (blog lo consente). Pubblicazione via WordPress.com MCP (Sessione 7).**

---

## 1. Quando triggera

- Invocata dal MM durante settimana per slot blog (frequenza standard: 1/sett ~4-6/mese)
- Invocata per articolo on-demand (es. risposta rapida a evento di settore, voce Analisi)
- Invocata da skill `month-plan` quando pipeline ATL flagga articolo lungo da preparare 7-14gg prima della pubblicazione
- Mai auto-trigger: brief MM obbligatorio

Tempo target di esecuzione: **15-25 minuti** (piÃ¹ lungo per articoli 2500p Analisi con apparato citazionale).

---

## 2. Output finale atteso

**File Markdown WordPress-ready** consegnato al MM, salvato dal MM in `Output_approvati/` con naming `[YYYY-MM-DD]_Blog-the-advisor_[tema]_[variante].md` + cartella `_assets/` per visual:

```markdown
---
canale: blog_the_advisor
data_pianificata: YYYY-MM-DD
orario_suggerito: [es. mar 09:00 â€” picco lettura mattino lavoro]
pillar: P[N] [Nome]
voce: [Spiegato Facile / Caso Reale / Analisi / Badvisor]
lunghezza: [N parole]
firma: [brand "La redazione Advisory+" | Daniele Simonini, Agent Admin & Advisor | altro socio/senior advisor]
# Taxonomy WordPress (modello ibrido v1.1.4)
wp_category_slug: [spiegato-facile | caso-reale | badvisor | analisi]
wp_category_id: [25 | 27 | 26 | 136]
wp_tags:
  pillar: [slug + ID, es. anzianita-ltc â†’ 141]
  attributi: [array di 0-2 tra: voce-advisor 149, news-reattiva 150, evergreen 151, caso-reale-disclaimer 152, specialty-drop 153]
  segmenti: [array di 0-2 tra: giovani-genitori 154 ... specialty-verticali 162]
seo:
  keyword_primaria: "[keyword]"
  keyword_secondarie: ["[kw1]", "[kw2]", "[kw3]", "[kw4]", "[kw5]"]
  meta_title: "[max 60 char]"
  meta_description: "[max 155 char]"
  slug_url: "[slug-url-friendly]"
visual:
  cover_blog: brief_cover_blog_[id].md (1200Ã—630)
  immagini_inline: [eventuali immagini/schemi nel corpo dell'articolo]
internal_linking: ["[URL articolo correlato 1]", "[URL articolo correlato 2]"]
disclaimer_rui: INCLUSO_IN_FONDO
compliance: ðŸŸ¢ / ðŸŸ¡ / ðŸ”´
---

# H1 â€” Titolo dell'articolo (uno solo, contiene keyword primaria)

[Apertura: 80-150 parole Â· hook coerente con voce scelta]

## H2 â€” Prima sezione (idealmente con keyword primaria o secondaria)

[Corpo sezione: 200-400 parole Â· paragrafi brevi 60-100p]

### H3 â€” Sotto-sezione (se utile per leggibilitÃ )

[Corpo Â· max 150p per sezione H3]

## H2 â€” Seconda sezione

[...]

[... 5-8 sezioni H2 totali ...]

## H2 â€” Conclusione / Punti chiave

[Sintesi 100-150p Â· CTA conversazionale non commerciale]

---

## Disclaimer

*Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo.*

[Se Caso Reale]
*Caso reale, nomi di fantasia.*

[Se Analisi e cita normativa specifica o sentenze]
**Fonti:**
- [Ente Â· titolo Â· anno Â· URL ufficiale]
- [...]
```

---

## 3. Specifiche blog THE ADVISOR

### Lunghezza
- **Articolo evergreen / pillar**: **1500-2500 parole** (deep-dive di un tema, premiato da Google per dwell-time)
- **Articolo short / news commento**: **600-1000 parole** (rapido, Analisi reattiva a sentenza/normativa)
- **Articolo medio**: **1000-1500 parole** (default consigliato per Spiegato Facile e Caso Reale)

### Struttura
- **H1 unico** all'inizio: contiene keyword primaria (SEO)
- **H2 5-8 sezioni**: ciascuna con idealmente una keyword secondaria
- **H3 dove serve** per spezzare H2 lunghe (>500p)
- **Paragrafi brevi 60-100 parole** per leggibilitÃ  mobile (oltre il 60% dei lettori legge da smartphone)
- **Liste e bullet** dove appropriato (Spiegato Facile a passi numerati, Analisi a tesi puntuali)
- **Citazioni in blockquote** per Caso Reale (snippet dialogo personaggio) o Analisi (estratto normativa/sentenza)

### SEO
- **Keyword primaria** in: H1, primo paragrafo, almeno una H2, slug URL, meta title, meta description
- **5 keyword secondarie** distribuite naturalmente nel corpo
- Skill invoca `advisory-plus:seo-keyword-research` (Sessione 5) per ricerca + raccomandazione keyword
- **Meta title**: max 60 caratteri (counter rigoroso, oltre Google tronca)
- **Meta description**: max 155 caratteri (counter rigoroso)
- **Slug URL**: kebab-case, contiene keyword primaria, max 60 char (es. `tcm-giovani-genitori-cosa-coprire`)

### Internal linking
- **2-4 link interni** ad articoli correlati giÃ  pubblicati su THE ADVISOR
- Skill controlla in `Output_approvati/` blog precedenti e propone link contestuali
- Anchor text: descrittivo, mai "clicca qui"
- External linking: solo a fonti autorevoli (IVASS, ANIA, COVIP, ISTAT) per voce Analisi; mai a competitor

### Visual
- **Cover blog 1200Ã—630** (template Cover Blog System Brand Book v1.2 sez. 8.1)
- Categoria editoriale visibile nel design (Educazione, Caso Reale, Analisi, Voce CEO, News)
- **Pendenza Art Director (Sessione 4)**: consolidamento categoria ðŸ“Š Analisi nel Cover Blog System (placeholder attuale)
- **Immagini inline**: opzionali, solo se aggiungono valore (schema, grafico, infografica)
- Mai foto identificabili di persone senza consenso
- Per Analisi con dati: schemi/grafici utili (handoff a Art Director per realizzazione)

### Disclaimer RUI
- **Sempre in fondo** all'articolo (blog Ã¨ canale che lo consente â€” Brand Book v1.2 sez. 7)
- Formula standard:
  > *Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo.*

### Categoria blog (4 voci editoriali â€” modello taxonomy ibrida v1.1.4)

**Decisione CEO 2026-05-19 Opzione C: categoria = voce editoriale.** La categoria WP non rappresenta piÃ¹ "funzione/pillar" (modello v1.1.3) ma direttamente la voce editoriale del Brand Book v1.2 sez. 4. Razionale SEO: topical authority + long-tail capture via tag (vedi sotto) + pillar pages futuri.

| Voce | Slug | Cat ID (WP) |
|---|---|---|
| Spiegato Facile | `spiegato-facile` | 25 |
| Badvisor | `badvisor` | 26 |
| Caso Reale | `caso-reale` | 27 |
| Analisi *(nuova v1.2)* | `analisi` | 136 |

Ogni articolo blog ha **una sola categoria WP** = la sua voce editoriale primaria. NB: NON esistono piÃ¹ le categorie "Educazione", "Voce CEO", "News di settore" come categorie WP â€” sono codificate diversamente (Educazione = tag pillar, Voce CEO = tag attributo `voce-advisor`, News = tag attributo `news-reattiva` + tag pillar `news-settore`).

### Tag blog (26 totali â€” modello taxonomy ibrida v1.1.4)

Ogni articolo blog porta **3-6 tag** tipicamente:
1. **1 tag pillar** obbligatorio (12 disponibili â€” Brand Book v1.2 sez. 6)
2. **0-2 tag attributo** (5 disponibili â€” firma, formato, marker compliance)
3. **0-2 tag segmento** (9 disponibili â€” Brand Book v1.2 sez. 3 target)

#### Tag pillar (12, Brand Book v1.2 sez. 6)
| Pillar | Slug | Tag ID |
|---|---|---|
| 1 Educazione assicurativa | `educazione-assicurativa` | 137 |
| 2 IdentitÃ  del consulente | `identita-consulente` | 138 |
| 3 News di settore | `news-settore` | 139 |
| 4 Famiglia & Vita | `famiglia-vita` | 140 |
| 5 AnzianitÃ  & LTC | `anzianita-ltc` | 141 |
| 6 Risparmio & Investimento | `risparmio-investimento` | 142 |
| 7 Tutela Legale | `tutela-legale` | 143 |
| 8 Casa & Patrimonio | `casa-patrimonio` | 144 |
| 9 Imprese & Professionisti | `imprese-professionisti` | 145 |
| 10 Mare & Yacht | `mare-yacht` | 146 |
| 11 Arte & Patrimonio | `arte-patrimonio` | 147 |
| 12 Enti religiosi & Terzo Settore | `enti-religiosi-terzo-settore` | 148 |

#### Tag attributi (5)
| Tag | Slug | Tag ID | Quando applicarlo |
|---|---|---|---|
| Voce Advisor | `voce-advisor` | 149 | Articolo firmato da un socio o senior advisor (NON brand "La redazione Advisory+"). NB: vietato `voce-ceo` per Brand Book sez. 12.1 |
| News reattiva | `news-reattiva` | 150 | Articolo pubblicato entro 48h da evento normativo/sentenza/news mandataria |
| Evergreen | `evergreen` | 151 | Articolo timeless, pillar deep-dive, non legato a evento specifico |
| Caso reale (disclaimer) | `caso-reale-disclaimer` | 152 | Articolo con disclaimer "Caso reale, nomi di fantasia" â€” sempre presente se categoria = `caso-reale` |
| Specialty drop | `specialty-drop` | 153 | Articolo durante drop trimestrale Specialty (Mare/Arte/Terzo Settore) |

#### Tag segmenti (9, Brand Book v1.2 sez. 3)
| Segmento | Slug | Tag ID |
|---|---|---|
| 1 Giovani genitori | `giovani-genitori` | 154 |
| 2 Adulti con anziani | `adulti-con-anziani` | 155 |
| 3 Pre-pensionati | `pre-pensionati` | 156 |
| 4 Patrimonializzati | `patrimonializzati` | 157 |
| 5 Professionisti & P.IVA | `professionisti-partite-iva` | 158 |
| 6 PMI famigliari | `pmi-famigliari` | 159 |
| 7 Imprese strutturate | `imprese-strutturate` | 160 |
| 8 Terzo Settore | `terzo-settore` | 161 |
| 9 Specialty verticali | `specialty-verticali` | 162 |

#### Esempio combinazione tag per articolo

Articolo "Marta, Ada e la mattina in cui tutto Ã¨ cambiato" (Caso Reale Pillar 5 LTC):
- **Categoria**: `caso-reale` (ID 27)
- **Tag pillar**: `anzianita-ltc` (ID 141)
- **Tag attributo 1**: `caso-reale-disclaimer` (ID 152) â€” sempre se categoria caso-reale
- **Tag attributo 2**: `evergreen` (ID 151)
- **Tag segmento**: `adulti-con-anziani` (ID 155)

= 5 tag totali. Sweet spot tipico: 3-6 tag per articolo.

### Orario di pubblicazione raccomandato
- **Mar-Mer-Gio**: 09:00-10:00 (picco lettura mattino lavoro)
- **Articoli short news**: ASAP rispetto all'evento (max 48h dopo sentenza/normativa)
- **Articoli pillar evergreen**: programmati nel month-plan, pubblicati nel pillar dominante del mese

---

## 4. Mapping pillar â†” voce primaria su blog (taxonomy ibrida v1.1.4)

Ricorda: **categoria WP = voce editoriale, tag = pillar**. Quindi il mapping Ã¨ "dato il pillar (tag) quale categoria voce (cat) Ã¨ quella consigliata".

| Tag pillar (Brand Book v1.2 sez. 6) | Categoria voce primaria | Categoria voce alternativa | Lunghezza |
|---|---|---|---|
| `educazione-assicurativa` (Pillar 1) | `spiegato-facile` | â€” | 1000-1500p |
| `identita-consulente` (Pillar 2) | (qualsiasi voce, prevalente `spiegato-facile`) | + tag `voce-advisor` obbligatorio | 800-1500p |
| `news-settore` (Pillar 3) | `analisi` | `spiegato-facile` (divulgativo) | 600-1500p Â· + tag `news-reattiva` se entro 48h |
| `famiglia-vita` (Pillar 4) | `spiegato-facile` | `caso-reale` | 1000-1500p |
| `anzianita-ltc` (Pillar 5) | `caso-reale` | `spiegato-facile` | 1200-2000p |
| `risparmio-investimento` (Pillar 6) | `spiegato-facile` | `analisi` (professional layer) | 1500-2500p |
| `tutela-legale` (Pillar 7) | `caso-reale` | `spiegato-facile` | 1200-1800p |
| `casa-patrimonio` (Pillar 8) | `spiegato-facile` | `caso-reale` | 1000-1500p |
| `imprese-professionisti` (Pillar 9) | `analisi` | `spiegato-facile` (entry) | 1800-2500p |
| `mare-yacht` (Specialty 10) | `caso-reale` | `analisi` | 1500-2000p Â· + tag `specialty-drop` |
| `arte-patrimonio` (Specialty 11) | `analisi` | `caso-reale` | 1800-2500p Â· + tag `specialty-drop` |
| `enti-religiosi-terzo-settore` (Specialty 12) | `analisi` | `caso-reale` | 1500-2000p Â· + tag `specialty-drop` |

### Badvisor su blog: raro
Badvisor su blog Ã¨ eccezionale, non default (Brand Book v1.2 sez. 4.2 â€” "raramente articolo lungo"). Quando usato:
- **Tetto 20% mese** rispettato (verifica quota cumulata)
- Lunghezza ridotta 600-900p (Badvisor non sopporta long-form)
- Strutturato come "opinione/critica al sistema/settore" (sarcasmo e irriverenza verso lo status quo, non verso il lettore)

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM (pillar, voce, tema, lunghezza target, eventuale ancoraggio: news/spunto/evergreen, data pubblicazione)
2. **Eseguire kickoff**
3. **Se voce Badvisor**: verifica quota 20% mese
4. **Invocare skill SEO** via Task tool per keyword research:
   ```
   Task(
     subagent_type: "advisory-plus:seo-keyword-research",
     prompt: "Tema [X] Â· pillar [N] Â· obiettivo: 1 keyword primaria + 5 secondarie Â· pubblico [retail/professional] Â· italiano Â· volume cercabile preferito > 100/mese."
   )
   ```
5. **Ricevere** raccomandazione keyword
6. **Invocare voce editoriale** via Task tool con brief blog lungo:
   ```
   Task(
     subagent_type: "advisory-plus:voce-[name]",
     prompt: "Brief: pillar [N] Â· tema [X] Â· canale Blog THE ADVISOR Â· lunghezza [N] parole Â· struttura H1 + H2 5-8 + H3 Â· keyword primaria [Y] in H1+primo paragrafo+1H2 Â· keyword secondarie [Z1..Z5] distribuite Â· 1 sola variante completa (articolo lungo)."
   )
   ```
7. **Ricevere** testo articolo completo
8. **Verifica struttura**:
   - H1 unico (grep `^# ` deve trovare 1 sola occorrenza)
   - H2 in range 5-8 (grep `^## `)
   - Paragrafi 60-100p (controllo automatico medie)
   - Keyword primaria presente nei punti chiave (H1, primo paragrafo, 1 H2, slug)
9. **Cercare internal linking** in `Output_approvati/` blog precedenti, proporre 2-4 link contestuali
10. **Generare meta tags**:
   - Meta title â‰¤60 char (counter rigoroso, include keyword primaria)
   - Meta description â‰¤155 char (include keyword primaria + CTA implicito)
   - Slug URL kebab-case â‰¤60 char
11. **Produrre brief cover blog** (handoff a skill `adv-image-cover-blog` Sessione 4) con: categoria, voce, palette Cover Blog System
12. **Inserire disclaimer RUI** in fondo (formula standard) + eventuale "Caso reale, nomi di fantasia" + eventuale sezione "Fonti" per Analisi
13. **Invocare Compliance Officer** via Task tool per gate finale (attenzione: claim, denominazione mandatarie, apparato citazionale Analisi, disclaimer)
14. **Se ðŸŸ¡**: riformulazione, ri-check
15. **Se ðŸŸ¢**: consegna al MM file Markdown completo

---

## 6. Casi particolari

### Articolo Analisi reattivo a sentenza/normativa
- Tempistica rapida (48h dall'evento)
- Lunghezza 800-1500p (piÃ¹ snello del pillar evergreen)
- Apparato citazionale puntuale (n. sentenza, data Regolamento, articolo decreto)
- Sezione "Fonti" obbligatoria in fondo
- Categoria blog: `Analisi`
- Tag include nome ente/sentenza

### Articolo pillar evergreen multi-puntata
- Articolo principale 2000-2500p
- "Vedi anche: [puntata 2], [puntata 3]" in chiusura
- Internal linking robusto tra le puntate

### Articolo firmato Daniele
- Voce autoriale 1Âª persona ammessa
- Categoria blog: `Voce CEO`
- Firma in cima: "Di Daniele Simonini, Agent, Admin & Advisor"
- Linkare 1-2 articoli correlati di altri soci (cross-promozione interna)

### Articolo Caso Reale storytelling
- Personaggio fittizio (nome + etÃ  + tratto identificativo)
- Disclaimer "Caso reale, nomi di fantasia" in fondo
- Numeri verosimili e cauti, mai inventati per effetto
- Categoria blog: `Caso Reale`

### Pattern "cifre quasi-prezzo ammesse" *(ratificato CEO 2026-05-18 â€” test runtime Pillar 5 LTC)*

> **Precedente codificato dal test runtime Pillar 5 LTC del 2026-05-18.** CEO ha approvato l'articolo blog "Marta, Ada e la mattina in cui tutto Ã¨ cambiato" (1.380 parole, Caso Reale) che conteneva la formula esemplificativa **"100-200 â‚¬/mese a 50 anni"** per la polizza LTC.

**Quando il pattern Ã¨ ammesso (3 condizioni cumulative â€” TUTTE e tre devono essere soddisfatte):**

1. âœ… **Cifre dichiarate esplicitamente esemplificative**, NON una quotazione di prodotto. Formule ammesse:
   - "indicativamente tra X e Y â‚¬/mese"
   - "a titolo esemplificativo, per un profilo Z, il costo puÃ² oscillare tra X e Y â‚¬"
   - "tipicamente, su questo tipo di copertura, si parla di X-Y â‚¬/mese"
   - "non parliamo di prezzi (variano molto), ma di ordine di grandezza: tra X e Y â‚¬/mese"
2. âœ… **Caveat consulenza individuale obbligatorio** nel paragrafo successivo o subito dopo la cifra:
   - "Il costo reale dipende da [variabili: etÃ , stato di salute, ammontare prestazione, durata, profilo familiare, ecc.]. Serve un preventivo personalizzato."
   - oppure: "Queste cifre sono indicative. La quotazione individuale richiede consulenza dedicata che valuta [variabili specifiche del prodotto]."
3. âœ… **Disclaimer RUI integrale in fondo all'articolo** (formula standard sez. 7 Brand Book + reference set informativo).

**Quando il pattern Ã¨ VIETATO:**

- ðŸ”´ Cifre presentate come **prezzo del prodotto** ("la nostra polizza LTC costa 150 â‚¬/mese")
- ðŸ”´ Confronto numerico con prodotti di compagnie **non mandatarie** ("noi costiamo meno di [competitor]")
- ðŸ”´ Promessa di **risparmio percentuale** ("risparmi il 30% rispetto a X")
- ðŸ”´ Cifre **inventate per effetto** (numeri tondi non plausibili, non sostenibili da ordine di grandezza reale del mercato)
- ðŸ”´ **Senza il caveat consulenza individuale** (cifra cita-e-fuggi)
- ðŸ”´ In articoli che parlano di **prodotti complessi a regolamentazione speciale**: D&O, RC professionale, unit linked (Reg. IVASS 40/2018 art. 56 â€” questi prodotti richiedono consulenza individuale che NON si presta a cifre esemplificative sul blog. Per questi â†’ solo formula "il costo varia significativamente, Ã¨ necessaria una consulenza dedicata", senza range).

**Esempi canonici approvati (Pillar 5 LTC, test runtime 2026-05-18):**

> *"Una polizza LTC sottoscritta a 50 anni con prestazione mensile di 1.500-2.500 â‚¬ costa, indicativamente, tra 100 e 200 â‚¬/mese di premio. Sono cifre esemplificative: il costo reale dipende dall'etÃ  alla sottoscrizione, dal profilo di salute, dalla prestazione scelta e dalla durata. Per una quotazione personalizzata serve un appuntamento di consulenza dedicato."*

> *"Stiamo parlando di ordine di grandezza, non di un listino: a 50 anni una LTC con prestazione di reddito mensile si muove tra 100 e 200 â‚¬/mese. A 60 anni, la stessa copertura puÃ² costare il doppio. Le variabili sono molte. La consulenza individuale serve esattamente a questo: misurare i bisogni, scegliere la prestazione giusta, capire il premio."*

**Compliance gate su articoli con cifre quasi-prezzo:**

- Skill `content/blog-article` invoca `compliance/gate-doppio` con flag `"contains_indicative_pricing": true`
- Compliance Officer verifica le 3 condizioni cumulative
- Se mancante anche una sola: ðŸŸ¡ con riformulazione obbligatoria
- Se prodotto Ã¨ in lista complessi (D&O, RC professionale, unit linked): ðŸ”´ hard, rimuovi la cifra

**Razionale strategico (Brand Book v1.2 sez. 4 + sez. 7):**

Il "non parlare mai di prezzi" Ã¨ una pseudo-regola che alla fine danneggia l'utente: in un articolo educativo come "Marta e Ada" il lettore vuole capire **se LTC Ã¨ alla sua portata o no**. Ometterlo completamente lascia il lettore senza orizzonte e spinge alla rinuncia per "paura del costo sconosciuto". Citare un range esemplificativo con caveat Ã¨ la **versione consulenziale** del prezzo â€” coerente con il pilastro "Approccio consulenziale, non commerciale" (Brand Book v1.2 sez. 2).

---

## 7. Cosa NON fare mai

- âŒ **PiÃ¹ di un H1** nell'articolo (SEO penalizzante)
- âŒ **Meta title >60 char** o meta description >155 char (Google tronca)
- âŒ **Paragrafi >150 parole** (illeggibile su mobile)
- âŒ **Keyword stuffing** (densitÃ  >2-3% = penalizzazione Google)
- âŒ **Saltare disclaimer RUI** in fondo (blog lo consente e lo richiede)
- âŒ **Riferimenti territoriali** (Versilia/Apuana â€” nazionale)
- âŒ **External linking a competitor** (vietato)
- âŒ **Loghi mandatarie** nel corpo (solo in disclosure footer)
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Citazione prezzi specifici di prodotto** (listino, quotazione individuale) â€” distinto dal pattern "cifre quasi-prezzo ammesse" sez. 6 che richiede 3 condizioni cumulative (esemplificative + caveat consulenza individuale + RUI integrale)
- âŒ **Sforare tetto Badvisor 20% mese**
- âŒ **Caso Reale senza disclaimer**
- âŒ **Analisi senza apparato citazionale** o con fonti vietate (giornali generalisti come fonte primaria, blog non firmati, AI-generated)
- âŒ **Articolo Badvisor lungo** (Badvisor Ã¨ voce breve, max 900p)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4 voci Â· sez. 6 Pillar Map Â· sez. 7 Compliance â€” disclaimer blog Â· sez. 8 Design System Cover Blog Â· sez. 9 Compagine firme)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/02_Copywriter.md` Â· `/01_Team/06_SEO_Specialist.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (mapping voce-canale, frequenze blog, dosaggio Badvisor 20%, disclaimer standard)
4. `config/design-system.json` (Cover Blog System)
5. `config/pillars-of-month.json`
6. Articoli blog precedenti in `Output_approvati/` per internal linking
7. Il brief operativo del MM

---

*SKILL v1.2 â€” advisory-plus:content-blog-article â€” Sessione 16 Plugin Build v1.1.4 patch taxonomy ibrida â€” 2026-05-19*
*Update v1.2: ristrutturazione taxonomy WordPress secondo decisione CEO 2026-05-19 Opzione C (modello ibrido SEO). Categoria WP = voce editoriale (4: spiegato-facile, caso-reale, badvisor, analisi). Tag = 12 pillar + 5 attributi + 9 segmenti (totale 26). Mapping pillarâ†”voce aggiornato in sez. 4 con tag attributi obbligatori (voce-advisor per Pillar 2, news-reattiva per news 48h, specialty-drop per Specialty 10-11-12). Razionale SEO: topical authority + long-tail capture + pillar pages futuri.*
*Update v1.1 (precedente, mantenuto): codificato pattern "cifre quasi-prezzo ammesse" sez. 6 (3 condizioni cumulative â€” ratificato CEO 2026-05-18 su test runtime Pillar 5 LTC "Marta, Ada e la mattina in cui tutto Ã¨ cambiato")*

