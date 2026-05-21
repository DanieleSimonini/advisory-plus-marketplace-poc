---
name: compliance-ai-disclosure
description: Genera la AI disclosure Advisory+ conforme AI Act UE (Regolamento UE 2024/1689, artt. 50 e 52) per contenuti che utilizzano sistemi di intelligenza artificiale generativa. Triggera automaticamente da skill content-* quando viene rilevato uso di HeyGen avatar o altri sistemi AI (esclusi correzioni testuali AI-assisted che non richiedono disclosure). Restituisce due formulazioni: (a) disclosure in caption/descrizione del contenuto (testuale completa) e (b) disclosure on-screen sottile da incorporare nel visual (sigla compatta). Codifica i vincoli definitivi Brand Book v1.2 sez. 14.4 + decisione CEO 2026-05-16: solo avatar generico HeyGen consentito, MAI clone Daniele Simonini o altri soci, MAI doppiaggio AI voce Daniele. Pendenza pre-go-live: validazione formulazione finale con consulente privacy/legale esterno PRIMA del primo video AI pubblicato. Una sola fonte di veritÃ  per tutte le AI disclosure Advisory+.
---
# ðŸ¤– Skill compliance-ai-disclosure â€” Generator AI disclosure AI Act UE

> **Regolamento UE 2024/1689 artt. 50, 52. Avatar generico OK con disclosure. Clone soci VIETATO. Pendenza validazione esterna pre-go-live.**

---

## 1. Quando triggera

- **Automatico**: invocata dalle skill content-reel-script e content-youtube-video quando il brief MM specifica uso di HeyGen avatar
- **Automatico futuro**: invocata da eventuali altre skill content-* che dovessero introdurre AI generativa in produzione (es. doppiaggio AI, sintesi vocale brand)
- **Manuale**: invocata via `/adv-ai-disclosure [tipologia]` per generare formula on-demand
- **Audit**: invocata via `/adv-ai-disclosure audit` per verificare contenuti AI giÃ  pubblicati

Tempo target: **<30 secondi** (lookup e return).

---

## 2. Output finale atteso

**Pacchetto duale** consegnato al chiamante:

```markdown
# AI DISCLOSURE â€” CAPTION/DESCRIZIONE (formulazione testuale completa)
[Formulazione adatta]

# AI DISCLOSURE â€” ON-SCREEN (sigla compatta da incorporare nel visual)
[Sigla]
```

---

## 3. Tipologie AI disclosure per scenario

### Tipologia A â€” Video con HeyGen avatar generico parlante
**Scenario**: explainer YouTube 5-10 min, Reel IG/FB 30-60 sec, case-study con avatar AI parlante professionale che NON imita Daniele nÃ© altri soci reali.

**Caption/descrizione (testuale completa):**
```
Video prodotto dalla redazione Advisory+. L'avatar Ã¨ generato con intelligenza artificiale (HeyGen) a scopo divulgativo. Daniele Simonini e i soci Advisory+ non sono rappresentati in alcun modo dall'avatar mostrato. I contenuti veicolati riflettono la posizione editoriale Advisory+ e sono verificati dalla redazione.
```

**On-screen (sigla compatta):**
```
Avatar AI Â· Advisory+
```
Posizione: corner basso destra Â· presente quando l'avatar HeyGen Ã¨ in scena.

### Tipologia B â€” Video Remotion tipografico/motion graphics
**Scenario**: Reel o YouTube Short interamente animato Remotion senza avatar, eventualmente con voice-over autentica (Daniele o operatore brand reale).

**Caption/descrizione (testuale completa):**
```
Video animation prodotto dalla redazione Advisory+. Animazioni e motion graphics realizzate con tecnologia Remotion. Voce e contenuti veicolati riflettono la posizione editoriale Advisory+.
```

**On-screen (sigla compatta):** NESSUNA (Remotion puro non richiede disclosure on-screen, Ã¨ motion graphic dichiarata)

### Tipologia C â€” Immagine generata con cc-nano-banana (Gemini 2.5 Flash Image)
**Scenario**: cover blog, post social, illustrazione concettuale generata con AI image (no fotorealismo persone).

**Caption/descrizione:**
- **Se l'immagine Ã¨ chiaramente illustrazione/concept (non foto)**: nessuna disclosure obbligatoria (il contenuto Ã¨ palesemente artistico-illustrativo)
- **Se l'immagine simula realtÃ  (es. foto-realismo)**: disclosure obbligatoria:
```
Immagine generata con intelligenza artificiale (Gemini 2.5 Flash Image) a scopo illustrativo. Non rappresenta persone, luoghi o situazioni reali.
```

**On-screen (sigla compatta):**
```
Immagine AI
```
Posizione: corner discreto del visual Â· solo se foto-realistico.

### Tipologia D â€” Testo generato/assistito con LLM (esempi: Claude, GPT, Gemini)
**Scenario**: testo prodotto o significativamente riscritto da LLM.

**Disclosure**: **NESSUNA obbligatoria per scelta editoriale Advisory+** (il testo Ã¨ sempre validato dalla redazione umana â€” MM + Copywriter persone come pattern. Anche se molti contenuti sono assistiti da modelli linguistici per produzione, la responsabilitÃ  editoriale Ã¨ umana e la validazione completa).

Nota: questa scelta editoriale Ã¨ coerente con AI Act UE artt. 50, 52 che richiedono disclosure per "deep fake" e contenuti generati AI "che potrebbero ingannare" â€” un testo informativo professionale verificato dalla redazione non rientra nella casistica obbligatoria.

**Audit pendente**: validare con consulente privacy/legale esterno se servono comunque eccezioni (es. articoli blog interamente AI-generated senza intervento editoriale).

### Tipologia E â€” VIETATO: clone Daniele/soci o doppiaggio AI Daniele
**Scenario**: il contenuto include avatar AI che riproduce fattezze di Daniele Simonini o altri soci, OPPURE doppiaggio AI della voce di Daniele.

**Decisione CEO 2026-05-16 + Brand Book v1.2 sez. 14**: **VIETATO DEFINITIVO**.

La skill, in questo caso:
1. Restituisce errore al chiamante: "ðŸ”´ BLOCCATO: clone fattezze o doppiaggio AI Daniele/soci VIETATO da decisione CEO 2026-05-16 e Brand Book v1.2 sez. 14.4. Reindirizzare il brief a tipologia A (avatar generico HeyGen) o tipologia B (Remotion tipografico) o produzione con voce/immagine autentica Daniele."
2. Notifica MM
3. Non genera nessuna disclosure (il contenuto non deve essere prodotto)

---

## 4. Pendenza pre-go-live â€” validazione esterna

**CRUCIALE**: le formulazioni della tipologia A (caption + on-screen) **DEVONO essere validate da consulente privacy/legale esterno** PRIMA del primo video AI pubblicato (target lancio YouTube giugno-luglio 2026).

Aspetti da validare:
- Sufficienza della formulazione caption rispetto agli obblighi AI Act UE artt. 50, 52
- Sufficienza della sigla on-screen rispetto al requisito di "marcatura riconoscibile" art. 50.2
- Eventuale necessitÃ  di registrazione in apposito registro AI Act UE (per sistemi ad alto rischio)
- Eventuale necessitÃ  di Privacy Impact Assessment (PIA) GDPR per uso di avatar AI

**Skill bloccata in modalitÃ  "draft" finchÃ© validazione esterna non chiusa.**

Quando la validazione Ã¨ chiusa:
- CEO/MM aggiorna `config/brand.json` campo `ai_disclosure_validation_status` da `"pendente"` a `"validata_YYYY-MM-DD_da_[nome_consulente]"`
- Skill cambia modalitÃ  a "production"
- Le skill content-reel-script e content-youtube-video possono pubblicare in automatico (precedentemente in modalitÃ  solo-bozza)

---

## 5. Riferimenti normativi

- **Regolamento UE 2024/1689** (AI Act) â€” entrato in vigore 1Â° agosto 2024
- **Art. 50** â€” Obblighi di trasparenza per fornitori e utilizzatori di sistemi AI generativi (in particolare deep fake e contenuti generati che potrebbero ingannare)
- **Art. 52** â€” Marcatura riconoscibile dei contenuti generati artificialmente (filigrana, sigla, watermarking)
- **GDPR (Reg. UE 2016/679)** â€” applicabile se l'avatar AI riproduce caratteristiche di persone fisiche identificabili (rilevante per il vincolo "no clone Daniele")

Riferimenti tenuti aggiornati in `config/brand.json` sez. `ai_act_ue`.

---

## 6. Logica di esecuzione â€” passo-passo

1. **Ricevere parametro** `tipologia` dal chiamante (A, B, C, D, E) + eventuali dettagli (es. tipo di voice-over, foto-realismo immagine)
2. **Eseguire kickoff** per contesto workspace
3. **Verificare** stato validazione esterna in `config/brand.json` sez. `ai_disclosure_validation_status`
4. **Se tipologia E** (clone/doppiaggio Daniele): errore bloccante, return
5. **Se validazione "pendente"** e tipologia A: aggiungere avviso al chiamante "AI disclosure in modalitÃ  DRAFT â€” pubblicazione bloccata finchÃ© validazione esterna non chiusa"
6. **Lookup** formulazione testuale + sigla on-screen per tipologia
7. **Applicare** eventuali dettagli forniti dal chiamante
8. **Restituire pacchetto duale** al chiamante

Nessuna scrittura file (skill solo lettura). La scrittura Ã¨ del chiamante.

---

## 7. Casi particolari

### Audit disclosure di contenuti AI giÃ  pubblicati
- Invocata via `/adv-ai-disclosure audit`
- Scansiona `Output_approvati/` e `/05_Calendario_editoriale/Log_pubblicati/` per identificare contenuti AI
- Verifica che le disclosure siano allineate alla formulazione corrente validata
- Restituisce lista discrepanze + suggerimenti aggiornamento

### Modifica delle formulazioni standard
- Modifica eseguita SOLO in questa skill + `config/brand.json` campo `ai_disclosure_version`
- Brand Strategist + Compliance Officer + (se possibile) consulente esterno devono validare la nuova formulazione
- Versionamento esplicito + propagazione automatica a tutte le skill che invocano questa

### Nuova tipologia AI generativa introdotta in futuro (es. video generative full Sora-like)
- Aggiungere nuova tipologia F, G, ecc. con sua formulazione
- Validazione esterna obbligatoria
- Update Brand Book v1.2 sez. 14 con nuova policy

### Multilingue (eventuale espansione futura)
- Formulazioni attuali sono solo italiano
- Eventuale espansione multilingue richiede validazione legale per ciascuna lingua (legislazione di destinazione)

---

## 8. Cosa NON fare mai

- âŒ **Generare disclosure per tipologia E** (clone/doppiaggio Daniele â€” vietato definitivo, errore bloccante)
- âŒ **Pubblicare con tipologia A** senza validazione esterna chiusa (modalitÃ  draft)
- âŒ **Omettere sigla on-screen** quando tipologia A richiesta (AI Act UE art. 52 marcatura riconoscibile)
- âŒ **Omettere disclosure caption** quando tipologia A o C foto-realistica
- âŒ **Modificare formulazione "al volo"** per singolo contenuto (formulazioni sono fisse e validate)
- âŒ **Inventare tipologie** non in mappa (sez. 3)
- âŒ **Tradurre disclosure senza validazione legale** della lingua di destinazione
- âŒ **Confondere AI disclosure con disclaimer RUI** (sono skill separate, formulazioni separate, posizioni diverse)
- âŒ **Posizionare sigla on-screen** in modo poco visibile o leggibile (deve essere riconoscibile, AI Act UE art. 52)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di generare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 14 AI Act UE + ETICA AI no clone Daniele Â· sez. 7 Compliance)
2. `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (sez. `ai_act_ue` Â· sez. `ai_disclosure_validation_status` Â· sez. `ai_disclosure_version`)

---

*SKILL v1.0 â€” advisory-plus:compliance-ai-disclosure â€” Sessione 4 Plugin Build â€” 2026-05-19*

