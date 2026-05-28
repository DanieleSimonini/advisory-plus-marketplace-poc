---
name: strategia-week-mon
description: Apertura settimanale automatizzata Advisory+ ogni lunedì alle 06:00 via scheduled task. Tre funzioni essenziali in sequenza, più Funzione (i-bis) parser autorità addendum v1.3 (2026-05-28). (i) Inbox check — legge la inbox marketing@advisoryplus.it per intercettare reply weekend al Friday Email (STOP #N · MODIFICA #N · RINVIA #N a W[NN+X] · subject speciali STOP TUTTO/MODALITÀ FERIE/MODALITÀ CRISI) PRIMA della pubblicazione delle 09:00. Polling ogni 2h ven 18:30 → lun 06:00 (addendum v1.3). (i-bis) Parser autorità — applica solo reply provenienti da daniele.simonini@advisoryplus.it; auto-reply gentile + log per reply soci non-CEO; escalation per sender esterni. (ii) Status digest mattutino — produce digest sintetico in Markdown e WhatsApp/email al CEO con cosa pubblica oggi su quali canali, eventuali blocchi, stato sistemi. (iii) Health check execution — verifica che Buffer queue · LinkedIn MCP · Meta MCP · WordPress MCP · Brevo SMTP siano online e raggiungibili; segnala anomalie a MM e CEO. Se trova reply pending del CEO o sistema down, blocca pubblicazione interessata e notifica. Triggera lun 06:00 auto + manualmente via /adv-monday-open.
---
# 🌅 Skill week-mon — Monday Opening Routine Advisory+

> **L'alba operativa della settimana. Intercetta reply weekend, valida il piano, controlla i sistemi PRIMA della pubblicazione delle 09:00.**

---

## 1. Quando triggera

- **Automatico**: ogni **lunedì alle 06:00** via scheduled task
- **Manuale**: invocata dal MM o CEO con `/adv-monday-open` (per ri-eseguire dopo intervento manuale, o per anticipare la routine)
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false` → skip routine, sistema in pausa totale

Tempo target di esecuzione: **<5 minuti** (deve chiudere ben prima delle 09:00 per dare margine).

---

## 2. Output finale atteso

**Una notifica al CEO** (email + WhatsApp se configurato), formato sintetico:

```
☀️ Advisory+ · Monday Opening · W[NN] · [data]

Reply CEO weekend: [nessuna / N applicate / N pending blocco]
Reply soci non-CEO loggate: [nessuna / N — vedi file _reply_soci_loggate.md]
Pubblicazione oggi: [N] contenuti pianificati su [canali]
Sistemi: [tutti OK / X anomalia: descrizione]
Block list: [contenuti bloccati per reply CEO o sistema down]
Next sync: [eventuale azione richiesta CEO]
```

**Una entry di log** in `/05_Calendario_editoriale/Monday_opens/[YYYY-MM-DD]_open.md` con dettaglio per riferimento futuro.

---

## 3. Tre funzioni in sequenza

### Funzione (i) — Inbox check (priorità 1)

**Cosa fa**: legge la inbox `marketing@advisoryplus.it` (IMAP, configurato in `config/email.env`) dalla **chiusura del Friday Email (ven 18:00)** fino a **ora corrente (lun 06:00)**.

> **NOTA addendum v1.3 (2026-05-28):** parser autorita ristretto + polling 2h ven-lun + auto-reply soci non-CEO. Vedi "Funzione (i-bis) parser autorita" sotto. File canonico: `03_Aree_di_lavoro/09_Brand_Identity/Output_approvati/2026-05-28_brand_book_addendum_v1.3_friday_email_protocol_evoluto.md`.

**Polling**: dal 2026-05-28 ogni 2 ore ven 18:30 -> lun 06:00 via Cloud Scheduler GCP (era 1/sett lun 06:00). Razionale: 4 soci ricevono la Friday Email, responsiveness piu alta + auto-reply tempestiva ai non-CEO.

### Funzione (i-bis) — Parser autorità (addendum v1.3)

Per ogni reply, MM valuta header `From:` PRIMA di qualsiasi parsing del body.

| Sender della reply | Comportamento MM |
|---|---|
| `daniele.simonini@advisoryplus.it` | OK — applica reply al piano (pattern `STOP #N` / `MODIFICA #N` / `RINVIA #N` / `OK su tutto`) |
| `antonio.agostini@advisoryplus.it` | NON applica. Auto-reply gentile + log in `05_Calendario_editoriale/Friday_emails/[YYYY-MM-DD]_reply_soci_loggate.md` |
| `alberto.fappani@advisoryplus.it` | idem |
| `michele.barrella@advisoryplus.it` | idem |
| Altri sender | Notifica MM + escalation CEO via email |

Body auto-reply standard (vedi addendum v1.3 sez. C): "Per coerenza con Decision Authority Framework, le decisioni operative sul piano editoriale sono in capo a Daniele Simonini. Inoltragli osservazioni se vuoi siano applicate. Tracciate per audit retrospettivo."

**Cosa NON fare**: NON applicare al piano reply da sender non-Daniele. Nessuna eccezione.

**Cosa cerca** (solo reply da `daniele.simonini@advisoryplus.it`):

1. **Subject speciali** (azione globale):
   - `STOP TUTTO` → kill switch immediato → set `config/AUTOMAZIONE_ATTIVA = false` → notifica al MM
   - `MODALITÀ FERIE [data fine]` → attiva modalità ferie in `config/state.json` → fino a data fine, solo always-on minimi
   - `MODALITÀ CRISI` → attiva modalità crisi → blocco pubblicazione, MM in presidio manuale

2. **Reply al Friday Email** (azione per-content):
   - Pattern: `STOP #N` (N = indice contenuto nella sezione B del Friday Email)
   - Pattern: `MODIFICA #N: [istruzione]` (applica istruzione al contenuto N)
   - Pattern: `RINVIA #N a W[NN+X]` (sposta a settimana successiva o specificata)
   - Pattern: `OK #N` / `MODIFICA #N` / `RIFIUTA #N` per big bets sez. C
   - Pattern: `OK su tutto` → applica piano B integralmente, conferma esplicita

3. **Subject pattern emergency** (azione MM):
   - `URGENTE` → notifica MM via WhatsApp/email per intervento manuale
   - `SPUNTO` → aggiunge a `Spunti_CEO.md` per trattamento prossimo ciclo

**Cosa NON fa**:
- Non interpreta email libere senza i subject/pattern attesi (le inoltra al MM)
- Non risponde direttamente al CEO (l'eventuale conferma arriva nel digest sez. 2)

**Se zero reply CEO** → procedi con il piano B del Friday Email applicato in toto (silent approval window scaduta lun 06:00).

### Funzione (ii) — Status digest mattutino

Produce il digest descritto in sez. 2. Componenti:

- **Reply CEO applicate**: lista delle reply CEO weekend e cosa ha modificato sul piano
- **Reply soci non-CEO loggate**: contatore + riferimento al file `_reply_soci_loggate.md` (non applicate)
- **Pubblicazione di oggi**: contatore + dettaglio per canale (LinkedIn brand · LinkedIn Daniele semi-manuale · Instagram · Facebook · YouTube se schedulato · Blog se pubblicazione blog oggi · Newsletter se invio settimanale oggi)
- **Block list**: contenuti bloccati per reply CEO o sistema down (con motivo)
- **Next sync**: eventuali azioni richieste al CEO (firma post LinkedIn Daniele entro 09:00, OK big bet residuo, etc.)

### Funzione (iii) — Health check execution

Verifica che i sistemi necessari alla pubblicazione siano online e raggiungibili.

**Checklist**:

| Sistema | Check | Se KO |
|---|---|---|
| Brevo SMTP | API ping (libreria Brevo shell) | Notifica CEO + MM, blocca email |
| LinkedIn MCP (brand) | health check tool MCP | Notifica + blocca post LinkedIn brand |
| LinkedIn (Daniele personale, semi-manuale) | n/a — preparazione preview only | n/a |
| LinkedIn soci (Agostini · Fappani · Barrella) addendum v1.3 | token freshness check `linkedin_tokens_*.json` | Notifica + skip publish socio se token expired |
| Meta MCP (FB + IG) | health check | Notifica + blocca post FB/IG |
| WordPress.com MCP | health check | Notifica + blocca pubblicazione blog |
| Buffer/Publer (se in uso come ponte) | API ping | Notifica + fallback su MCP nativo |
| Google Calendar MCP | health check | Notifica, eventi calendario potrebbero non sincronizzare |
| HeyGen MCP | health check (solo se schedulato video AI) | Skip video, notifica |
| Supermetrics MCP | health check (solo per Friday Email next) | Skip KPI nel prossimo Friday |
| Cloudinary MCP | health check (solo se asset multimedia in pipeline) | Skip trasformazioni asset |
| cc-nano-banana CLI | binary ping | Notifica se rotto, fallback Canva |

**Soglia critica**: se >50% dei sistemi necessari alla pubblicazione di oggi sono KO → **blocco totale pubblicazione + notifica urgente CEO**.

---

## 4. Logica di esecuzione — passo-passo

1. **Eseguire kickoff** (skill `advisory-plus:kickoff`) per caricare contesto workspace
2. **Verificare** `config/AUTOMAZIONE_ATTIVA` (se false → skip + notifica)
3. **Verificare** `config/state.json` per modalità ferie/crisi attive
4. **Eseguire Funzione (i)** Inbox check via Bash + libreria IMAP
5. **Applicare Funzione (i-bis)** parser autorità → distingue reply CEO (da applicare) da reply soci non-CEO (auto-reply + log) da sender esterni (escalation)
6. **Applicare** reply CEO al piano della settimana (file `/05_Calendario_editoriale/[YYYY-MM]_*.md`)
7. **Inviare auto-reply** ai soci non-CEO eventualmente intercettati + appendere log
8. **Eseguire Funzione (iii)** Health check sistemi
9. **Comporre Funzione (ii)** Status digest
10. **Inviare** digest via email a CEO (Brevo SMTP) + WhatsApp (Twilio fase 2)
11. **Log** in `/05_Calendario_editoriale/Monday_opens/[YYYY-MM-DD]_open.md`
12. **Schedulare** pubblicazione di oggi (ogni contenuto al suo orario) — handoff a skill `adv-publish-*` (Sessione 7)

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

### Modalità Ferie attiva
- Skip Funzione (i) — non si applicano reply ad un piano in pausa
- Funzione (ii) si limita a "Modalità Ferie attiva fino al [data]. Always-on minimo eseguito (1 post P1 ed. settimanale)."
- Funzione (iii) check minimo (solo SMTP e blog)

### Reply socio non-CEO con contenuto sostanziale (addendum v1.3)
- MM NON inferisce intent di applicare al piano
- Auto-reply gentile standard (vedi Funzione i-bis) + log in `_reply_soci_loggate.md`
- Annotazione in Friday Email W+1 sez. F (Trust Calibration) se ricorrente: "ricevute N reply soci non-CEO loggate questa settimana"

---

## 6. Cosa NON fare mai

- ❌ **Applicare reply non provenienti da `daniele.simonini@advisoryplus.it`** al piano editoriale (addendum v1.3 — nessuna eccezione)
- ❌ **Eseguire la pubblicazione delle 09:00 senza aver completato Funzione (i) + (i-bis)** (rischio: pubblicare contenuto vetoato dal CEO durante il weekend)
- ❌ **Marcare un sistema KO come "ok" per sicurezza** — meglio bloccare e notificare
- ❌ **Inviare digest dopo le 07:00** senza notifica preventiva (CEO ha bisogno di leggere prima dell'eventuale finestra di intervento manuale)
- ❌ **Auto-rispondere al CEO** — la skill informa, non dialoga
- ❌ **Saltare il log** in `/Monday_opens/` o in `/Friday_emails/[YYYY-MM-DD]_reply_soci_loggate.md` (sono memoria operativa)
- ❌ **Bypassare AUTOMAZIONE_ATTIVA = false** in nome dell'efficienza
- ❌ **Interpretare creativamente** reply CEO ambigue — chiedere via notifica
- ❌ **Cambiare il body auto-reply standard** per soci non-CEO senza passare da chat 09 Brand Identity (è canonico, addendum v1.3 sez. C)

---

## 7. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di eseguire, leggi in ordine:

1. `/00_README.md`
2. `/00_Brand_Book_v1.2.md` (sez. 13 MM Decision Authority · sez. 13.5 Friday Email Protocol + NOTA addendum v1.3)
3. `/01_Team/00_Marketing_Manager.md`
4. `/03_Aree_di_lavoro/09_Brand_Identity/Output_approvati/2026-05-28_brand_book_addendum_v1.3_friday_email_protocol_evoluto.md` (riferimento normativo parser autorità)
5. `/05_Calendario_editoriale/[YYYY-MM]_*.md` (piano in corso)
6. `/05_Calendario_editoriale/Friday_emails/[ultimo].md` (per riferimenti #N reply)
7. `/05_Calendario_editoriale/Friday_emails/[YYYY-MM-DD]_reply_soci_loggate.md` (se esiste, per evitare duplicate logging)
8. `config/AUTOMAZIONE_ATTIVA` · `config/state.json` · `config/email.env` · `config/pillars-of-month.json`

---

*Plugin v1.1.8 — SKILL v1.1 advisory-plus:week-mon — Sessione 2 Plugin Build 2026-05-17 · cascata addendum v1.3 + ricostruzione sez. 5-7 Sessione 24 2026-05-28*
