---
name: seo-technical-audit
description: Esegue audit tecnico SEO trimestrale del sito advisoryplus.it. Verifica: robots.txt + sitemap.xml accessibili e validi Â· canonical tags correttamente impostati Â· page speed (Core Web Vitals LCP/INP/CLS) Â· mobile-friendliness Â· schema markup site-wide (Organization, LocalBusiness se sedi attive, BreadcrumbList) Â· errori 404 e redirect 301/302 Â· indicizzazione Google Search Console Â· HTTPS e sicurezza headers Â· meta robots. Output: report sintetico + lista azioni prioritizzate da girare al freelance webmaster del sito. Trigger: trimestrale (schedulato in chat 08 Performance & Analytics) oppure on-demand dopo modifiche strutturali.
---
# ðŸ”§ Skill seo-technical-audit â€” Audit tecnico advisoryplus.it (trimestrale)

> **Audit infrastrutturale SEO. Output: report sintetico + lista azioni prioritizzate per il webmaster.**

---

## 1. Quando triggera

- **Schedulazione trimestrale** in chat 08 Performance & Analytics (es. ultimo venerdÃ¬ del trimestre)
- Invocata on-demand dal MM dopo modifiche strutturali al sito (rilascio nuova sezione, migrazione hosting, cambio template WordPress.com)
- Invocata in fase di pre-launch di una nuova pagina servizio
- Mai auto-trigger: brief MM o scheduled task obbligatori

Tempo target di esecuzione: **30-60 minuti** (piÃ¹ lungo se WebFetch lento su 5-10 URL chiave).

---

## 2. Output finale atteso

**File Markdown** in `Output_approvati/seo/[YYYY-MM-DD]_technical-audit_advisoryplus-it.md`:

```markdown
---
data: YYYY-MM-DD
sito_auditato: advisoryplus.it
trimestre: [Q1 2026 | Q2 2026 | ...]
score_complessivo: ðŸŸ¢ OK / ðŸŸ¡ ATTENZIONE / ðŸ”´ CRITICO
prossimo_audit: [YYYY-MM-DD +90gg]
---

## Sintesi esecutiva (5 righe)

[Cosa Ã¨ ok, cosa va sistemato, quanto Ã¨ urgente, chi deve agire (freelance webmaster + nostro lato)]

## Checklist tecnica

| Area | Check | Stato | Note + raccomandazione |
|---|---|---|---|
| Crawling | robots.txt accessibile | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [URL: advisoryplus.it/robots.txt] |
| Crawling | sitemap.xml accessibile e valida | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N URL Â· last-mod recente] |
| Crawling | meta robots su pagine chiave | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Crawling | Canonical tag su tutte le pagine | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Performance | LCP (Largest Contentful Paint) | ðŸŸ¢ â‰¤2.5s / ðŸŸ¡ 2.5-4s / ðŸ”´ >4s | [misurato su homepage e 1 blog post] |
| Performance | INP (Interaction to Next Paint) | ðŸŸ¢ â‰¤200ms / ðŸŸ¡ 200-500ms / ðŸ”´ >500ms | [...] |
| Performance | CLS (Cumulative Layout Shift) | ðŸŸ¢ â‰¤0.1 / ðŸŸ¡ 0.1-0.25 / ðŸ”´ >0.25 | [...] |
| Performance | Mobile-friendliness | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Performance | Lazy loading immagini | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Schema markup | Organization | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Schema markup | LocalBusiness (5 sedi se applicabile) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Schema markup | BreadcrumbList | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Schema markup | Article su blog | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Errori | 404 critici (link interni rotti) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [lista 404 rilevati] |
| Errori | Redirect 301/302 catene | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Sicurezza | HTTPS site-wide | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Sicurezza | Headers sicurezza (HSTS, CSP) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Indicizzazione | GSC: copertura indice | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N pagine indicizzate / dichiarate] |
| Indicizzazione | GSC: errori di scansione | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| URL | Struttura URL pulita | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| URL | Trailing slash coerente | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [...] |
| Internazionalizzazione | hreflang (se multilingua) | ðŸŸ¢/ðŸŸ¡/ðŸ”´ | [N/A se solo IT] |

## Azioni prioritizzate

### ðŸ”¥ Urgenti (entro 7 giorni â€” bloccano ranking)
1. [Azione] â€” Responsabile: [Webmaster / MM / CEO] â€” Effort: [basso/medio/alto]

### ðŸŸ¡ Importanti (entro 30 giorni)
1. [...]

### ðŸŸ¢ Migliorative (entro fine trimestre)
1. [...]

## Handoff al webmaster

[Lista azioni filtrate per quelle che richiedono accesso CMS/server, formattata in modo che CEO possa girarla direttamente]

## Caveat metodologico

[Audit qualitativa basata su WebFetch + Lighthouse-style euristica. Per misure precise CWV usare PageSpeed Insights Â· per copertura indicizzazione usare Google Search Console direttamente. Plugin v1.1 non ha API Search Console wired.]
```

---

## 3. Le 22 voci dell'audit (in dettaglio)

### 3.1 Crawling (4 voci)

**robots.txt accessibile** â†’ fetch `advisoryplus.it/robots.txt`. Deve esistere, non bloccare la sitemap, non avere `Disallow: /` cieco.

**sitemap.xml accessibile e valida** â†’ fetch `advisoryplus.it/sitemap.xml` o `sitemap_index.xml`. Verifica: URL listate, last-modified recente, no errori XML.

**meta robots su pagine chiave** â†’ home, blog index, pagine servizio devono avere `index, follow` (no `noindex`).

**Canonical tag** â†’ ogni pagina deve avere `<link rel="canonical">` puntante a se stessa o alla versione canonica. Verifica su 5-10 URL chiave.

### 3.2 Performance (5 voci)

**LCP** â‰¤ 2.5s (Core Web Vitals soglia "Good")
**INP** â‰¤ 200ms
**CLS** â‰¤ 0.1
**Mobile-friendliness** â†’ Lighthouse / PageSpeed Insights mobile score â‰¥ 80
**Lazy loading immagini** â†’ `loading="lazy"` su immagini sotto la fold

### 3.3 Schema markup (4 voci)

**Organization** â†’ presente in homepage e footer site-wide. Campi: name="Studio Solutions S.r.l." (o "Advisory+" come legalName/alternateName), URL, logo, sameAs (LinkedIn, IG, FB, YouTube quando attivo).

**LocalBusiness** â†’ opzionale per le 5 sedi. Se attivato, una entry per ogni sede (Viareggio, Massa, Carrara, Pietrasanta, Camaiore). **Nota Brand Book v1.2 sez. 2**: le 5 sedi sono fatto logistico-operativo, non asset narrativo. LocalBusiness OK per pagina contatti, NO per pagine editoriali blog.

**BreadcrumbList** â†’ su blog post e pagine servizio.

**Article** â†’ su tutti gli articoli blog (gestito dal tema WordPress.com tipicamente).

### 3.4 Errori (2 voci)

**404 critici** â†’ crawl interno per link interni rotti. Verifica via Search Console "Errori 404".
- ðŸŸ¢ Zero 404 da link interni
- ðŸŸ¡ 1-3 (correggibili)
- ðŸ”´ â‰¥4 (segnale di link rot)

**Redirect 301/302 catene** â†’ no piÃ¹ di 1 redirect in catena. Verifica via WebFetch following redirects.

### 3.5 Sicurezza (2 voci)

**HTTPS site-wide** â†’ http://advisoryplus.it deve redirectare 301 a https://. Tutto contenuto in HTTPS (no mixed content).

**Headers sicurezza** â†’ HSTS, X-Content-Type-Options, Referrer-Policy. CSP opzionale ma raccomandato.

### 3.6 Indicizzazione (2 voci)

**Copertura indice GSC** â†’ N pagine indicizzate vs dichiarate in sitemap. Gap >10% = flag ðŸŸ¡.

**Errori di scansione GSC** â†’ errori server, soft 404, accesso negato. Da verificare direttamente in Search Console (la skill flagga "verifica manuale GSC").

### 3.7 URL (2 voci)

**Struttura URL pulita** â†’ kebab-case, no parametri inutili, no caratteri speciali, profonditÃ  â‰¤4 livelli.

**Trailing slash coerente** â†’ tutto il sito usa `/page/` o tutto `/page`, non misto.

### 3.8 Internazionalizzazione (1 voce)

**hreflang** â†’ N/A se sito solo IT. Se in futuro versione EN/altro, hreflang obbligatorio.

---

## 4. Logica di esecuzione â€” 5 fasi

### Fase 1 â€” Discovery URL chiave
- Homepage: advisoryplus.it
- Blog index: advisoryplus.it/the-advisor (o equivalente)
- 1-2 blog post recenti
- Pagina chi siamo / studio
- Pagina contatti
- Pagina servizi/prodotti chiave

### Fase 2 â€” Fetch + parsing
WebFetch su ogni URL chiave. Estrarre:
- Status code (200 / redirect / 404)
- Headers (HSTS, content-type, canonical, meta robots)
- Title, meta description
- Schema markup JSON-LD
- Performance approssimativa (size HTML, n. risorse esterne)

### Fase 3 â€” Specialized check
- robots.txt e sitemap.xml come fetch separati
- Verifica HTTPS redirect da http://
- Lista 5-10 URL interni dal sitemap â†’ fetch a campione per 404/redirect

### Fase 4 â€” Compilazione checklist + scoring
- Compilare le 22 voci
- Score complessivo:
  - ðŸŸ¢ OK = â‰¥18/22 verdi, max 2 ðŸ”´ minori
  - ðŸŸ¡ ATTENZIONE = 12-17 verdi, max 3 ðŸ”´
  - ðŸ”´ CRITICO = <12 verdi o â‰¥4 ðŸ”´ o 1 ðŸ”´ critico (sitemap rotta, HTTPS assente, no indicizzazione)

### Fase 5 â€” Priorizzazione azioni + handoff
- Ordinare azioni per impatto SEO Ã— urgenza Ã— effort
- Filtrare quelle che richiedono webmaster (CMS/server access) per handoff
- Stimare effort qualitativo (basso/medio/alto)

---

## 5. Casi particolari

### Sito appena migrato
- Aspettarsi turbolenza ranking 2-4 settimane
- Verifica robots.txt e meta robots con prioritÃ  (rischio noindex residuo)
- Verifica redirect mapping vecchi URL â†’ nuovi

### Lancio nuova sezione (es. categoria blog Specialty)
- Verifica sitemap aggiornata
- Verifica internal linking da homepage e blog index
- Submit sitemap a Search Console

### Performance critica (CWV ðŸ”´)
- Identificare hop principali (immagini non ottimizzate, JS bloccante, font caricamento)
- Handoff webmaster + raccomandare Cloudinary MCP (Sessione 4 wiring) per ottimizzazione immagini automatica

### Errori 404 da link esterni (referenti che linkano URL vecchi)
- Mappare top 404 con backlink
- Impostare redirect 301 verso pagina piÃ¹ rilevante
- Lascia ðŸŸ¢ anche con 404 isolati se link entranti sono trascurabili

---

## 6. Cosa NON fare mai

- âŒ **Eseguire crawl invasivo** del sito (max ~20 fetch per audit, no spider profondo)
- âŒ **Promettere ranking specifico** post-fix
- âŒ **Modificare direttamente il sito** â€” la skill Ã¨ read-only, propone azioni al webmaster
- âŒ **Tagliare le 5 sedi dal sito** (sono fatto logistico-operativo OK per pagina contatti/LocalBusiness) â€” Brand Book v1.2 sez. 2 limita solo l'uso narrativo
- âŒ **Affidamento WebFetch senza caveat** â€” alcune misure CWV richiedono PageSpeed Insights diretto, GSC per indicizzazione. Flag esplicito "verifica manuale richiesta"
- âŒ **Bypassare disclaimer RUI** verifica nel footer (sito Ã¨ canale che lo richiede â€” Brand Book v1.2 sez. 7)
- âŒ **Bloccare con ðŸ”´ per ottimizzazioni cosmetiche** (es. CSS minification senza impatto reale su CWV)

---

## 7. Compliance hooks

Verifica nel report:
- Disclaimer RUI presente nel footer site-wide (Brand Book v1.2 sez. 7) â†’ se assente, flag ðŸ”´ critico (compliance, non SEO)
- Denominazione "Studio Solutions S.r.l. â€” Advisory+" corretta in chi siamo e footer
- Numero RUI A000669271 visibile

Compliance Officer interviene se trova discrepanze a livello legale-formale.

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di auditare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 1 identitÃ  Â· sez. 7 Compliance Â· sez. 8 Design System)
2. `/01_Team/06_SEO_Specialist.md`
3. `config/brand.json` (sez. identitÃ , URL, sedi, disclaimer)
4. Output_approvati/seo/ technical-audit precedenti (per confronto trend)
5. Il brief operativo del MM (scope: full audit / quick check / post-deploy)

---

*SKILL v1.0 â€” advisory-plus:seo-technical-audit â€” Sessione 5 Plugin Build â€” 2026-05-20*

