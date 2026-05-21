---
name: compliance-disclaimer-rui
description: Genera il disclaimer RUI Advisory+ adatto al canale di destinazione (Brand Book v1.2 sez. 7). Restituisce la formulazione corretta per ciascun contesto: integrale per brochure stampate, completo per blog/newsletter/sito/email/descrizione YouTube, parziale per bio social (LinkedIn brand, Instagram, Facebook), assente per Stories (limite formato â€” la bio fa copertura). Triggera automaticamente da skill content-* prima dell'output finale. Triggera anche manualmente via /adv-disclaimer-rui [canale] per generare formula on-demand. Garantisce coerenza cross-canale e aggiornamento automatico se il dato societario cambia (RUI Sez. A n. A000669271 sempre, sede legale Via Marco Polo 180/C 55049 Viareggio LU sempre, denominazione "Studio Solutions S.r.l. â€” Advisory+" sempre). Una sola fonte di veritÃ  per tutti i disclaimer pubblicati.
---
# ðŸ“œ Skill compliance-disclaimer-rui â€” Generator disclaimer RUI per canale

> **Una sola fonte di veritÃ  per tutti i disclaimer Advisory+. Coerenza cross-canale garantita. Brand Book v1.2 sez. 7.**

---

## 1. Quando triggera

- **Automatico**: invocata dalle skill content-* (content-blog-article, content-newsletter, content-brochure, content-youtube-video) per inserire disclaimer corretto nel file finale
- **Manuale**: invocata via `/adv-disclaimer-rui [canale]` per generare formula on-demand
- **Manuale audit**: invocata via `/adv-disclaimer-rui audit` per verificare che disclaimer di contenuti giÃ  pubblicati siano allineati alla formula corrente

Tempo target: **<30 secondi** (lookup e return).

---

## 2. Output finale atteso

**Stringa Markdown** consegnata al chiamante:

```markdown
[Formula disclaimer adatta al canale richiesto]
```

Senza preamboli o commenti aggiuntivi nel return.

---

## 3. Formule disclaimer per canale

### Canale: `brochure` (stampati corporate)
**Formulazione INTEGRALE estesa**

```
Studio Solutions S.r.l. â€” Advisory+ â€” Sede legale: Via Marco Polo 180/C, 55049 Viareggio (LU).
Iscritta al RUI Sez. A n. A000669271, soggetta a vigilanza IVASS.

Mandati con: Generali Italia â€“ Cattolica Assicurazioni, DAS Difesa Legale, UCA Tutela Legale e Peritale, Europ Assistance.

Le informazioni contenute in questo materiale hanno scopo informativo e non costituiscono offerta di prodotti assicurativi nÃ© consulenza personalizzata. Prima della sottoscrizione di qualsiasi prodotto assicurativo, leggere attentamente il set informativo precontrattuale e contrattuale, disponibile presso le nostre sedi e sul sito web della compagnia mandante.

Per maggiori informazioni: www.advisoryplus.it â€” tel. [da inserire] â€” email: info@advisoryplus.it
```

### Canale: `blog`, `newsletter`, `sito`, `email`, `descrizione_youtube`
**Formulazione COMPLETA standard**

```
Studio Solutions S.r.l. â€” Advisory+ â€” Iscritta RUI Sez. A n. A000669271, soggetta a vigilanza IVASS. Informazioni a scopo informativo, non vincolanti. Prima della sottoscrizione leggere il set informativo.
```

### Canale: `bio_linkedin_brand`, `bio_instagram`, `bio_facebook`
**Formulazione COMPATTA per bio social**

```
Advisory+ Â· Studio Solutions S.r.l. Â· RUI Sez. A n. A000669271 Â· IVASS Â· www.advisoryplus.it
```

### Canale: `bio_linkedin_daniele` (profilo personale Daniele Simonini)
**Formulazione COMPATTA per bio personale**

```
Agent, Admin & Advisor Â· Advisory+ (Studio Solutions S.r.l.) Â· RUI Sez. A n. A000669271
```

### Canale: `stories_ig`, `stories_fb`
**ASSENTE** (limite formato â€” la bio del profilo fa copertura, Brand Book v1.2 sez. 7)

Output: stringa vuota + nota informativa:
```
[Nessun disclaimer in Stories â€” bio profilo fa copertura. Verifica bio in regola via /adv-bio-audit.]
```

### Canale: `post_linkedin_brand`, `post_linkedin_daniele`, `post_facebook`, `caption_instagram`, `caption_reel`
**ASSENTE nel singolo post** â€” la bio del profilo/pagina fa copertura per la sezione "intermediario assicurativo"

Eccezione: se il post **cita prodotti specifici** o **invita alla sottoscrizione** â†’ aggiungere mini-disclaimer in coda:
```
*Per dettagli su prodotti e condizioni, scrivici: info@advisoryplus.it Â· www.advisoryplus.it*
```

### Canale: `whatsapp_business_utility` (comunicazioni 1:1)
**Formulazione COMPATTA personalizzata** (al primo contatto di una conversazione)

```
Salve, sono [Nome operatore Advisory+]. Studio Solutions S.r.l. â€” Advisory+ â€” RUI Sez. A n. A000669271 â€” IVASS.
Le comunicazioni via WhatsApp hanno scopo informativo. Per offerte e contratti, ci sentiamo via email o di persona.
```

---

## 4. Aggiunte condizionali

### Se il contenuto cita mandatarie (qualsiasi canale)
Aggiungere sezione in disclosure:
```
Mandati con: Generali Italia â€“ Cattolica Assicurazioni, DAS Difesa Legale, UCA Tutela Legale e Peritale, Europ Assistance.
```

(NB: in canali compatti come bio social, omettere; in canali completi/integrali, includere sempre)

### Se il contenuto Ã¨ un Caso Reale (qualsiasi canale, anche Stories)
Aggiungere in coda al contenuto (NON nel disclaimer RUI):
```
*Caso reale, nomi di fantasia.*
```

### Se il contenuto usa AI generativa (HeyGen avatar, eventuali AI doppiaggio futuri)
Aggiungere AI disclosure (gestita da skill separata `advisory-plus:compliance-ai-disclosure`):
```
[Vedi skill compliance-ai-disclosure per formulazione AI Act UE artt. 50, 52]
```

### Se il contenuto Ã¨ una partnership/co-marketing
Aggiungere riferimento partner in disclosure:
```
In partnership con [Nome Partner â€” eventuale ruolo].
```

---

## 5. Dati societari fonte di veritÃ 

**Tutti i disclaimer attingono da `config/brand.json`**, mai hard-coded nelle skill content-*. Questo garantisce che eventuali modifiche societarie (cambio sede, aggiornamento mandati, nuovo numero RUI per ipotesi di rebranding) si propaghino automaticamente.

Campi attesi in `config/brand.json` sez. `identita`:
- `denominazione_legale`: "Studio Solutions S.r.l."
- `marchio_commerciale`: "Advisory+"
- `rui_sezione`: "A"
- `rui_numero`: "A000669271"
- `sede_legale`: "Via Marco Polo 180/C, 55049 Viareggio (LU)"
- `vigilanza`: "IVASS"
- `sito_web`: "www.advisoryplus.it"
- `email_contatto`: "info@advisoryplus.it"
- `mandatarie`: lista 4 mandatarie con denominazione completa

Se uno di questi campi cambia in `config/brand.json`, tutti i disclaimer generati dalla skill cambiano automaticamente alla prossima invocazione.

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere parametro** `canale` dal chiamante (es. `blog`, `newsletter`, `brochure`, `bio_linkedin_brand`, ecc.)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/brand.json` sez. `identita` per campi correnti
4. **Lookup** formulazione adatta al canale (sez. 3 di questa skill)
5. **Applicare** sostituzioni dinamiche (denominazione, RUI, sede, mandatarie da config)
6. **Aggiungere** moduli condizionali se richiesti dal chiamante (mandatarie inline, Caso Reale, partnership)
7. **Restituire stringa Markdown** al chiamante

Nessuna scrittura file (skill solo lettura `Read+Glob+Grep`). La scrittura Ã¨ del chiamante (skill content-* o MM).

---

## 7. Casi particolari

### Audit di disclaimer in contenuti giÃ  pubblicati
- Invocata via `/adv-disclaimer-rui audit`
- Scansiona `Output_approvati/` per cercare disclaimer presenti e confrontarli con la formulazione corrente
- Restituisce lista di file con disclaimer "vecchi" (es. con vecchia sede o vecchio RUI)
- Suggerisce ri-pubblicazione o aggiornamento (decisione MM)

### Canale non riconosciuto
- Errore: "Canale [X] non riconosciuto. Canali validi: brochure, blog, newsletter, sito, email, descrizione_youtube, bio_linkedin_brand, bio_instagram, bio_facebook, bio_linkedin_daniele, stories_ig, stories_fb, whatsapp_business_utility, post_linkedin_brand, post_linkedin_daniele, post_facebook, caption_instagram, caption_reel."
- Skill non genera output, segnala errore al chiamante

### Modifica della formulazione standard
- Modifica eseguita SOLO in questa skill SKILL.md + `config/brand.json` (mai nelle skill content-*)
- Brand Strategist + Compliance Officer devono validare la nuova formulazione PRIMA della modifica
- Versionamento esplicito in `config/brand.json` (campo `disclaimer_version`: v1.0 â†’ v1.1)

---

## 8. Cosa NON fare mai

- âŒ **Hard-coding del disclaimer** in skill content-* (sempre invocare questa skill)
- âŒ **Modificare la formulazione "al volo"** per un singolo contenuto (formulazioni sono fisse per canale)
- âŒ **Inventare canali** non in mappa (sez. 3)
- âŒ **Omettere riferimento IVASS** (obbligatorio sempre, anche in versioni compatte)
- âŒ **Abbreviazioni RUI** ("RUI A000669271" â†’ no, sempre "RUI Sez. A n. A000669271")
- âŒ **Dimenticare mandatarie** nei canali integrali/completi se il contenuto le cita
- âŒ **Mescolare disclaimer RUI con AI disclosure** (sono skill separate, formulazioni separate)
- âŒ **Tradurre il disclaimer in inglese** o altre lingue senza validazione legale esplicita

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 7 Compliance â€” disclaimer per canale)
2. `config/brand.json` (sez. `identita` â€” fonte di veritÃ  dati societari + mandatarie + disclaimer standard)

---

*SKILL v1.0 â€” advisory-plus:compliance-disclaimer-rui â€” Sessione 4 Plugin Build â€” 2026-05-19*

