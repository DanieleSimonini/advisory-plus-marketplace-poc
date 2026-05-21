---
name: strategia-week-mon
description: Apertura settimanale automatizzata Advisory+ ogni lunedÃ¬ alle 06:00 via scheduled task. Tre funzioni essenziali in sequenza: (i) Inbox check â€” legge la inbox marketing@advisoryplus.it per intercettare eventuali reply weekend del CEO al Friday Email (STOP #N Â· MODIFICA #N Â· RINVIA #N a W[NN+X] Â· subject speciali STOP TUTTO/MODALITÃ€ FERIE/MODALITÃ€ CRISI) PRIMA della pubblicazione delle 09:00. (ii) Status digest mattutino â€” produce digest sintetico in Markdown e WhatsApp/email al CEO con cosa pubblica oggi su quali canali, eventuali blocchi, stato sistemi. (iii) Health check execution â€” verifica che Buffer queue Â· LinkedIn MCP Â· Meta MCP Â· WordPress MCP Â· Brevo SMTP siano online e raggiungibili; segnala anomalie a MM e CEO. Se trova reply pending del CEO o sistema down, blocca pubblicazione interessata e notifica. Triggera lun 06:00 auto + manualmente via /adv-monday-open.
---
# ðŸŒ… Skill week-mon â€” Monday Opening Routine Advisory+

> **L'alba operativa della settimana. Intercetta reply weekend, valida il piano, controlla i sistemi PRIMA della pubblicazione delle 09:00.**

---

## 1. Quando triggera

- **Automatico**: ogni **lunedÃ¬ alle 06:00** via scheduled task
- **Manuale**: invocata dal MM o CEO con `/adv-monday-open` (per ri-eseguire dopo intervento manuale, o per anticipare la routine)
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false` â†’ skip routine, sistema in pausa totale

Tempo target di esecuzione: **<5 minuti** (deve chiudere ben prima delle 09:00 per dare margine).

---

## 2. Output finale atteso

**Una notifica al CEO** (email + WhatsApp se configurato), formato sintetico:

```
â˜€ï¸ Advisory+ Â· Monday Opening Â· W[NN] Â· [data]

Reply CEO weekend: [nessuna / N applicate / N pending blocco]
Pubblicazione oggi: [N] contenuti pianificati su [canali]
Sistemi: [tutti OK / X anomalia: descrizione]
Block list: [contenuti bloccati per reply CEO o sistema down]
Next sync: [eventuale azione richiesta CEO]
```

**Una entry di log** in `/05_Calendario_editoriale/Monday_opens/[YYYY-MM-DD]_open.md` con dettaglio per riferimento futuro.

---

## 3. Tre funzioni in sequenza

### Funzione (i) â€” Inbox check (prioritÃ  1)

**Cosa fa**: legge la inbox `marketing@advisoryplus.it` (IMAP, configurato in `config/email.env`) dalla **chiusura del Friday Email (ven 18:00)** fino a **ora corrente (lun 06:00)**.

**Cosa cerca**:

1. **Subject speciali** (azione globale):
   - `STOP TUTTO` â†’ kill switch immediato â†’ set `config/AUTOMAZIONE_ATTIVA = false` â†’ notifica al MM
   - `MODALITÃ€ FERIE [data fine]` â†’ attiva modalitÃ  ferie in `config/state.json` â†’ fino a data fine, solo always-on minimi
   - `MODALITÃ€ CRISI` â†’ attiva modalitÃ  crisi â†’ blocco pubblicazione, MM in presidio manuale

2. **Reply al Friday Email** (azione per-content):
   - Pattern: `STOP #N` (N = indice contenuto nella sezione B del Friday Email)
   - Pattern: `MODIFICA #N: [istruzione]` (applica istruzione al contenuto N)
   - Pattern: `RINVIA #N a W[NN+X]` (sposta a settimana successiva o specificata)
   - Pattern: `OK #N` / `MODIFICA #N` / `RIFIUTA #N` per big bets sez. C

3. **Subject pattern emergency** (azione MM):
   - `URGENTE` â†’ notifica MM via WhatsApp/email per intervento manuale
   - `SPUNTO` â†’ aggiunge a `Spunti_CEO.md` per trattamento prossimo ciclo

**Cosa NON fa**:
- Non interpreta email libere senza i subject/pattern attesi (le inoltra al MM)
- Non risponde direttamente al CEO (l'eventuale conferma arriva nel digest sez. 2)

**Se zero reply** â†’ procedi con il piano B del Friday Email applicato in toto (silent approval window scaduta lun 06:00).

### Funzione (ii) â€” Status digest mattutino

Produce il digest descritto in sez. 2. Componenti:

- **Reply applicate**: lista delle reply CEO weekend e cosa ha modificato sul piano
- **Pubblicazione di oggi**: contatore + dettaglio per canale (LinkedIn brand Â· LinkedIn Daniele semi-manuale Â· Instagram Â· Facebook Â· YouTube se schedulato Â· Blog se pubblicazione blog oggi Â· Newsletter se invio settimanale oggi)
- **Block list**: contenuti bloccati per reply CEO o sistema down (con motivo)
- **Next sync**: eventuali azioni richieste al CEO (firma post LinkedIn Daniele entro 09:00, OK big bet residuo, etc.)

### Funzione (iii) â€” Health check execution

Verifica che i sistemi necessari alla pubblicazione siano online e raggiungibili.

**Checklist**:

| Sistema | Check | Se KO |
|---|---|---|
| Brevo SMTP | API ping (libreria Brevo shell) | Notifica CEO + MM, blocca email |
| LinkedIn MCP (brand) | health check tool MCP | Notifica + blocca post LinkedIn brand |
| LinkedIn (Daniele personale, semi-manuale) | n/a â€” preparazione preview only | n/a |
| Meta MCP (FB + IG) | health check | Notifica + blocca post FB/IG |
| WordPress.com MCP | health check | Notifica + blocca pubblicazione blog |
| Buffer/Publer (se in uso come ponte) | API ping | Notifica + fallback su MCP nativo |
| Google Calendar MCP | health check | Notifica, eventi calendario potrebbero non sincronizzare |
| HeyGen MCP | health check (solo se schedulato video AI) | Skip video, notifica |
| Supermetrics MCP | health check (solo per Friday Email next) | Skip KPI nel prossimo Friday |
| Cloudinary MCP | health check (solo se asset multimedia in pipeline) | Skip trasformazioni asset |
| cc-nano-banana CLI | binary ping | Notifica se rotto, fallback Canva |

**Soglia critica**: se >50% dei sistemi necessari alla pubblicazione di oggi sono KO â†’ **blocco totale pubblicazione + notifica urgente CEO**.

---

## 4. Logica di esecuzione â€” passo-passo

1. **Eseguire kickoff** (skill `advisory-plus:kickoff`) per caricare contesto workspace
2. **Verificare** `config/AUTOMAZIONE_ATTIVA` (se false â†’ skip + notifica)
3. **Verificare** `config/state.json` per modalitÃ  ferie/crisi attive
4. **Eseguire Funzione (i)** Inbox check via Bash + libreria IMAP
5. **Applicare** reply CEO al piano della settimana (file `/05_Calendario_editoriale/[YYYY-MM]_*.md`)
6. **Eseguire Funzione (iii)** Health check sistemi
7. **Comporre Funzione (ii)** Status digest
8. **Inviare** digest via email a CEO (Brevo SMTP) + WhatsApp (Twilio fase 2)
9. **Log** in `/05_Calendario_editoriale/Monday_opens/[YYYY-MM-DD]_open.md`
10. **Schedulare** pubblicazione di oggi (ogni contenuto al suo orario) â€” handoff a skill `adv-publish-*` (Sessione 7)

---

## 5. Casi particolari

### Reply CEO ambigua o non parseable
- MM legge come fallback umano
- Notifica al CEO: "Reply non parseata: [oggetto]. Confermi STOP/MODIFICA/RINVIA? Pubblicazione interessata bloccata in attesa."

### Inbox irraggiungibile (IMAP down)
- Notifica urgente CEO + MM
- **Default conservativo**: blocca pubblicazione fino a recovery (meglio non pubblicare che pubblicare un contenuto vetoato di cui non sappiamo il veto)

### Sistema critico KO (es. LinkedIn MCP)
- Blocca solo i contenuti del sistema KO
- Reschedula in coda quando il sistema torna online
- Notifica CEO con stima recovery

### Big bet pending senza reply CEO entro lun 06:00
- **Default conservativo**: rinvia il big bet a settimana successiva
- Notifica: "Big bet #N senza tua reply entro silent approval window. Rinviato a W[NN+1]. Conferma o rivedi."

### ModalitÃ  Ferie attiva
- Skip Funzione (i) â€” non si applicano reply ad un piano in pausa
- Funzione (ii) si limita a "ModalitÃ  Ferie attiva fino al [data]. Always-on minimo eseguito (1 post P1 ed. settimanale)."
- Funzione (iii) check minimo (solo SMTP e blog)

---

## 6. Cosa NON fare mai

- âŒ **Eseguire la pubblicazione delle 09:00 senza aver completato Funzione (i)** (rischio: pubblicare contenuto vetoato dal CEO durante il weekend)
- âŒ **Marcare un sistema KO come "ok" per sicurezza** â€” meglio bloccare e notificare
- âŒ **Inviare digest dopo le 07:00** senza notifica preventiva (CEO ha bisogno di leggere prima dell'eventuale finestra di intervento manuale)
- âŒ **Auto-rispondere al CEO** â€” la skill informa, non dialoga
- âŒ **Saltare il log** in `/Monday_opens/` (Ã¨ la memoria operativa)
- âŒ **Bypassare AUTOMAZIONE_ATTIVA = false** in nome dell'efficienza
- âŒ **Interpretare creativamente** reply CEO ambigue â€” chiedere via notifica

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire, leggi in ordine:

1. `/00_README.md`
2. `/00_Brand_Book_v1.2.md` (sez. 13 MM Decision Authority)
3. `/01_Team/00_Marketing_Manager.md`
4. `/05_Calendario_editoriale/[YYYY-MM]_*.md` (piano in corso)
5. `/05_Calendario_editoriale/Friday_emails/[ultimo].md` (per riferimenti #N reply)
6. `config/AUTOMAZIONE_ATTIVA` Â· `config/state.json` Â· `config/email.env` Â· `config/pillars-of-month.json`

---

*SKILL v1.0 â€” advisory-plus:week-mon â€” Sessione 2 Plugin Build â€” 2026-05-17*

