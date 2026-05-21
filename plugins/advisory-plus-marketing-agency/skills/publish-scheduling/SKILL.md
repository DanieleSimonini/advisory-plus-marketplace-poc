---
name: publish-scheduling
description: Orchestrator centrale di TUTTE le pubblicazioni programmate Advisory+ su 8 canali (LI Pagina Â· LI Daniele semi-manuale Â· IG Â· FB Â· Blog Â· Newsletter Â· YouTube Â· WhatsApp utility event-driven). Esegue il polling continuo del calendario editoriale per slot in stato `Programmato`, attiva il pre-publish check T-30 minuti per ogni slot, invoca la skill canale-specifica appropriata (publish-linkedin-pagina Â· publish-linkedin-daniele Â· publish-meta Â· publish-wordpress Â· email-newsletter via Brevo Â· publish-youtube via API o Chrome MCP). Implementa: KILL SWITCH globale (`config/AUTOMAZIONE_ATTIVA = false` â†’ STOP), CRISIS MODE (blocco tutti i flow non-utility), VACATION MODE (parziale 50% riduzione Â· totale stop), retry exponential backoff su errori transitori, audit log centralizzato in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_master_log.md`. Compliance gate-doppio applicato a OGNI pubblicazione. Cron schedulato via scheduled-tasks MCP (Sessione 8).
---
# ðŸŽ› Skill publish-scheduling â€” Orchestrator centrale pubblicazioni programmate

> **8 canali Â· kill switch Â· crisis/vacation mode Â· gate-doppio per ogni publish Â· retry Â· audit log centralizzato.**

---

## 1. Quando triggera

- **Cron schedulato ogni 15 minuti** via scheduled-tasks MCP (Sessione 8): polling calendario per slot `Programmato` con timestamp imminente (entro T+45min)
- Invocata da `production-editorial-calendar` quando cambia uno stato (passaggio Approvato â†’ Programmato)
- Invocata on-demand dal MM per forzare un publish (es. urgenza Â· big bet con OK CEO)
- **Mai trigger** se kill switch `config/AUTOMAZIONE_ATTIVA = false`
- **Stop conditional**: Crisis mode globale Â· Vacation mode totale

Tempo target di esecuzione: **2-5 min** per iterazione polling (no pubblicazioni in coda) Â· **5-15 min** se 1-3 publish da orchestrare nella iterazione.

---

## 2. Output finale atteso

**Master log** in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_master_log.md`:

```markdown
## Iterazione orchestrator 2026-XX-XX HH:MM

- **Slot rilevati in calendario** (stato Programmato, timestamp â‰¤T+45min): N
- **Slot processati**:
  - [HH:MM] LinkedIn Pagina Â· pillar P[N] Â· esito ðŸŸ¢ â†’ handoff publish-linkedin-pagina
  - [HH:MM] Newsletter Â· pillar P[N] Â· esito ðŸŸ¡ (drift Compliance) â†’ riformulazione MM
  - [HH:MM] Blog THE ADVISOR Â· pillar P[N] Â· esito ðŸŸ¢ â†’ handoff publish-wordpress
- **Kill switch**: âœ… ACTIVE
- **Crisis mode**: âŒ OFF
- **Vacation mode**: parziale (Daniele OOO 23-30 mag) â€” Pillar 2 always-on saltato per quest'iterazione
- **Token health**: Meta OK (32 giorni a scadenza Â· refresh proattivo programmato T+25gg) Â· WordPress OK Â· Brevo OK Â· LinkedIn pending MDP
- **Eventuali avvisi**: [...]
```

E **handoff a skill canale-specifiche** per ogni slot processato. Ogni skill canale-specifica produce il proprio log entry (sez. 2 di `publish-linkedin-pagina` Â· `publish-meta` Â· `publish-wordpress` Â· etc.).

---

## 3. Mapping slot â†’ skill canale-specifica

| Canale calendario | Skill canale-specifica | Note |
|---|---|---|
| LinkedIn Pagina | `advisory-plus:publish-linkedin-pagina` | API + fallback Buffer |
| LinkedIn Daniele | `advisory-plus:publish-linkedin-daniele` | Semi-manuale, click finale Daniele |
| LinkedIn altri soci (Agostini/Barrella/Fappani) | `advisory-plus:publish-linkedin-daniele` (variante con destinatario notifica) | Semi-manuale, click finale del socio firmatario |
| Instagram | `advisory-plus:publish-meta` | Post Â· carosello Â· Reel Â· Stories |
| Facebook | `advisory-plus:publish-meta` | Post + cross-post da IG |
| Blog THE ADVISOR | `advisory-plus:publish-wordpress` | WordPress.com MCP |
| Newsletter | `advisory-plus:publish-newsletter` (handoff a script `brevo-create-campaign.sh`) | Brevo API REST v3 |
| YouTube | `advisory-plus:publish-youtube` (futura â€” pre-launch giugno 2026) | YouTube Data API v3 |
| WhatsApp utility | event-driven, non in calendario standard | Twilio MCP (fase 2) |

âš ï¸ **Pubblicazione newsletter, YouTube, WhatsApp** sono coperte da skill placeholder/future in v1.1, non da skill dedicate in questa sessione. Il pattern resta identico (drift check + invocazione script).

---

## 4. Pre-publish check globale (orchestrator level)

### 4.1 Kill switch check (sempre, ad ogni iterazione)
```
if config/AUTOMAZIONE_ATTIVA == "false":
    log "Kill switch attivo, nessuna pubblicazione"
    return
```

### 4.2 Crisis mode check
```
if config/MODALITA_CRISI == "true":
    log "Crisis mode attivo, blocco tutto non-utility"
    notify_CEO("Crisis mode: N pubblicazioni saltate")
    return
```

### 4.3 Vacation mode check
- **Vacation totale**: stop completo
- **Vacation parziale**: riduzione 50% (skip 1 slot ogni 2 nel ciclo di rotazione, mantieni utility + Friday Email + WhatsApp)
- **Daniele OOO**: skip Pillar 2 always-on personale + rinvia ai prossimi slot Daniele

### 4.4 Token health check (ogni iterazione)
Verifica scadenza dei token API critici:
- Meta long-lived: scadenza 60gg â†’ refresh proattivo a 7gg dalla scadenza
- WordPress.com MCP: scadenza variabile (token Bearer) â†’ refresh proattivo a 7gg
- Brevo API key: stabile (no scadenza standard, ma rotazione raccomandata annuale)
- LinkedIn API: post-MDP approval token long-lived 60gg â†’ refresh proattivo a 7gg

Se token scadenza â‰¤7gg: tenta refresh automatico + notifica CEO entro 1h se fallisce.

### 4.5 Schedulazione pre-publish T-30min per ogni slot
Per ogni slot in calendario `Programmato` con timestamp <= now + 45min:
1. Verifica che pre-publish T-30min check non sia giÃ  stato eseguito (idempotenza)
2. Determina skill canale-specifica (mapping sez. 3)
3. Invoca skill canale-specifica via Task tool con flag `mode=pre_publish_check`
4. Skill canale-specifica esegue il drift Compliance + health check (sez. 4 di ogni skill)
5. Esito ðŸŸ¢ â†’ ok, attesa T-0 per publish Â· ðŸŸ¡ â†’ riformulazione Â· ðŸ”´ â†’ blocco

### 4.6 Retry exponential backoff su errori transitori
Errori transitori (network, API quota, 5xx server) â†’ retry con backoff:
- Tentativo 1: T+5min
- Tentativo 2: T+15min
- Tentativo 3: T+45min
- Se persistente: blocco + notifica MM

Errori non-transitori (4xx auth, validation error) â†’ blocco immediato + notifica CEO.

---

## 5. Logica di esecuzione â€” passo-passo (iterazione cron ogni 15min)

1. **Cron trigger** (scheduled-tasks MCP, ogni 15min Â· es. :00 :15 :30 :45)
2. **Cascata di contesto** (sez. 12)
3. **Kill switch check** (sez. 4.1): se OFF â†’ STOP iterazione + log
4. **Crisis mode check** (sez. 4.2): se ON â†’ STOP non-utility + notify CEO + log
5. **Vacation mode check** (sez. 4.3): applica filtri
6. **Token health check** (sez. 4.4): refresh proattivo se necessario
7. **Polling calendario editoriale**: leggi `/05_Calendario_editoriale/[YYYY-MM]_calendario.md`, filtra slot `Programmato` con timestamp `>= now AND <= now + 45min`
8. **Per ogni slot**:
   a. Determina skill canale-specifica (mapping sez. 3)
   b. **Pre-publish check T-30min**: invoca skill canale-specifica con `mode=pre_publish_check`
   c. Esito ðŸŸ¢ â†’ attendi T-0 trigger publish Â· ðŸŸ¡ â†’ riformulazione Â· ðŸ”´ â†’ blocco + notifica MM
9. **Per slot in stato Compliance OK e T-0 raggiunto**:
   a. Invoca skill canale-specifica con `mode=publish`
   b. Ricevi response (permalink + screenshot path)
   c. Aggiorna calendario editoriale (handoff `production-editorial-calendar`)
   d. Aggiorna master log
10. **Compilare master log** dell'iterazione (sez. 2)
11. **Notificare MM** se anomalie (ðŸ”´ Â· token scadenza imminente Â· token refresh fallito Â· errori retry esauriti)
12. **Cron schedula** prossima iterazione (auto)

---

## 6. ModalitÃ  operative speciali

### 6.1 ModalitÃ  "Shadow" (test pre-go-live Â· primi 7 giorni post-deploy plugin)
**Configurabile** via `config/MODALITA_SHADOW = true`.

In modalitÃ  Shadow:
- Orchestrator esegue tutti i pre-publish check
- Logga cosa farebbe (skill chiamata, payload, schedulazione)
- **NON** invoca le skill canale-specifiche con `mode=publish`
- MM verifica i log shadow ogni mattina
- Se tutto OK per 7 giorni â†’ switch a `MODALITA_SHADOW = false` (go-live automazione)

### 6.2 ModalitÃ  "Drain" (pre-vacation/pre-shutdown)
**Configurabile** via `config/MODALITA_DRAIN = "[data]"`.

In modalitÃ  Drain:
- Orchestrator pubblica tutti gli slot `Programmato` con timestamp â‰¤ data drain
- Slot con timestamp > data drain â†’ stato `Sospeso fino [data fine drain]`
- Drain finita â†’ ripristino normale

### 6.3 ModalitÃ  "Sandbox" (testing)
**Configurabile** via `config/MODALITA_SANDBOX = true`.

In modalitÃ  Sandbox:
- Pubblicazioni dirette a ambienti di test (LinkedIn page test Â· IG test Â· WordPress staging Â· Brevo test list)
- Mai pubblicare su account produzione
- Per dev/QA del plugin

---

## 7. Audit log centralizzato

`/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_master_log.md` Ã¨ log master mensile. Conserva:
- Ogni iterazione orchestrator (ora Â· esito Â· slot processati)
- Aggregazione: N pubblicazioni totali nel mese Â· N successi Â· N fallimenti Â· N blocchi Compliance Â· N retry
- Token refresh events
- Kill switch / Crisis / Vacation events
- Anomalie significative

**Retention**: 12 mesi attivi + archivio in `/99_Archivio/Log_pubblicati_storici/[anno]_master_log.md`.

**Audit GDPR**: nessun dato personale di utenti nei master log (solo pubblicazioni Advisory+, non interazioni utenti).

---

## 8. Casi particolari

### Slot collisione (piÃ¹ publish stesso minuto)
- Se 2+ slot stesso minuto: serializzazione sequenziale (publish A â†’ wait T+30s â†’ publish B)
- Evita race condition su API quotas

### Big bet "ultra-urgente" con OK CEO mid-iteration
- MM forza publish via on-demand â†’ orchestrator esegue immediatamente (skippa cron 15min wait)
- Esegue comunque pre-publish check + Compliance gate

### Errore skill canale-specifica (es. 500 server WordPress)
- Retry exponential backoff (sez. 4.6)
- Se 3 tentativi fallano â†’ blocco slot + notifica MM + flag `Errore_persistente` nel calendario
- MM decide se riprovare manualmente o archiviare

### Token Meta refresh fallito
- Notifica CEO entro 1h ("Token Meta scaduto, riconnetti app via [link]")
- Slot IG/FB programmati â†’ stato `Sospeso token refresh` finchÃ© CEO non riconnette
- Altri canali continuano operativi

### Polling calendario rileva slot stato anomalo (es. `Programmato` ma timestamp passato)
- Slot "in ritardo" >2h dal timestamp â†’ flag automatica + log "Slot in ritardo, decisione MM"
- Slot "in ritardo" <2h â†’ riprova publish (potrebbe essere stato un cron mancato)

### Conflitto tra Vacation mode e big bet CEO
- Big bet con OK CEO esplicito â†’ override Vacation mode (CEO ha giÃ  autorizzato esplicitamente)
- Documentato nel log "Big bet override vacation"

---

## 9. KPI publish-scheduling (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Pubblicazioni programmate vs effettive | â‰¥98% (gap = vacation/crisis/big bet override) |
| Latency tra timestamp programmato e pubblicazione effettiva | <5 min mediana |
| Compliance drift block rate (ðŸ”´ al T-30min) | <2% |
| Retry success rate (errori transitori) | â‰¥80% |
| Token refresh proattivo (>7gg scadenza) | 100% |
| Kill switch usato in emergenza | <1 volta/anno (auspicabile mai) |
| Master log accuratezza | 100% pubblicazioni loggate |

---

## 10. Integrazione cross-skill

### Dipendenze in input
- `production-editorial-calendar`: fonte di slot programmati
- `compliance-gate-doppio`: gate verificato pre-publish T-30min
- `config/email.env`: token API per ogni canale
- `config/AUTOMAZIONE_ATTIVA`: kill switch
- `config/MODALITA_*`: crisis Â· vacation Â· shadow Â· drain Â· sandbox

### Skill invocate in output (Task tool)
- `publish-linkedin-pagina`
- `publish-linkedin-daniele`
- `publish-meta`
- `publish-wordpress`
- (Sessione 7 placeholder) `publish-newsletter` via `brevo-create-campaign.sh`
- (Pre-launch) `publish-youtube`
- `production-editorial-calendar` (update stato post-publish)
- `compliance-gate-doppio` (drift check)

### Cron correlati (scheduled-tasks MCP Sessione 8)
- Friday Email Protocol (ven 18:00) â€” `strategia-week-fri`
- Monday Status (lun 06:00) â€” `strategia-week-mon`
- Monthly report (ultimo ven mese) â€” `data-monthly-performance-report`
- CRM lifecycle recompute (1Â° mese 03:00) â€” `crm-lifecycle`
- Asset audit (1Â° trimestre) â€” `production-asset-library`
- Technical SEO audit (1Â° trimestre) â€” `seo-technical-audit`

---

## 11. Compliance & sicurezza

âœ… **Kill switch globale** sempre verificato prima di qualsiasi azione
âœ… **Crisis mode** rispettato â€” stop tutto non-utility
âœ… **Vacation mode** rispettato â€” parziale o totale
âœ… **Gate-doppio Compliance** invocato T-30min su ogni slot
âœ… **Token health** monitorato continuo + refresh proattivo 7gg
âœ… **Master audit log** completo + immutabile (append-only)
âœ… **Big bet override** documentato esplicitamente nel log
âœ… **No publish in modalitÃ  sandbox** verso produzione
âœ… **No publish senza OK CEO** per big bet
âœ… **Notifica CEO** entro 1h per errori critici

âŒ **Mai**:
- Bypassare kill switch
- Pubblicare in Crisis mode (eccetto utility WhatsApp)
- Modifica payload tra approvazione e pubblicazione
- Retry infinito (max 3 tentativi exponential backoff, poi blocco)
- Token refresh manuale senza notifica CEO
- Audit log corrotto o cancellato (append-only)
- Pubblicare slot stato anomalo (in ritardo >2h) senza decisione MM

---

## 12. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di ogni iterazione orchestrator, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia canali Â· sez. 7 Compliance Â· sez. 13 MM Decision Authority + Trust Calibration)
2. `/01_Team/00_Marketing_Manager.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (canali attivi, frequenze)
4. `config/AUTOMAZIONE_ATTIVA` (kill switch)
5. `config/MODALITA_*` (crisis, vacation, shadow, drain, sandbox)
6. `config/email.env` (token API per token health check)
7. `/05_Calendario_editoriale/[YYYY-MM]_calendario.md` (slot programmati)
8. `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_master_log.md` (log iterazioni precedenti per idempotenza)

---

## 13. Cosa NON fare mai

- âŒ **Pubblicare senza pre-publish check** Compliance gate-doppio
- âŒ **Bypassare kill switch / Crisis mode / Vacation mode totale**
- âŒ **Pubblicare slot ottenuto fuori dal calendario editoriale** (Slot non noti = no audit trail = compliance risk)
- âŒ **Retry infinito** su errori â€” max 3 tentativi
- âŒ **Token refresh manuale** senza notifica CEO
- âŒ **Modifica master log** post-fatto (append-only)
- âŒ **Race condition** su slot collisioni (sempre serializzare con T+30s gap)
- âŒ **Pubblicare in sandbox verso produzione** (verifica MODALITA_SANDBOX prima)
- âŒ **Skip log entries** (audit trail integrale)
- âŒ **Notifica CEO** generica â€” sempre specifica (canale Â· slot Â· ragione)

---

*SKILL v1.0 â€” advisory-plus:publish-scheduling â€” Sessione 7 Plugin Build â€” 2026-05-22*

