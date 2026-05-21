---
name: compliance-gate-doppio
description: Esegue il doppio gate hard pre-pubblicazione Advisory+ (Brand Book v1.2 sez. 13 â€” MM Decision Authority Framework) â€” gate 1 Compliance Officer (semaforo ðŸŸ¢/ðŸŸ¡/ðŸ”´ IVASS/RUI/AI Act UE) + gate 2 Brand Strategist (coerenza con Brand Book v1.2). Triggera automaticamente prima di ogni pubblicazione automatica sui canali brand (LinkedIn Pagina, Facebook, Instagram, YouTube, Blog WordPress, Newsletter Brevo) e prima della consegna semi-manuale al CEO per LinkedIn personale Daniele. Il gate Ã¨ "hard": ðŸ”´ di entrambi i gate = blocco assoluto + email alert al CEO entro 1h. ðŸŸ¡ = riformulazione obbligatoria + ri-check (1 iterazione max prima di escalation MM). ðŸŸ¢ = pubblicazione consentita. Invoca le skill persona `advisory-plus:compliance-officer` (Read+Grep only, solo lettura) e `advisory-plus:brand-strategist` (Read+Glob+Grep only) via Task tool in parallelo per ottimizzare tempo. Aggrega gli esiti, decide go/no-go, logga in /05_Calendario_editoriale/Log_pubblicati/compliance_gate_[YYYY-MM]_log.md. Triggera anche fuori-pubblicazione su richiesta MM per validare bozza in corso di lavorazione.
---
# ðŸ”’ Skill compliance-gate-doppio â€” Doppio gate hard Advisory+

> **Compliance Officer + Brand Strategist in parallelo. ðŸ”´ di uno dei due = blocco + alert CEO entro 1h. Brand Book v1.2 sez. 13.**

---

## 1. Quando triggera

- **Automatico**: invocato dal MM o da skill di canale (`content-*`) come step obbligatorio pre-consegna al MM
- **Automatico pre-pubblicazione**: invocato 30 minuti prima dell'orario di pubblicazione automatica (gate 2 ridondante per intercettare drift tra produzione e pubblicazione, decisione CEO 2026-05-16)
- **Manuale**: invocato dal MM via `/adv-compliance` per validare una bozza in corso
- **Bloccato** se `config/AUTOMAZIONE_ATTIVA = false` (kill switch globale)

Tempo target di esecuzione: **2-3 minuti** (i due gate girano in parallelo).

---

## 2. Output finale atteso

**Verdetto consolidato** consegnato al chiamante (MM o skill di canale):

```markdown
---
gate_doppio_id: gate_[YYYY-MM-DD-HHMM]_[hash]
contenuto_oggetto: [riferimento file]
canale_target: [es. linkedin_pagina_brand]
data_pubblicazione: [YYYY-MM-DD HH:MM]
---

# VERDETTO CONSOLIDATO
[ðŸŸ¢ PUBBLICABILE | ðŸŸ¡ RIFORMULAZIONE | ðŸ”´ BLOCCATO]

## Gate 1 â€” Compliance Officer
Esito: [ðŸŸ¢/ðŸŸ¡/ðŸ”´]
[Eventuali note specifiche e riformulazioni proposte]

## Gate 2 â€” Brand Strategist
Esito: [ðŸŸ¢/ðŸŸ¡/ðŸ”´]
[Eventuali note specifiche e riformulazioni proposte]

# AZIONE RICHIESTA
[Pubblicazione consentita / Riformulazione obbligatoria con istruzioni / BLOCCO totale + email alert CEO]

# LOG ENTRY
[Stringa formattata per /05_Calendario_editoriale/Log_pubblicati/compliance_gate_[YYYY-MM]_log.md]
```

---

## 3. Logica del doppio gate

### Gate 1 â€” Compliance Officer (semaforo IVASS/RUI/AI Act UE)
Verifica:
- Claim e promesse (no rendimenti garantiti, no claim assoluti)
- Denominazione corretta mandatarie (Generali Italia â€“ Cattolica Assicurazioni Â· DAS Difesa Legale Â· UCA Tutela Legale e Peritale Â· Europ Assistance)
- Disclaimer RUI presente dove canale lo richiede (blog, newsletter, brochure, descrizione YouTube)
- Loghi mandatarie solo in disclosure footer (mai cover/corpo)
- Citazione prezzi specifici di prodotto solo con contesto
- AI disclosure presente se HeyGen avatar usato (AI Act UE artt. 50, 52)
- No clone Daniele Simonini o altri soci con AI
- No doppiaggio AI voce Daniele
- Caso Reale ha disclaimer "Caso reale, nomi di fantasia"
- Analisi ha apparato citazionale corretto (fonte+anno)
- Riferimenti normativi puntuali (n. sentenza, articolo decreto)
- Nessun contenuto denigratorio verso concorrenti
- Privacy: nessuna foto/dato persona identificabile senza consenso

### Gate 2 â€” Brand Strategist (coerenza Brand Book v1.2)
Verifica:
- Voce editoriale coerente con pillar e canale (mapping Brand Book v1.2 sez. 4 + sez. 6)
- Tono coerente con posizionamento "Consulenza assicurativa. Sul serio."
- Tagline "Consulenza assicurativa. Sul serio." non alterata o sostituita
- 5 pilastri di differenziazione (Brand Book v1.2 sez. 2) almeno uno agganciato
- Pillar map 12 â€” contenuto agganciato a pillar esistente, non inventato
- Posizionamento nazionale rispettato (zero riferimenti territoriali)
- Ratio 80/20 firma rispettato (Daniele â‰¤70% firme cumulate mese)
- Tetto Badvisor 20% mese rispettato (se voce Ã¨ Badvisor)
- Compagine usata correttamente (ordine alfabetico nei materiali identitari, mandate solo se autorizzate)
- Cover Blog System usato correttamente per blog (Brand Book v1.2 sez. 8.1)
- Design System palette/font corretto (Brand Book v1.2 sez. 8)
- Voci editoriali non sostituite o reinventate

### Semaforo aggregato â€” logica di consolidamento

| Gate 1 | Gate 2 | Verdetto consolidato | Azione |
|---|---|---|---|
| ðŸŸ¢ | ðŸŸ¢ | **ðŸŸ¢ PUBBLICABILE** | Pubblicazione consentita |
| ðŸŸ¢ | ðŸŸ¡ | ðŸŸ¡ RIFORMULAZIONE | Brand Strategist propone riformulazione, ri-check |
| ðŸŸ¡ | ðŸŸ¢ | ðŸŸ¡ RIFORMULAZIONE | Compliance Officer propone riformulazione, ri-check |
| ðŸŸ¡ | ðŸŸ¡ | ðŸŸ¡ RIFORMULAZIONE | Entrambi propongono riformulazioni, ri-check con max 1 iterazione |
| ðŸ”´ | qualsiasi | **ðŸ”´ BLOCCO** | Blocco assoluto + email alert CEO entro 1h |
| qualsiasi | ðŸ”´ | **ðŸ”´ BLOCCO** | Blocco assoluto + email alert CEO entro 1h |

### Limite iterazioni
- **Max 1 iterazione di riformulazione** consentita
- Se dopo la riformulazione il verdetto resta ðŸŸ¡ o ðŸ”´ â†’ **escalation al MM** (non chiusa autonomamente)
- MM decide: ulteriore riformulazione manuale o rinvio del contenuto a settimana successiva

---

## 4. Email alert CEO su BLOCCO ðŸ”´ (entro 1h)

Quando il verdetto Ã¨ ðŸ”´, la skill:
1. Blocca pubblicazione del contenuto interessato
2. **Notifica MM immediato**
3. **Compone email alert CEO** entro 1h via Brevo SMTP (libreria shell):

```
Subject: ðŸ”´ Advisory+ ALERT Compliance â€” [contenuto] BLOCCATO

Daniele,
Compliance gate ha bloccato la pubblicazione di:

Contenuto: [titolo + canale]
Data pubblicazione pianificata: [YYYY-MM-DD HH:MM]
Pillar: P[N] [Nome]
Voce: [voce editoriale]

Gate 1 Compliance Officer: ðŸ”´
Motivo: [sintesi 3-5 righe + violazione specifica]

Gate 2 Brand Strategist: [ðŸŸ¢/ðŸŸ¡/ðŸ”´]
Motivo: [sintesi 3-5 righe + violazione specifica]

Azione MM consigliata: [opzione A: rinvio Â· opzione B: riformulazione sostanziale Â· opzione C: cancellazione]

Risposta richiesta entro 24h via email o STOP/MODIFICA/RIFIUTA #N.

Marketing Manager Advisory+ Plugin
```

4. Logga il ðŸ”´ nel `compliance_gate_[YYYY-MM]_log.md` con dettaglio violazione

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere contenuto** da validare (file Markdown completo con frontmatter, caption, hashtag, visual brief)
2. **Eseguire kickoff** per contesto workspace
3. **Verificare** `config/AUTOMAZIONE_ATTIVA` (se false â†’ skip + notifica MM)
4. **Invocare in parallelo** entrambi i gate via Task tool:
   ```
   Task(
     subagent_type: "advisory-plus:compliance-officer",
     prompt: "Gate 1 doppio gate hard: verifica contenuto [riferimento]. Restituisci semaforo ðŸŸ¢/ðŸŸ¡/ðŸ”´ + eventuali note di riformulazione."
   )
   Task(
     subagent_type: "advisory-plus:brand-strategist",
     prompt: "Gate 2 doppio gate hard: verifica coerenza contenuto [riferimento] con Brand Book v1.2 (pillar, voce, posizionamento, ratio 80/20, tetto Badvisor 20%, Cover Blog System). Restituisci semaforo ðŸŸ¢/ðŸŸ¡/ðŸ”´ + eventuali note."
   )
   ```
5. **Ricevere** entrambi i semafori
6. **Aggregare** secondo logica sez. 3 (tabella consolidamento)
7. **Se ðŸŸ¢/ðŸŸ¢**: consegnare verdetto PUBBLICABILE al chiamante
8. **Se ðŸŸ¡**: rimandare al chiamante con riformulazioni proposte, attendere ri-check (max 1 iterazione)
9. **Se ðŸ”´**: blocco + email alert CEO entro 1h + log
10. **Loggare** sempre in `/05_Calendario_editoriale/Log_pubblicati/compliance_gate_[YYYY-MM]_log.md` (formato: timestamp + contenuto + canale + verdetto + motivo se ðŸŸ¡/ðŸ”´ + azione)

---

## 6. Casi particolari

### Gate 2 pre-pubblicazione (30 min prima orario auto)
- Re-invocato 30 min prima dell'orario di pubblicazione automatica
- Verifica drift: il contenuto Ã¨ ancora coerente rispetto a eventi nuovi (es. nessuna crisi mandataria scoppiata nel frattempo)?
- Se trova nuove anomalie â†’ blocca pubblicazione + email alert CEO + log

### ModalitÃ  Crisi attiva
- TUTTI i contenuti automatici sono bloccati di default
- Gate doppio NON viene neanche invocato durante crisi
- Solo MM/CEO possono autorizzare contenuti durante crisi (gestione manuale fuori-skill)

### Contenuto firmato Daniele (LinkedIn personale)
- Gate doppio comunque eseguito
- ðŸŸ¡/ðŸ”´ â†’ MM blocca consegna a Daniele
- ðŸŸ¢ â†’ MM consegna a Daniele per rilettura e click semi-manuale
- Daniele puÃ² comunque decidere ulteriori modifiche (autoritÃ  ultima sulla sua voce)

### Big bet in pubblicazione (decisione CEO esplicita richiesta)
- Gate doppio eseguito DOPO l'OK CEO ricevuto via reply Friday Email
- ðŸ”´ dopo OK CEO = comunque blocco + secondo alert CEO ("Hai approvato ma compliance ha bloccato â€” riformula o ritira?")

### Riformulazione automatica accettata (gate 1 propone modifica e gate 2 conferma)
- Applicata in automatico
- Loggata come "riformulazione automatica applicata"
- Ri-check dopo applicazione (verifica che la riformulazione non abbia introdotto altri problemi)

---

## 7. Cosa NON fare mai

- âŒ **Bypassare gate 1 per fretta** (anche su contenuti "innocui")
- âŒ **Bypassare gate 2 per fretta** (la coerenza brand Ã¨ importante quanto la compliance)
- âŒ **Pubblicare con ðŸŸ¡ non risolto** (sempre riformulazione)
- âŒ **Pubblicare con ðŸ”´** sotto nessuna circostanza (no override)
- âŒ **Omettere email alert CEO** su ðŸ”´ (entro 1h obbligatorio)
- âŒ **Omettere log** in `compliance_gate_[YYYY-MM]_log.md`
- âŒ **Iterazioni infinite** di riformulazione (max 1, poi escalation MM)
- âŒ **Validare il proprio output del gate** (i due gate sono indipendenti e paralleli)
- âŒ **Eseguire gate sequenzialmente invece che in parallelo** (perdita tempo, non aggiunge valore)
- âŒ **Auto-modificare il contenuto** senza passare per il chiamante (la modifica spetta sempre al chiamante che applica le riformulazioni proposte)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 7 Compliance Â· sez. 13 MM Decision Authority Framework Â· sez. 14 AI Act UE)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/01_Brand_Strategist.md` Â· `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (mandatarie, disclaimer, denominazioni, tetto Badvisor)
4. `config/AUTOMAZIONE_ATTIVA` Â· `config/state.json`
5. Il contenuto oggetto di validazione (file Markdown completo)

---

*SKILL v1.0 â€” advisory-plus:compliance-gate-doppio â€” Sessione 4 Plugin Build â€” 2026-05-19*

