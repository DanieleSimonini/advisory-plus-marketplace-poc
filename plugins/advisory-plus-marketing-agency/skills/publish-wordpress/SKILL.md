---
name: publish-wordpress
description: Pubblicazione automatica articoli blog "THE ADVISOR" su advisoryplus.it via WordPress REST API nativa (`/wp-json/wp/v2/`) con Basic Auth Application Password. Sito Ã¨ WordPress.org self-hosted (verificato 2026-05-19), NON WordPress.com â€” questa SKILL Ã¨ stata riscritta in v1.1.3 dopo il rilevamento della discrepanza architetturale (decisione CEO 2026-05-19 "patch immediato pre go-live"). Supporta: articoli evergreen 1500-2500p Â· short news 600-1000p Â· Caso Reale 1200-1500p Â· Analisi tecnica 1500-2500p Â· firma autoriale (Daniele/Brand/altri soci) Â· cover Cover Blog System 1200Ã—630 OG con consolidamento categoria ðŸ“Š Analisi Â· meta title â‰¤60 char + meta description â‰¤155 char Â· slug URL kebab-case Â· internal linking 2-4 Â· schema markup Article + Organization JSON-LD Â· disclaimer RUI integrale in fondo Â· categorie blog (Educazione Â· Caso Reale Â· Analisi Â· Voce CEO Â· News) con risoluzione automatica taxonomy slug â†’ integer ID via REST API. Doppio gate Compliance T-30min + SEO on-page check via `advisory-plus:seo-on-page-analysis` prima della pubblicazione. Tutta logica tecnica delegata a `scripts/publish-wordpress.sh` (v1.1.3 REST API self-hosted). Screenshot post-publish + log permalink.
---
# ðŸ“° Skill publish-wordpress â€” Blog THE ADVISOR su advisoryplus.it (REST API self-hosted)

> **WordPress.org self-hosted Â· REST API nativa /wp-json/wp/v2/ Â· Basic Auth Application Password Â· 5 categorie editoriali Â· SEO on-page check Â· Cover Blog System Â· gate-doppio.**
> **Riscritta in v1.1.3 (patch architetturale immediato decisione CEO 2026-05-19).**

---

## 1. Quando triggera

- Invocata dal MM su slot blog programmato (frequenza standard: 1 art/sett ~4-6/mese)
- Invocata da `publish/scheduling` orchestrator a T-30min dallo slot programmato (cron-driven)
- Mai auto-trigger: serve sempre articolo giÃ  approvato in `Output_approvati/` con stato `pronto_per_pubblicazione`

Tempo target di esecuzione: **5-8 minuti** (skill orchestrazione) + ~10 sec REST API call effettiva.

---

## 2. Output finale atteso

Risposta JSON al chiamante con metadata pubblicazione:

```json
{
  "status": "published",
  "wordpress_post_id": 1234,
  "permalink": "https://advisoryplus.it/blog/long-term-care-cos-e-quando-serve/",
  "scheduled_date": "2026-05-26T09:00:00+02:00",
  "categoria_wp_id": 12,
  "tag_wp_ids": [45, 46, 47, 48],
  "featured_media_id": 567,
  "schema_jsonld_inserted": true,
  "disclaimer_rui_verified": true,
  "compliance_gate": "green",
  "brand_strategist_gate": "green",
  "screenshot_path": "Output_approvati/[file]_assets/screenshot_published.png",
  "log_path": "05_Calendario_editoriale/Log_pubblicati/2026-05_master_log.md"
}
```

---

## 3. Specifiche WordPress.org self-hosted Advisory+

### Stack tecnico
- **CMS:** WordPress.org self-hosted (NON WordPress.com hosted)
- **URL admin:** `https://advisoryplus.it/wp-admin/`
- **Permalink struttura:** `/%postname%/` ("Nome articolo" verificato 2026-05-19) â€” gli articoli sono in **root del dominio**, NON sotto `/blog/`. URL articolo: `https://advisoryplus.it/{slug}/`. L'URL `/blog/` visibile nei menu Ã¨ di norma una archive page personalizzata, non un parent path reale.
- **REST API endpoint base:** `https://advisoryplus.it/wp-json/wp/v2/`
- **Authentication:** **Application Password** (WordPress core feature dal 5.6, raccomandata per integrazione API) con header `Authorization: Basic base64(username:app_password)`
- **NO OAuth** (Ã¨ solo per WordPress.com hosted, non applicabile qui)
- **NO JWT** (richiederebbe plugin terzo tipo JWT Authentication, evitato per ridurre superficie di attacco)

### Env variables richieste (`config/wordpress.env`)
```env
WORDPRESS_BASE_URL=https://advisoryplus.it
WORDPRESS_REST_ENDPOINT=https://advisoryplus.it/wp-json/wp/v2
WORDPRESS_USERNAME=[username admin]
WORDPRESS_APP_PASSWORD=[application password senza spazi, 24 char]
WORDPRESS_BLOG_PATH_PREFIX=/blog
WORDPRESS_AUTH_TYPE=basic_auth_app_password
WORDPRESS_DEFAULT_AUTHOR_ID=1
WORDPRESS_TIMEOUT_SECONDS=30
```

### Endpoint REST API usati

| Endpoint | Metodo | Uso |
|---|---|---|
| `/wp-json/wp/v2/posts` | POST | Crea articolo (status=publish o status=future per scheduling) |
| `/wp-json/wp/v2/posts/{id}` | GET | Verifica post creato + permalink |
| `/wp-json/wp/v2/media` | POST (multipart) | Upload immagine cover blog (featured_media) |
| `/wp-json/wp/v2/categories?slug={slug}` | GET | Risoluzione categoria slug â†’ integer ID |
| `/wp-json/wp/v2/tags?slug={slug}` | GET | Risoluzione tag slug â†’ integer ID |
| `/wp-json/wp/v2/tags` | POST | Creazione tag se non esistente |

### Payload POST `/posts` (esempio)

```json
{
  "title": "Long Term Care: cos'Ã¨, perchÃ© in Italia se ne parla poco, quando attivarla",
  "slug": "long-term-care-cos-e-quando-serve",
  "content": "<HTML completo dell'articolo con schema JSON-LD inline + disclaimer RUI>",
  "excerpt": "Long Term Care spiegata semplice: cos'Ã¨, perchÃ© in Italia Ã¨ poco diffusa, a chi serve, quando attivarla.",
  "status": "future",
  "date": "2026-05-26T09:00:00",
  "date_gmt": "2026-05-26T07:00:00",
  "categories": [12],
  "tags": [45, 46, 47, 48],
  "featured_media": 567,
  "author": 1,
  "comment_status": "closed",
  "ping_status": "closed",
  "meta": {
    "_yoast_wpseo_title": "Long Term Care: cos'Ã¨ e quando serve davvero | Advisory+",
    "_yoast_wpseo_metadesc": "Long Term Care spiegata semplice: cos'Ã¨, perchÃ© in Italia Ã¨ poco diffusa, a chi serve, quando attivarla. Guida del consulente Advisory+.",
    "_yoast_wpseo_canonical": "https://advisoryplus.it/blog/long-term-care-cos-e-quando-serve/"
  }
}
```

Nota: i campi `meta._yoast_wpseo_*` funzionano solo se sul sito Ã¨ installato **Yoast SEO** o **Rank Math**. Verificare al primo run; in alternativa usare custom field generici o plugin SEO API equivalente.

### Risoluzione taxonomy (categoria + tag)

Le categorie e tag in WP REST API si passano come **array di integer ID**, NON come slug stringhe. Procedura:

1. GET `/categories?slug={slug_categoria}` â†’ estrai `id` dal primo risultato
2. Se categoria non esiste â†’ ðŸ”´ blocco (le 5 categorie editoriali devono pre-esistere sul sito, creare manualmente se necessario)
3. Per ogni tag: GET `/tags?slug={slug_tag}` â†’ se esiste prendi `id`, se non esiste POST `/tags` con `{"name": "...", "slug": "..."}` per crearlo

### Upload media (featured_image)

Per la cover blog 1200Ã—630 OG:

1. POST `/wp-json/wp/v2/media` con header `Content-Disposition: attachment; filename="cover_og.jpg"` + binary body del file
2. WordPress restituisce `{"id": 567, "source_url": "..."}` 
3. Salvare `id` come `featured_media` nel payload POST `/posts`
4. Settare `alt_text` via PATCH `/media/{id}` se necessario

### Disclaimer RUI hard

Validazione pre-call OBBLIGATORIA: il `content` HTML del post DEVE contenere la stringa esatta `"RUI Sez. A n. A000669271"`. Se assente â†’ ðŸ”´ blocco, log warning, notifica MM.

### Schema markup JSON-LD

Skippato per ora se Yoast SEO o Rank Math Ã¨ installato (lo iniettano automaticamente). Se nessun plugin SEO Ã¨ installato â†’ la skill inserisce manualmente `<script type="application/ld+json">` con schema Article + Organization in coda al `content` HTML.

### Categorie editoriali blog â€” 4 voci (modello ibrido v1.1.4)

**Decisione CEO 2026-05-19 Opzione C: categoria WP = voce editoriale Brand Book v1.2 sez. 4.**

| Slug WP | Display | Voce editoriale | Cat ID |
|---|---|---|---|
| `spiegato-facile` | Spiegato Facile | ðŸ§  Spiegato Facile | 25 |
| `badvisor` | Badvisor | ðŸ”¥ Badvisor | 26 |
| `caso-reale` | Caso Reale | ðŸ“– Caso Reale | 27 |
| `analisi` | Analisi | ðŸ“Š Analisi *(nuova v1.2)* | 136 |

**Categoria fallback default:**
| Slug | Display | Uso |
|---|---|---|
| `senza-categoria` | Senza categoria | Default WP fallback (cat ID 1), invisibile in front-end (count 0). Mai usata dal plugin per pubblicazioni â€” solo backup |

âš ï¸ Le 4 categorie sono **pre-esistenti** sul sito (setup completato Sessione 16 via `setup_taxonomy.ps1`). Plugin verifica esistenza ID al primo run; se IDs non corrispondono â†’ notifica MM (situazione critica: ricreare via setup_taxonomy.ps1).

âš ï¸ **NON esistono piÃ¹ categorie "Educazione", "Voce CEO", "News di settore"** (modello v1.1.3 deprecato). Queste dimensioni sono codificate come **tag**:
- Educazione â†’ tag pillar `educazione-assicurativa` (ID 137)
- Voce CEO â†’ tag attributo `voce-advisor` (ID 149) â€” NB: NON `voce-ceo` per Brand Book sez. 12.1
- News â†’ tag attributo `news-reattiva` (ID 150) + tag pillar `news-settore` (ID 139)

### Tag editoriali blog â€” 26 totali (modello ibrido v1.1.4)

**3 famiglie di tag:**

#### Pillar (12 tag â€” Brand Book v1.2 sez. 6)
| Slug | Tag ID | | Slug | Tag ID |
|---|---|---|---|---|
| `educazione-assicurativa` | 137 | | `casa-patrimonio` | 144 |
| `identita-consulente` | 138 | | `imprese-professionisti` | 145 |
| `news-settore` | 139 | | `mare-yacht` | 146 |
| `famiglia-vita` | 140 | | `arte-patrimonio` | 147 |
| `anzianita-ltc` | 141 | | `enti-religiosi-terzo-settore` | 148 |
| `risparmio-investimento` | 142 | | | |
| `tutela-legale` | 143 | | | |

#### Attributi (5 tag)
| Slug | Tag ID | Uso |
|---|---|---|
| `voce-advisor` | 149 | Articolo firmato da socio o senior advisor |
| `news-reattiva` | 150 | Pubblicato entro 48h da evento |
| `evergreen` | 151 | Articolo timeless deep-dive |
| `caso-reale-disclaimer` | 152 | Disclaimer "Caso reale, nomi di fantasia" |
| `specialty-drop` | 153 | Drop trimestrale Specialty |

#### Segmenti (9 tag â€” Brand Book v1.2 sez. 3)
| Slug | Tag ID | | Slug | Tag ID |
|---|---|---|---|---|
| `giovani-genitori` | 154 | | `pmi-famigliari` | 159 |
| `adulti-con-anziani` | 155 | | `imprese-strutturate` | 160 |
| `pre-pensionati` | 156 | | `terzo-settore` | 161 |
| `patrimonializzati` | 157 | | `specialty-verticali` | 162 |
| `professionisti-partite-iva` | 158 | | | |

**Tag tipici per articolo:** 3-6 totali (1 pillar obbligatorio + 0-2 attributi + 0-2 segmenti).

---

## 4. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** dal MM o dall'orchestrator `publish/scheduling`: articolo path + data pubblicazione + cover image path
2. **Eseguire kickoff** per contesto workspace
3. **Verifica kill switch globale** (`config/AUTOMAZIONE_ATTIVA=true`)
4. **Verifica modalitÃ  ferie/crisi** (se attive â†’ blocco con notifica)
5. **Leggere articolo + frontmatter YAML** dal file Markdown
6. **Validazione hard pre-call**:
   - Disclaimer RUI presente nel content (`grep "RUI Sez. A n. A000669271"`)
   - Meta title â‰¤ 60 caratteri
   - Meta description â‰¤ 155 caratteri
   - Slug â‰¤ 60 char, kebab-case, ASCII-only
   - Categoria editoriale valida (1 delle 5)
   - Tag presenti (4-6 raccomandati)
7. **Invocare `compliance/gate-doppio`** via Task tool (T-30min check)
   - Se ðŸ”´ â†’ blocco assoluto + email alert CEO entro 1h
   - Se ðŸŸ¡ â†’ riformulazione con CEO approval o auto-revert
   - Se ðŸŸ¢ â†’ procedi
8. **Invocare `seo/on-page-analysis`** via Task tool (18 voci checklist read-only)
   - Output report â†’ archivia in log
9. **Risolvere taxonomy**: categoria slug â†’ ID + tag slugs â†’ IDs (creando tag se non esistenti)
10. **Upload featured_image** via `/wp-json/wp/v2/media` â†’ ottenere media ID
11. **Convertire Markdown â†’ HTML** (skill interna: pandoc o markdown-it via Bash, con whitelist tag HTML)
12. **Iniettare schema JSON-LD** se nessun plugin SEO rilevato
13. **POST `/wp-json/wp/v2/posts`** via `scripts/publish/publish-wordpress.sh` con payload completo
14. **Polling stato post** (3 attempts Ã— 2 sec) per verifica permalink generato
15. **Screenshot post-publish** via Chrome MCP (apre permalink, scatta screenshot 1920Ã—1080) â†’ salva in `Output_approvati/[file]_assets/`
16. **Loggare** in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_master_log.md` con: data, post_id, permalink, categoria, tag, autore, compliance gate, durata
17. **Aggiornare calendario editoriale** dello slot a stato `Pubblicato`
18. **Restituire metadata** al chiamante (JSON sez. 2)

---

## 5. Casi particolari

### REST API disabilitata sul sito (404 su `/wp-json/`)
- ðŸ”´ blocco generazione
- Cause comuni: plugin di security (Wordfence, iThemes Security) che disabilitano REST API endpoint, oppure custom code in `functions.php`
- Notifica MM con istruzione: "Verifica in WP admin â†’ Tools â†’ Site Health o disabilita temporaneamente plugin di security per testare. Fallback: ripristina pubblicazione manuale via freelance."

### Application Password invalida (401 Unauthorized)
- ðŸ”´ blocco
- Cause: password scaduta/revocata, username errato, base64 encoding fallito
- Notifica MM: "Application Password WordPress non valida. Genera nuova in wp-admin â†’ Utenti â†’ Profilo â†’ Application Passwords. Aggiorna `config/wordpress.env`."

### Capability missing (403 Forbidden)
- ðŸ”´ blocco
- Cause: user non ha capability `edit_posts` o `publish_posts`
- Notifica MM: "User WordPress senza permessi pubblicazione. Verifica ruolo in WP admin â†’ Utenti (deve essere Administrator o Editor)."

### Categoria editoriale mancante sul sito
- ðŸ”´ blocco
- Notifica MM: "Categoria `{slug}` non presente in WP. Creare manualmente in wp-admin â†’ Articoli â†’ Categorie."

### Pubblicazione scheduling (future)
- Usare `status=future` + campo `date` formato ISO 8601 con timezone Europe/Rome
- WordPress eseguirÃ  il cron interno per pubblicare alla data â€” verificare che `wp-cron` sia funzionante (alternativa: cron di sistema)

### Articolo Badvisor (raro su blog)
- Verifica quota mensile 20% Badvisor cumulato (lookup calendario editoriale)
- Se quota giÃ  satura â†’ ðŸŸ¡ raccomanda rinvio o riformulazione voce

### Pubblicazione articolo firmato Daniele
- Verifica firma "Daniele Simonini, Agent, Admin & Advisor" (mai "CEO") nel content
- Categoria forzata `voce-ceo`
- Notifica MM: questa Ã¨ "modalitÃ  semi-manuale" â€” Daniele clicca finale come per LinkedIn personale? (vedi sez. 6)

### Rate limiting
- WordPress nativo non rate-limit di default, ma plugin security potrebbero
- Se 429 â†’ backoff esponenziale 5/15/45 sec, max 3 retry

---

## 6. Pubblicazione articoli firmati Daniele â€” semi-manuale?

**Decisione MM pending CEO:** per coerenza con il pattern LinkedIn personale Daniele (Brand Book v1.2 sez. 13.10), articoli categoria `voce-ceo` sul blog richiedono click finale CEO o pubblicazione automatica come gli altri?

- **Opzione A** â€” Tutti automatici (anche `voce-ceo`): coerente con resto blog, freelance era giÃ  automatico â†’ switch totale
- **Opzione B** â€” Solo `voce-ceo` semi-manuale: skill prepara payload + apre Chrome MCP a wp-admin â†’ CEO clicca "Pubblica" â†’ polling permalink. Coerente con asimmetria etica LinkedIn personale.
- **Opzione C** â€” Tutti semi-manuali: troppo costoso (1 click CEO per ogni articolo blog â†’ vanifica automazione)

**Raccomandazione MM (default in v1.1.3 fino a decisione):** Opzione A (tutti automatici), motivazione: il blog Ã¨ canale brand "La redazione Advisory+" by default, non firma autoriale 1:1 come LinkedIn personale; il caso `voce-ceo` Ã¨ un'eccezione minoritaria (~4-6 articoli/anno), il content Ã¨ giÃ  stato approvato dal CEO nella sessione di stesura della chat 04 Blog â†’ seconda approvazione runtime sarebbe ridondante.

---

## 7. Cosa NON fare mai

- âŒ **Pubblicare senza disclaimer RUI integrale** nel content (hard rule)
- âŒ **Salvare Application Password nel build tree del plugin** (deve restare solo in `config/_local/wordpress.env` gitignored)
- âŒ **Esporre credenziali in log** (mascherare username + password in tutti i log)
- âŒ **Saltare il compliance gate-doppio** prima della pubblicazione
- âŒ **Skippare il SEO on-page check** (18 voci checklist obbligatoria)
- âŒ **Loghi mandatarie nel content body** (solo in disclosure footer, IVASS hard)
- âŒ **Riferimenti territoriali** in articoli evergreen (posizionamento nazionale)
- âŒ **External linking a competitor** (vietato Brand Book)
- âŒ **Promesse rendimenti garantiti** o claim assoluti
- âŒ **Pubblicare in `status=publish` senza screenshot post-publish** (audit trail incompleto)
- âŒ **Modificare manualmente in wp-admin un articolo pubblicato dal plugin** (rompe coerenza log) â€” se serve correzione, passare dal plugin con `update-wordpress-post` skill
- âŒ **Sforare timeout REST API** (default 30 sec; se piÃ¹ lungo â†’ indica problema infrastruttura, notifica MM)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pubblicare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia canale blog Â· sez. 6 Pillar Map Â· sez. 7 Compliance â€” disclaimer blog integrale Â· sez. 13.10 Publishing Automation Map post-Onda 4)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/04_Compliance_Officer.md` Â· `/01_Team/06_SEO_Specialist.md`
3. `config/brand.json` (mapping voce-canale, frequenze blog, dosaggio Badvisor 20%, disclaimer standard)
4. `config/wordpress.env` (credenziali REST API)
5. `config/AUTOMAZIONE_ATTIVA` (kill switch globale)
6. `docs/SETUP_WORDPRESS.md` (procedura Application Password + troubleshooting + scope freelance post-patch)
7. Articolo da pubblicare in `Output_approvati/04_Blog_THE_ADVISOR/`
8. Calendario editoriale `/05_Calendario_editoriale/[YYYY-MM]_*.md` per slot programmato

---

## 9. Migrazione v1.1.2 â†’ v1.1.3 â€” cosa Ã¨ cambiato

| Aspetto | v1.1.2 (e precedenti) | v1.1.3 |
|---|---|---|
| CMS target dichiarato | WordPress.com hosted | **WordPress.org self-hosted** |
| API endpoint | `public-api.wordpress.com/rest/v1.1/sites/{id}/posts/new` | **`advisoryplus.it/wp-json/wp/v2/posts`** |
| Auth | OAuth Automattic | **Basic Auth Application Password** |
| MCP wired | `wordpress-com` (nel manifest) | `wordpress-rest-api` (custom shell script wrapper, no MCP ufficiale) |
| Credenziali | Client ID + Client Secret + OAuth tokens | Username + Application Password |
| Setup time primo run | ~5 min OAuth flow browser | ~60 sec (genera Application Password in wp-admin) |
| Site ID required | SÃ¬ | No (usa direttamente URL base) |

**Razionale del cambio (decisione CEO 2026-05-19):** verifica diretta del CEO che `advisoryplus.it/wp-admin/` Ã¨ WordPress.org self-hosted, non WordPress.com. Patch immediato pre-go-live invece di rinvio a Onda 2 per evitare gap funzionale al go-live del 31 maggio.

---

*SKILL v1.1.4 â€” advisory-plus:publish-wordpress â€” Sessione 16 Plugin Build patch taxonomy ibrida â€” 2026-05-19*
*Update v1.1.4: ristrutturazione modello taxonomy WordPress secondo decisione CEO 2026-05-19 Opzione C (modello ibrido SEO). Categoria WP = voce editoriale (4: spiegato-facile, caso-reale, badvisor, analisi). Tag = 12 pillar + 5 attributi + 9 segmenti (totale 26). IDs WordPress codificati nel manifest plugin (cat 25/26/27/136, tag 137-162). Setup completato via `setup_taxonomy.ps1` + `fix_default_category.ps1` 2026-05-19.*
*Storia v1.1.3 (precedente, Sessione 15): riscritta integralmente da v1.0 (Sessione 7) per WordPress.org self-hosted REST API + Basic Auth Application Password. Decisione CEO Opzione B "patch immediato pre go-live".*

