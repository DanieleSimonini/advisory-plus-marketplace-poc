---
name: compliance-mandatarie-check
description: Validator denominazione corretta delle 4 compagnie mandatarie Advisory+ (Brand Book v1.2 sez. 7). Triggera automaticamente da skill content-* e da compliance-gate-doppio prima di output finale. Scansiona il testo del contenuto + il visual brief per individuare riferimenti a mandatarie e verifica che la denominazione sia corretta e completa: Generali Italia â€“ Cattolica Assicurazioni (mai solo "Generali" o solo "Cattolica") Â· DAS Difesa Legale Â· UCA Tutela Legale e Peritale Â· Europ Assistance. Verifica inoltre che i loghi mandatarie siano usati ESCLUSIVAMENTE in area disclosure (brochure footer, descrizione YouTube, sito) e MAI in cover/corpo del contenuto. Restituisce semaforo ðŸŸ¢/ðŸŸ¡/ðŸ”´ + lista violazioni + correzioni proposte. Triggera anche manualmente via /adv-mandatarie-check [file] per validare bozza in corso.
---
# âœ… Skill compliance-mandatarie-check â€” Validator denominazione mandatarie

> **4 mandatarie. 4 denominazioni esatte. Loghi solo in disclosure. Brand Book v1.2 sez. 7 vincolo IVASS hard.**

---

## 1. Quando triggera

- **Automatico**: invocata dalle skill content-* (in particolare content-brochure, content-newsletter, content-blog-article, content-youtube-video) prima della consegna al MM
- **Automatico aggregato**: invocata da `compliance-gate-doppio` come sotto-verifica del gate 1
- **Manuale**: invocata via `/adv-mandatarie-check [file]` per validare bozza in corso

Tempo target: **<30 secondi** (scansione testuale + lookup).

---

## 2. Output finale atteso

**Verdetto** consegnato al chiamante:

```markdown
# MANDATARIE CHECK
Esito: [ðŸŸ¢ NESSUNA VIOLAZIONE | ðŸŸ¡ VIOLAZIONI MINORI (riformulazione proposta) | ðŸ”´ VIOLAZIONI GRAVI (blocco)]

## Mandatarie rilevate nel contenuto
[Lista mandatarie effettivamente citate Â· forma usata]

## Violazioni denominazione (se ðŸŸ¡/ðŸ”´)
[Lista violazioni Â· forma sbagliata trovata Â· forma corretta proposta Â· riga/posizione nel file]

## Violazioni uso loghi (se ðŸŸ¡/ðŸ”´)
[Lista violazioni Â· posizione logo nel visual brief Â· regola applicabile]

## Riformulazione proposta
[Testo corretto con sostituzioni applicate Â· ready-to-merge per il chiamante]
```

---

## 3. Le 4 mandatarie â€” denominazioni esatte

### ðŸ”µ Generali Italia â€“ Cattolica Assicurazioni
- **Corretto**: `Generali Italia â€“ Cattolica Assicurazioni`
- **Sbagliato**: `Generali` da solo Â· `Cattolica` da solo Â· `Generali Italia` da solo Â· `Cattolica Assicurazioni` da solo Â· `Generali-Cattolica` (trattino normale) Â· `Generali e Cattolica` Â· `Gruppo Generali`
- **Trattino corretto**: en-dash `â€“` (U+2013), NON trattino normale `-` (U+002D)
- **Aliasing accettati** (in contesti di compagine dove serve sintesi): `Generali Italia â€“ Cattolica` (forma corta accettabile in tabelle, mai in testi pubblicitari estesi)

### ðŸŸ¢ DAS Difesa Legale
- **Corretto**: `DAS Difesa Legale`
- **Sbagliato**: `DAS` da solo Â· `DAS Tutela Legale` (confusione con UCA) Â· `D.A.S.` con puntini Â· `Difesa Legale DAS`
- **Aliasing accettati**: nessuno (sempre denominazione completa)

### ðŸŸ¡ UCA Tutela Legale e Peritale
- **Corretto**: `UCA Tutela Legale e Peritale`
- **Sbagliato**: `UCA` da solo Â· `UCA Tutela Legale` (manca "e Peritale") Â· `U.C.A.` con puntini Â· `Tutela Legale UCA`
- **Aliasing accettati**: nessuno (sempre denominazione completa)

### ðŸŸ  Europ Assistance
- **Corretto**: `Europ Assistance`
- **Sbagliato**: `Europ` da solo Â· `Europe Assistance` (con "e" finale, errore comune) Â· `Europe Assist` Â· `Europ Assistance Italia`
- **Aliasing accettati**: nessuno (sempre denominazione completa)

---

## 4. Vincolo IVASS uso loghi mandatarie

**Brand Book v1.2 sez. 7 vincolo hard**: i loghi delle 4 mandatarie devono essere usati **ESCLUSIVAMENTE nell'area disclosure** dei materiali corporate:
- âœ… **Permesso**: footer brochure, footer sito web pagina contatti, descrizione YouTube area "mandati", footer newsletter mensile sezione compagine
- ðŸ”´ **Vietato**: cover brochure, cover blog, hero banner newsletter, thumbnail YouTube, visual post LinkedIn/Facebook/Instagram, visual Reel, visual Stories, copertina sito web, materiali co-marketing (devono essere autorizzati esplicitamente dalla mandataria)

Le mandatarie tipicamente vincolano l'uso del proprio logo a finalitÃ  di disclosure dell'intermediario, **mai per veicolare prodotti specifici** o promuovere la mandataria stessa attraverso Advisory+.

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere file** dal chiamante (Markdown completo + brief visual)
2. **Eseguire kickoff** per contesto workspace
3. **Leggere** `config/brand.json` sez. `mandatarie` per denominazioni correnti (fonte di veritÃ )
4. **Scansione testuale** del contenuto (Grep):
   - Cerca occorrenze "Generali", "Cattolica", "DAS", "UCA", "Europ"
   - Per ogni occorrenza, verifica forma usata vs forma corretta
5. **Scansione visual brief** (se presente):
   - Verifica posizione di eventuali loghi mandatarie nel brief
   - Se logo in cover/corpo (non in disclosure) â†’ violazione ðŸ”´
6. **Aggregare** verdetto:
   - Nessuna violazione â†’ ðŸŸ¢
   - Solo violazioni minori (es. forma corta accettabile in contesto sbagliato) â†’ ðŸŸ¡ con riformulazione
   - Violazione denominazione grave (es. "Generali" da solo in caption pubblicitaria) o logo fuori-disclosure â†’ ðŸ”´
7. **Produrre riformulazione** automatica (se applicabile) con sostituzione di stringhe
8. **Restituire verdetto** + lista violazioni + riformulazione proposta al chiamante

Nessuna scrittura del file originale (skill solo lettura). Il chiamante applica le correzioni.

---

## 6. Casi particolari

### Contenuto editoriale generico senza riferimento mandatarie
- Skill restituisce ðŸŸ¢ + "Nessuna mandataria citata. Check non applicabile."
- Tempo di esecuzione minimo

### Caso Reale con coperture generiche ("polizza vita TCM", "polizza tutela legale")
- Verifica che il contenuto NON menzioni prodotti specifici delle mandatarie (es. "Generali Vita Sereno" â†’ forma di prodotto specifico, attenzione Compliance)
- Se solo coperture generiche citate â†’ ðŸŸ¢
- Se prodotti specifici citati â†’ ðŸŸ¡ + richiesta context (Ã¨ autorizzato? c'Ã¨ disclaimer set informativo?)

### Brochure linea Famiglia con loghi 4 mandatarie in footer
- âœ… Permesso (Ã¨ l'uso elettivo dei loghi mandatarie)
- ðŸŸ¢ se denominazione corretta nel testo

### Post LinkedIn con logo Generali nel visual
- ðŸ”´ violazione grave (logo mandataria fuori disclosure)
- Riformulazione proposta: rimuovere logo dal visual, sostituire con illustrazione/grafica brand Advisory+
- Mai pubblicare con logo mandataria su visual social

### Post LinkedIn brand che cita "Generali" da solo
- ðŸŸ¡ violazione minore
- Riformulazione proposta: sostituire con "Generali Italia â€“ Cattolica Assicurazioni"
- Pubblicazione consentita dopo correzione

### Articolo blog Analisi che cita normativa con riferimento a una mandataria
- ðŸŸ¢ ok se denominazione corretta
- ðŸŸ¡ se denominazione abbreviata
- Apparato citazionale Analisi richiede precisione, quindi denominazione completa obbligatoria

### Brochure co-marketing con partner non-mandatario
- Logo partner in cover o footer Ã¨ autorizzato dalla partnership
- Loghi 4 mandatarie restano vincolati a disclosure footer (regola IVASS invariata)
- Compliance gate raddoppiato per brochure co-marketing

---

## 7. Cosa NON fare mai

- âŒ **Auto-correggere il file originale** (skill solo lettura â€” correzione Ã¨ del chiamante)
- âŒ **Accettare aliasing** non in lista (sez. 3) anche se sembrano "ovvi"
- âŒ **Ignorare il trattino en-dash `â€“`** in "Generali Italia â€“ Cattolica Assicurazioni" (Ã¨ il formato corretto, non il trattino normale)
- âŒ **Confondere DAS Difesa Legale con UCA Tutela Legale e Peritale** (sono mandatarie distinte con denominazioni diverse)
- âŒ **Permettere logo mandataria fuori disclosure** (vincolo IVASS hard)
- âŒ **Saltare scansione visual brief** (i loghi sono il rischio principale, piÃ¹ della denominazione testuale)
- âŒ **Citare prodotti specifici della mandataria** senza disclaimer set informativo (rischio Compliance)
- âŒ **Modificare denominazione corrente** delle mandatarie nel `config/brand.json` senza decisione esplicita CEO + verifica con la mandataria stessa

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di validare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 7 Compliance â€” denominazione mandatarie + vincolo loghi)
2. `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (sez. `mandatarie` â€” fonte di veritÃ  denominazioni)

---

*SKILL v1.0 â€” advisory-plus:compliance-mandatarie-check â€” Sessione 4 Plugin Build â€” 2026-05-19*

