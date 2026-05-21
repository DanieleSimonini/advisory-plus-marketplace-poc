---
name: seo-on-page-analysis
description: Esegue audit SEO on-page di un articolo blog o pagina sito PRIMA della pubblicazione. Verifica: H1 unico, H2 5-8, H3 dove serve, meta title â‰¤60 char, meta description â‰¤155 char, densitÃ  keyword naturale (1-2%), internal linking 2-4, alt text immagini, schema markup Article/Organization, slug URL kebab-case â‰¤60 char. Output checklist verde/giallo/rosso con raccomandazioni di correzione puntuali. Invocata da content-blog-article (Sessione 3) come step finale, o on-demand su pagine sito esistenti. Read-only sull'articolo, NON modifica direttamente.
---
# ðŸ” Skill seo-on-page-analysis â€” Audit SEO on-page pre-publish

> **Check pre-pubblicazione. Read-only. Output: checklist verde/giallo/rosso + raccomandazioni di correzione puntuali.**

---

## 1. Quando triggera

- Invocata da `advisory-plus:content-blog-article` (Sessione 3) come step finale prima del Compliance gate
- Invocata da `advisory-plus:seo-technical-audit` come sotto-routine quando audita una singola pagina
- Invocata on-demand dal MM per audit ex-post di articoli giÃ  pubblicati (es. fix retro-attivi su pillar evergreen)
- Mai auto-trigger: brief MM o skill chiamante obbligatori

Tempo target di esecuzione: **2-5 minuti** per articolo.

---

## 2. Output finale atteso

**Report Markdown** consegnato alla skill chiamante o al MM, salvato (se on-demand) in `Output_approvati/seo/[YYYY-MM-DD]_on-page-audit_[slug].md`:

```markdown
---
data: YYYY-MM-DD
file_auditato: [path o URL]
keyword_primaria_dichiarata: "[...]"
score_complessivo: ðŸŸ¢ OK / ðŸŸ¡ ATTENZIONE / ðŸ”´ BLOCCO
---

## Sintesi (1-2 righe)

[OK pubblicabile | Riformulare prima di pubblicare | Bloccato, fix sostanziale]

## Checklist

| Check | Stato | Note |
|---|---|---|
| H1 unico | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [trovati N H1] |
| H2 in range 5-8 | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [trovati N H2] |
| H3 dove serve | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Meta title â‰¤60 char | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | "[title]" â€” [N char] |
| Meta description â‰¤155 char | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | "[desc]" â€” [N char] |
| Keyword primaria in H1 | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Keyword primaria in primo paragrafo (primi 100p) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Keyword primaria in 1 H2 | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Keyword primaria nello slug URL | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | "[slug]" |
| DensitÃ  keyword naturale (1-2%) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N occorrenze su [tot] parole = X%] |
| Keyword secondarie distribuite | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N/5 secondarie presenti] |
| Paragrafi 60-100p | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N paragrafi >150p] |
| Internal linking 2-4 | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N link interni] |
| Anchor text descrittivi (no "clicca qui") | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| External linking solo fonti autorevoli | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Alt text su immagini | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N/tot immagini con alt] |
| Schema markup Article | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [presente/assente â€” solo verifica dichiarata, on-page non lo genera] |
| Schema markup Organization | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [presente/assente] |
| Slug URL kebab-case â‰¤60 char | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | "[slug]" â€” [N char] |
| Disclaimer RUI presente (canali che lo consentono) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |

## Raccomandazioni di correzione (se ðŸŸ¡ o ðŸ”´)

1. [Punto specifico + soluzione proposta]
2. [...]

## Stima ranking opportunity (qualitativa)

- **Quick win (24-48h)**: [se applicabile]
- **Medio termine (1-3 mesi)**: [se applicabile]
- **Lungo termine (6-12 mesi)**: [se applicabile]
```

---

## 3. Le 18 voci della checklist (in dettaglio)

### 3.1 Struttura semantica

**H1 unico** â†’ grep `^# ` deve trovare **1 sola occorrenza**.
- ðŸŸ¢ Esattamente 1
- ðŸŸ¡ 0 o 2 (errore correggibile)
- ðŸ”´ â‰¥3 (riformulazione strutturale)

**H2 in range 5-8** â†’ grep `^## `.
- ðŸŸ¢ 5-8
- ðŸŸ¡ 3-4 oppure 9-10
- ðŸ”´ <3 oppure >10

**H3 dove serve** â†’ presenti SOLO se serve spezzare H2 lunghe (>500 parole).
- ðŸŸ¢ H3 presenti in modo coerente
- ðŸŸ¡ H3 presenti senza necessitÃ  (frammentazione) o assenti dove servono
- ðŸ”´ (raro, non bloccante di solito)

### 3.2 Meta tags

**Meta title â‰¤60 char** â†’ counter rigoroso (oltre Google tronca).
- ðŸŸ¢ â‰¤60
- ðŸŸ¡ 61-65 (borderline, accettabile in alcuni casi)
- ðŸ”´ >65

**Meta description â‰¤155 char** â†’ counter rigoroso.
- ðŸŸ¢ â‰¤155
- ðŸŸ¡ 156-160
- ðŸ”´ >160

### 3.3 Keyword placement

**Keyword primaria in H1** â†’ presente almeno come radice (lemmatizzazione tollerata).
- ðŸŸ¢ Presente
- ðŸŸ¡ Variante stretta (es. plurale vs singolare)
- ðŸ”´ Assente

**Keyword primaria in primo paragrafo** (primi 100 parole dopo H1).
- ðŸŸ¢ Presente
- ðŸŸ¡ Sinonimo presente
- ðŸ”´ Assente

**Keyword primaria in 1 H2** â†’ almeno una H2 contiene la keyword o variante.
- ðŸŸ¢ Presente
- ðŸŸ¡ Sinonimo presente
- ðŸ”´ Assente

**Keyword primaria nello slug URL** â†’ kebab-case.
- ðŸŸ¢ Presente
- ðŸŸ¡ Variante
- ðŸ”´ Assente

### 3.4 DensitÃ  keyword

**DensitÃ  keyword naturale (1-2%)** â†’ (occorrenze keyword / totale parole) Ã— 100.
- ðŸŸ¢ 0.8-2.0%
- ðŸŸ¡ 0.3-0.8% (sotto-utilizzata) oppure 2.0-2.5% (alta ma OK)
- ðŸ”´ <0.3% (keyword "fantasma") oppure >2.5% (stuffing, penalizzazione Google)

**Keyword secondarie distribuite** â†’ almeno 4/5 secondarie devono comparire nel corpo.
- ðŸŸ¢ 5/5 o 4/5
- ðŸŸ¡ 3/5
- ðŸ”´ â‰¤2/5

### 3.5 LeggibilitÃ 

**Paragrafi 60-100 parole** â†’ oltre il 60% dei lettori legge da smartphone.
- ðŸŸ¢ Tutti i paragrafi â‰¤120 parole
- ðŸŸ¡ 1-2 paragrafi 120-150 parole
- ðŸ”´ >2 paragrafi >150 parole

### 3.6 Linking

**Internal linking 2-4** â†’ link a contenuti correlati giÃ  pubblicati su THE ADVISOR.
- ðŸŸ¢ 2-4
- ðŸŸ¡ 1 o 5-6
- ðŸ”´ 0 o >6

**Anchor text descrittivi** â†’ mai "clicca qui", "leggi di piÃ¹", "vai".
- ðŸŸ¢ Tutti descrittivi
- ðŸŸ¡ 1 generico tollerato
- ðŸ”´ â‰¥2 generici

**External linking solo a fonti autorevoli** â†’ IVASS, ANIA, COVIP, ISTAT, sentenze Cassazione, Regolamenti UE.
- ðŸŸ¢ Tutti autorevoli
- ðŸŸ¡ 1 fonte borderline (es. testata generalista come supporto, non primaria)
- ðŸ”´ Link a competitor (vietato) o fonti non autorevoli (blog non firmati, social, AI-generated)

### 3.7 Asset visivi

**Alt text su immagini** â†’ ogni `<img>` o riferimento markdown ha alt descrittivo.
- ðŸŸ¢ Tutte coperte
- ðŸŸ¡ 1 immagine senza alt
- ðŸ”´ â‰¥2 immagini senza alt

### 3.8 Schema markup (verifica dichiarata)

**Schema Article** â†’ la skill on-page NON genera schema (compito del CMS WordPress.com), ma verifica dichiarazione nel frontmatter o nelle note tecniche.
- ðŸŸ¢ Dichiarato (gestito dal tema WordPress.com)
- ðŸŸ¡ Non dichiarato esplicitamente
- ðŸ”´ (raro)

**Schema Organization** â†’ idem, gestito a livello sito.
- ðŸŸ¢/ðŸŸ¡ come sopra

### 3.9 URL

**Slug URL kebab-case â‰¤60 char** â†’ contiene keyword primaria, lowercase, trattini.
- ðŸŸ¢ â‰¤60, kebab-case, keyword primaria
- ðŸŸ¡ 61-70 oppure manca keyword
- ðŸ”´ >70 oppure underscore/spazi/caratteri speciali

### 3.10 Compliance baseline

**Disclaimer RUI presente** â†’ solo per canali che lo richiedono (blog, newsletter, sito, brochure â€” Brand Book v1.2 sez. 7).
- ðŸŸ¢ Presente integrale in fondo
- ðŸŸ¡ Presente ma incompleto
- ðŸ”´ Assente (canale lo richiede)

---

## 4. Logica di esecuzione â€” passo-passo

1. **Ricevere file/path/contenuto** dall'invocazione (skill chiamante o brief MM)
2. **Estrarre frontmatter** (keyword primaria, secondarie, meta tags dichiarati, canale, slug)
3. **Eseguire i 18 check** uno per uno con regex/grep e counter
4. **Calcolare densitÃ  keyword**: (occorrenze keyword case-insensitive / totale parole testo) Ã— 100
5. **Verificare lemmatizzazione tollerante** (singolare/plurale, masc/fem) per non penalizzare varianti naturali
6. **Compilare tabella checklist** con stato per ogni voce
7. **Calcolare score complessivo**:
   - ðŸŸ¢ OK = tutti ðŸŸ¢ oppure max 2 ðŸŸ¡ non critici (meta description borderline, internal linking 1)
   - ðŸŸ¡ ATTENZIONE = 3-5 ðŸŸ¡ oppure 1 ðŸ”´ minore (slug, alt text)
   - ðŸ”´ BLOCCO = â‰¥6 ðŸŸ¡ oppure â‰¥2 ðŸ”´ oppure 1 ðŸ”´ critico (>1 H1, keyword stuffing, disclaimer RUI assente su canale che lo richiede)
8. **Scrivere raccomandazioni di correzione** puntuali (numerate, ognuna con il check fallito + soluzione proposta)
9. **Stimare ranking opportunity** qualitativa (quick win = fix meta tags, medio termine = fix struttura, lungo termine = fix internal linking + keyword secondarie)
10. **Consegnare report** alla skill chiamante o al MM

---

## 5. Casi particolari

### Articolo pillar evergreen 2500p
- Richiede H2 7-8 (non 5)
- Internal linking minimo 3 (non 2)
- DensitÃ  keyword 1.0-1.8% (piÃ¹ bassa per articoli lunghi naturali)

### Articolo short news 600-1000p
- H2 3-5 accettabili (non penalizzati a ðŸŸ¡)
- Internal linking minimo 1 (lascia ðŸŸ¡ se 0)

### Pagina servizio sito (non blog)
- Schema markup richiesto: Service / LocalBusiness oltre a Organization
- CTA presenti (contatti, preventivo)
- Disclaimer RUI in footer site-wide (verifica dichiarata)

### Articolo voce Analisi
- Apparato citazionale verificato da skill `compliance-citazioni-check` (handoff, non in scope on-page)
- External linking a fonti normative obbligatorio (tollerato 4-6 link esterni, non penalizzato)

---

## 6. Cosa NON fare mai

- âŒ **Modificare direttamente l'articolo** â€” la skill Ã¨ read-only, propone fix, applica il MM o la skill chiamante
- âŒ **Approvare ðŸŸ¢ con keyword stuffing** anche se altri check OK
- âŒ **Approvare ðŸŸ¢ senza disclaimer RUI** su canali che lo richiedono
- âŒ **Promettere ranking specifico** ("con questo audit rankerai primo") â€” il SEO Ã¨ probabilistico
- âŒ **Affidamento cieco a counter automatici** â€” counter sono indicativi, lemmatizzazione e contesto contano
- âŒ **Penalizzare varianti naturali** della keyword (singolare/plurale) come ðŸ”´

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di auditare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 7 Compliance â€” disclaimer canali Â· sez. 6 Pillar Map Â· sez. 2 posizionamento nazionale)
2. `/01_Team/06_SEO_Specialist.md` (persona)
3. `config/brand.json` (regole linking, anchor text, disclaimer per canale)
4. Il file/contenuto da auditare

---

*SKILL v1.0 â€” advisory-plus:seo-on-page-analysis â€” Sessione 5 Plugin Build â€” 2026-05-20*

