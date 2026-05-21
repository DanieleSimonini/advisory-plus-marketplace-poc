---
name: production-asset-library
description: Gestisce la libreria asset visivi/audio/template del workspace Advisory+ in /04_Risorse/ (Loghi Â· Foto Â· Brand_Visual Â· Mandanti Â· Disclaimer Â· Compagine). Manutiene naming convention strutturato + index README per sottocartella + sync bidirezionale Cloudinary MCP (Sessione 8 wiring) per asset condivisi/CDN. Funzioni: registrazione nuovo asset (manuale via Write o auto da cc-nano-banana/Canva MCP output) Â· audit periodico orfani/duplicati/non-utilizzati Â· enforcement convention naming Â· gestione consensi foto persone (8 anagrafici pendenti â€” 4 soci + 4 senior advisor) Â· diritti d'uso loghi mandatarie (vincolo IVASS hard). Read-write su /04_Risorse/, log audit in /04_Risorse/_audit_log.md.
---
# ðŸ—ƒ Skill production-asset-library â€” Gestione libreria asset /04_Risorse/

> **Naming convention + index + Cloudinary sync + consensi foto + diritti loghi mandatarie.**

---

## 1. Quando triggera

- Invocata quando un nuovo asset viene generato (output da `visual/image-static-nano-banana` Â· da Canva MCP Â· da Cloudinary MCP Â· da Remotion render Â· da upload manuale CEO)
- Invocata in **audit trimestrale** schedulato (1Â° giorno del trimestre) â€” pulizia orfani Â· duplicati Â· non-utilizzati
- Invocata in **setup iniziale plugin v1.1** per definire schema + naming + index iniziale
- Invocata da `advisory-plus:visual/*` skill come dipendenza (recupero asset esistenti riusabili prima di generarne di nuovi)
- Invocata on-demand dal MM per registrazione asset critici (es. nuova foto consensata)

Tempo target di esecuzione: **15-30 min** per audit periodico, **<5 min** per registrazione singolo asset.

---

## 2. Struttura libreria asset

```
ðŸ“ /04_Risorse/
   â”œâ”€â”€ ðŸ“ Loghi/                    â€” loghi Advisory+ vector + raster
   â”‚   â”œâ”€â”€ Advisory + - Logo colori.svg
   â”‚   â”œâ”€â”€ Advisory+ - Logo bianco.svg
   â”‚   â””â”€â”€ (varianti PNG/PDF se esistono)
   â”‚
   â”œâ”€â”€ ðŸ“ Foto/                     â€” foto persone + sedi + ambient
   â”‚   â”œâ”€â”€ ðŸ“ Soci/                 â€” foto 4 soci (consenso scritto obbligatorio)
   â”‚   â”œâ”€â”€ ðŸ“ Senior_Advisor/       â€” foto 4 senior advisor (consenso scritto obbligatorio)
   â”‚   â”œâ”€â”€ ðŸ“ Sedi/                 â€” foto sedi GENERICHE (no panoramiche territoriali â€” Brand Book v1.2 sez. 2)
   â”‚   â”œâ”€â”€ ðŸ“ Ambient/              â€” foto ambientali non-identificabili (interni studio, scrivanie, dettagli)
   â”‚   â””â”€â”€ _CONSENSI.md             â€” registro consensi scritti (8 pendenti)
   â”‚
   â”œâ”€â”€ ðŸ“ Brand_Visual/             â€” Design System + template Cover Blog System
   â”‚   â”œâ”€â”€ Design_System_v1.html
   â”‚   â”œâ”€â”€ ðŸ“ Cover_blog_template/  â€” template Cover Blog System (5 categorie consolidate)
   â”‚   â”œâ”€â”€ ðŸ“ Highlight_IG/         â€” cover highlight permanenti (5 set Sessione 4)
   â”‚   â””â”€â”€ ðŸ“ Stories_template/     â€” template Stories ricorrenti
   â”‚
   â”œâ”€â”€ ðŸ“ Mandanti/                 â€” loghi compagnie mandatarie (uso SOLO disclosure)
   â”‚   â”œâ”€â”€ Generali_Italia_Cattolica.svg
   â”‚   â”œâ”€â”€ DAS_Difesa_Legale.svg
   â”‚   â”œâ”€â”€ UCA_Tutela_Legale_Peritale.svg
   â”‚   â”œâ”€â”€ Europ_Assistance.svg
   â”‚   â””â”€â”€ _DIRITTI_USO.md          â€” regole rigide uso loghi mandatarie
   â”‚
   â”œâ”€â”€ ðŸ“ Disclaimer/               â€” testi standard RUI/IVASS
   â”‚   â”œâ”€â”€ Disclaimer_RUI.md
   â”‚   â”œâ”€â”€ Disclaimer_Caso_Reale.md
   â”‚   â”œâ”€â”€ Disclaimer_AI_Avatar.md  â€” pendenza pre-go-live: validazione consulente privacy/legale esterno
   â”‚   â””â”€â”€ Disclaimer_Mandatarie.md
   â”‚
   â”œâ”€â”€ ðŸ“ Compagine/                â€” materiali identitari soci + senior advisor
   â”‚   â”œâ”€â”€ Compagine_Voci.md
   â”‚   â”œâ”€â”€ ðŸ“ Bio_soci/             â€” bio 80-120p ciascuna (4 pendenti)
   â”‚   â””â”€â”€ ðŸ“ Bio_senior_advisor/   â€” bio (4 pendenti)
   â”‚
   â””â”€â”€ ðŸ“ _audit_log.md             â€” log audit trimestrali
```

---

## 3. Naming convention obbligatoria

### Pattern generale
```
[Categoria]_[descrittore]_[dimensione]_[v[N]].[ext]
```

### Esempi
- `Cover_blog_LTC_caso_reale_1200x630_v2.png`
- `Foto_socio_Daniele_Simonini_ritratto_corporate_v1.jpg`
- `Highlight_IG_chi-siamo_1080x1920_v1.png`
- `Logo_Advisory_colori_3000x800_v1.svg`
- `Reel_intro_remotion_LTC_1080x1920_v1.mp4`

### Regole
- âœ… Lowercase per nomi descrittivi (eccetto sigle prodotto: LTC, TCM, RC, D&O)
- âœ… Underscore `_` come separatore (no spazi, no dash)
- âœ… Dimensioni nel formato `larghezza_x_altezza` per asset visivi
- âœ… Versione `v[N]` incrementale (no overwrite, sempre nuova versione)
- âœ… Estensione corretta (svg per vector, png per immagini brand, jpg per foto, mp4 per video, wav/mp3 per audio)
- âŒ No spazi nei nomi file (rotture su shell + URL)
- âŒ No caratteri speciali (italici, accenti, simboli) â€” usare ASCII
- âŒ No date nel nome file (le date sono nel git history / log audit)
- âŒ No nomi generici (`image1.png`, `final_FINAL_v2.png`)

---

## 4. Index README per sottocartella

Ogni sottocartella `/04_Risorse/[area]/` deve avere un `_INDEX.md` che lista gli asset presenti con metadata:

```markdown
# Index â€” [Nome cartella]

Ultimo aggiornamento: YYYY-MM-DD HH:MM

## Asset disponibili

| Filename | Tipo | Dimensione | Uso autorizzato | Note |
|---|---|---|---|---|
| Logo_Advisory_colori_3000x800_v1.svg | Vector | 3000Ã—800 | Tutti i canali | preferenziale per stampa |
| Foto_socio_Daniele_Simonini_ritratto_corporate_v1.jpg | Foto | 2400Ã—3000 | Pillar 2 Voce CEO Â· brochure Â· LinkedIn personale | consenso firmato 2026-04-15 |
| ... | ... | ... | ... | ... |

## Asset non-pubblicabili (in attesa)

| Filename | Ragione | Pendenza | Owner |
|---|---|---|---|
| Foto_socio_Agostini_v1.jpg | Manca consenso scritto | CEO da raccogliere | CEO |

## Audit history

[Audit trimestrali con esito sintetico, link a _audit_log.md]
```

---

## 5. Registro consensi foto (`/04_Risorse/Foto/_CONSENSI.md`)

```markdown
# Registro consensi foto persone

> **Vincolo Brand Book v1.2 sez. 7**: nessuna foto identificabile di persona puÃ² essere pubblicata senza consenso scritto. GDPR Art. 6 + 7.

## Soci (4 anagrafici)

| Persona | Consenso scritto | Data firma | Scope autorizzato | File foto |
|---|---|---|---|---|
| Daniele Simonini | â³ pendente | â€” | â€” | â€” |
| Antonio Agostini | â³ pendente | â€” | â€” | â€” |
| Michele Barrella | â³ pendente | â€” | â€” | â€” |
| Alberto Fappani | â³ pendente | â€” | â€” | â€” |

## Senior advisor (4 anagrafici)

| Persona | Consenso scritto | Data firma | Scope autorizzato | File foto |
|---|---|---|---|---|
| Daniele Roberto Cerioni | â³ pendente | â€” | â€” | â€” |
| Leonardo Roncoli | â³ pendente | â€” | â€” | â€” |
| Sergio Annunziata | â³ pendente | â€” | â€” | â€” |
| Annamaria Gardino | â³ pendente | â€” | â€” | â€” |

## Template scope autorizzato

- Pubblicazione su sito advisoryplus.it sezione "Chi siamo"
- Pubblicazione su blog THE ADVISOR articoli firmati
- Pubblicazione su pagina LinkedIn aziendale + profili personali
- Pubblicazione su brochure corporate
- Pubblicazione su newsletter footer Compagine
- Revocabile in qualsiasi momento con preavviso scritto
- NO uso per training AI Â· NO clone AI Â· NO doppiaggio AI (decisione CEO 2026-05-16 etica)
```

---

## 6. Diritti uso loghi mandatarie (`/04_Risorse/Mandanti/_DIRITTI_USO.md`)

```markdown
# Diritti uso loghi compagnie mandatarie

> **Vincolo IVASS HARD + Brand Book v1.2 sez. 7**: uso loghi compagnie mandatarie consentito ESCLUSIVAMENTE in disclosure footer di brochure/newsletter/blog/sito/brochure. MAI in cover, MAI nel corpo di un contenuto, MAI in post social, MAI come asset narrativo.

## Compagnie mandatarie

- **Generali Italia â€“ Cattolica Assicurazioni** (compagnia primaria multiramo)
- **DAS Difesa Legale**
- **UCA Tutela Legale e Peritale**
- **Europ Assistance**

## Denominazione corretta (sempre)

[Vedi `/04_Risorse/Disclaimer/Disclaimer_Mandatarie.md`]

## Uso consentito (esclusivamente)

âœ… Disclosure footer brochure
âœ… Disclosure footer newsletter
âœ… Sezione "Compagnie mandatarie" su sito advisoryplus.it
âœ… Disclosure footer YouTube descrizione (post-launch)

## Uso vietato (mai)

âŒ Cover blog Â· cover video Â· thumbnail YouTube
âŒ Post sociale LinkedIn Â· Instagram Â· Facebook
âŒ Stories Â· Reel Â· carousel
âŒ Body di articoli blog
âŒ Visual emozionali / narrativi
âŒ Co-branding con asset Advisory+ in modo che sembri "endorsement della compagnia"
âŒ Modifiche al logo originale (no riproporzione Â· no cambio colori Â· no overlay)

## Audit

Skill `advisory-plus:compliance-mandatarie-check` (Sessione 4) verifica uso loghi ad ogni invocazione visual brief.

## Pendenza

Se mandanti cambiano (revoca contratto, nuova compagnia), aggiornare immediatamente questo file + `config/brand.json` sez. mandanti.
```

---

## 7. Sync Cloudinary MCP (Sessione 8 wiring)

### Cosa va su Cloudinary
Asset destinati a CDN per uso multi-canale + trasformazioni automatiche:
- Loghi Advisory+ (con variants size automatiche)
- Cover blog (con resize automatici 1200Ã—630 OG Â· 1080Ã—1080 IG Â· 1080Ã—1350 Stories)
- Thumbnail YouTube
- Foto soci (con resize automatici varie dimensioni)
- Asset evergreen riusabili

### Cosa NON va su Cloudinary
- Asset una-tantum (es. visual specifico di una campagna chiusa)
- Asset in attesa consenso (foto persone non firmate)
- Disclaimer testuali (sono in /04_Risorse/Disclaimer/ locale)
- File audio voice-over Daniele autentici (privacy + non riusabili senza contesto)
- Asset con loghi mandatarie (gestione separata Â· IVASS sensibile)

### Direzione sync
- **Push**: skill registra nuovo asset â†’ upload Cloudinary â†’ URL salvato in `_INDEX.md`
- **Pull**: audit trimestrale verifica che asset su Cloudinary corrispondano a quelli in `/04_Risorse/` (no drift)
- **Tag Cloudinary**: ogni asset taggato con categoria + pillar + voce + data per query rapida da skill visual

---

## 8. Audit trimestrale (1Â° giorno del trimestre)

### Checklist audit

1. **Orfani**: file in `/04_Risorse/` non referenziati da nessuna SKILL.md Â· `_INDEX.md` Â· Output_approvati/
   - Esito ðŸŸ¡: spostamento in `/04_Risorse/_archivio_orfani/`
   - Esito ðŸ”´: cancellazione previa approvazione MM

2. **Duplicati**: stesso asset in piÃ¹ sottocartelle o con versioni multiple non incrementali
   - Esito ðŸŸ¡: consolidamento in 1 versione + redirect dagli altri
   - Esito ðŸ”´: cancellazione duplicati previa approvazione MM

3. **Naming non conforme**: asset con nomi non rispettano convention (sez. 3)
   - Esito ðŸŸ¡: proposta rename + esecuzione previa approvazione MM

4. **Consensi foto pendenti**: verifica `_CONSENSI.md` aggiornato
   - Esito ðŸ”´: rimozione foto da `_INDEX.md` finchÃ© consenso non firmato

5. **Loghi mandatarie**: verifica uso solo in disclosure (cross-check con Output_approvati)
   - Esito ðŸ”´: alert immediato CEO + Compliance Officer

6. **Cloudinary sync drift**: verifica asset Cloudinary corrispondono a `/04_Risorse/`
   - Esito ðŸŸ¡: re-sync + log discrepanze

7. **Asset non-utilizzati >12 mesi**: candidati ad archiviazione
   - Esito ðŸŸ¡: spostamento in `/04_Risorse/_archivio_inattivi/` (recoverable)

### Output audit

File in `/04_Risorse/_audit_log.md` (append-only):
```markdown
## Audit del YYYY-MM-DD (Q[N] [anno])

**Risultati:**
- N asset totali in libreria
- N orfani rilevati Â· esito
- N duplicati rilevati Â· esito
- N naming non conformi Â· esito
- N consensi pendenti
- N asset Cloudinary in drift Â· esito
- N asset non-utilizzati >12 mesi Â· esito

**Azioni eseguite:** [...]

**Azioni in attesa approvazione MM:** [...]
```

---

## 9. Pendenze critiche correnti (riferimento Verbale chat 10 + chat 09 Brand Identity)

### Pendenze identitate consensi foto (8 anagrafici)
- 4 soci: Daniele Simonini Â· Antonio Agostini Â· Michele Barrella Â· Alberto Fappani
- 4 senior advisor: Daniele Roberto Cerioni Â· Leonardo Roncoli Â· Sergio Annunziata Â· Annamaria Gardino
- **Responsabile**: CEO (raccolta consensi + sessione fotografica)
- **Blocca**: footer newsletter Compagine Â· pagina chi siamo sito Â· brochure corporate identitarie

### Pendenza bio sintetiche 4 soci
- 80-120 parole ciascuna, in `/04_Risorse/Compagine/Bio_soci/`
- **Responsabile**: CEO o brief da CEO con raccolta da skill `voce-spiegato-facile`
- **Blocca**: footer newsletter Â· pagina chi siamo

### Pendenza AI disclosure formulazione
- File `/04_Risorse/Disclaimer/Disclaimer_AI_Avatar.md` resta in stato "draft" finchÃ© consulente privacy/legale esterno non valida formulazione
- **Responsabile**: CEO (incarico esterno) + Compliance Officer (review)
- **Blocca**: lancio YouTube con avatar HeyGen (target giugno-luglio 2026)

### Pendenza decisione formale ordine alfabetico 4 soci
- Raccomandazione MM: Agostini Â· Barrella Â· Fappani Â· Simonini (alfabetico)
- **Responsabile**: CEO (decisione formale)
- **Impatta**: footer newsletter Compagine Â· pagina chi siamo Â· brochure

---

## 10. Logica di esecuzione â€” passo-passo

### ModalitÃ  A â€” Registrazione nuovo asset
1. Ricevere brief (path file + categoria + metadata)
2. Verificare naming convention (sez. 3) â€” proporre rename se non conforme
3. Spostare file in sottocartella corretta `/04_Risorse/[area]/`
4. Aggiornare `_INDEX.md` della sottocartella con metadata
5. Se asset Ã¨ "Cloudinary-eligible" (sez. 7): trigger upload Cloudinary
6. Log registrazione in `_audit_log.md`

### ModalitÃ  B â€” Audit trimestrale
1. Eseguire i 7 check (sez. 8)
2. Compilare report audit
3. Eseguire azioni automatiche (es. spostamento orfani)
4. Notificare MM per azioni che richiedono approvazione
5. Append in `_audit_log.md`

### ModalitÃ  C â€” Recupero asset esistente (per skill visual)
1. Skill chiamante (es. `visual/cover-blog`) interroga `_INDEX.md` per categoria + pillar
2. Restituisce lista asset riusabili + URL Cloudinary
3. Se nessun asset corrispondente: handoff a `visual/image-static-nano-banana` per generazione

---

## 11. Cosa NON fare mai

- âŒ **Pubblicare foto persone senza consenso scritto** verificato in `_CONSENSI.md`
- âŒ **Usare loghi mandatarie fuori da disclosure** (mai cover, mai body â€” IVASS hard)
- âŒ **Modificare loghi mandatarie** (riproporzione, colori, overlay vietati)
- âŒ **Cancellare asset senza approvazione MM** (sempre spostamento `_archivio_*`, mai delete diretto)
- âŒ **Naming generico** (`image1.png`, `final.jpg`)
- âŒ **Overwrite versioni precedenti** (sempre `v[N+1]`, mai sovrascrivere)
- âŒ **Sync Cloudinary di asset sensibili** (foto non-consensate, voice-over Daniele autentici, loghi mandatarie)
- âŒ **Skip audit trimestrale** (libreria si gonfia di orfani Â· drift Cloudinary Â· consensi scaduti)
- âŒ **Asset con riferimenti territoriali** (foto sede con cartello "Versilia" â€” Brand Book v1.2 sez. 2)
- âŒ **Caratteri speciali nei nomi file** (rotture shell + URL)

---

## 12. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di operare sulla libreria, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 1 identitÃ  Â· sez. 7 Compliance + GDPR Â· sez. 8 Design System)
2. `/01_Team/05_Art_Director.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (mandatarie Â· disclaimer Â· sedi) + `config/compagine.json`
4. `_INDEX.md` di tutte le sottocartelle `/04_Risorse/`
5. `_CONSENSI.md` per verificare stato consensi foto
6. `_DIRITTI_USO.md` per verifica regole mandatarie
7. `_audit_log.md` per storico audit
8. Il brief operativo del MM o cron trimestrale

---

*SKILL v1.0 â€” advisory-plus:production-asset-library â€” Sessione 6 Plugin Build â€” 2026-05-21*

