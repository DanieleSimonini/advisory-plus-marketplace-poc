---
name: publish-linkedin-pagina
description: Pubblica post sulla LinkedIn Pagina Aziendale Advisory+ (`/company/advisory-plus20/`) via LinkedIn Pages API (post-approvazione LinkedIn Marketing Developer Platform â€” procedura 2-4 settimane in corso). Fallback transitorio Buffer/Publer scheduling via Chrome MCP se MDP non ancora approvato. Doppio gate Compliance OBBLIGATORIO: (1) alla scrittura del post (skill content-*) Â· (2) T-30min pre-pubblicazione (drift check re-invocato automatico). Screenshot post-publish via Chrome MCP entro 2 min + log permalink in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`. Kill switch `config/AUTOMAZIONE_ATTIVA = false` blocca tutto. Tutta la logica tecnica delegata a `scripts/publish-linkedin.sh` (Sessione 7 script). Skill orchestra: lettura post approvato + verifica Compliance T-30min + invocazione script + log + screenshot + update calendario editoriale stato "Pubblicato".
---
# ðŸ“¤ Skill publish-linkedin-pagina â€” Pubblicazione LinkedIn Pagina Aziendale

> **API ufficiale post-MDP Â· fallback Buffer Â· gate-doppio compliance Â· log+screenshot Â· kill switch.**

---

## 1. Quando triggera

- **Schedulazione automatica** ogni volta che il calendario editoriale ha un post LinkedIn Pagina in stato `Programmato` con timestamp imminente (T-30min trigger del pre-publish check)
- Invocata da `advisory-plus:publish-scheduling` come step di esecuzione canale-specifico
- Invocata on-demand dal MM per pubblicazione ad-hoc (es. risposta rapida a news, big bet CEO)
- Mai trigger se kill switch `config/AUTOMAZIONE_ATTIVA = false`
- Mai trigger se Crisis mode o Vacation mode totale attivo

Tempo target di esecuzione: **3-5 minuti** end-to-end (pre-check + publish + screenshot + log).

---

## 2. Output finale atteso

**Log entry** in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`:

```markdown
## Pubblicazione 2026-XX-XX HH:MM â€” LinkedIn Pagina

- **Skill chiamante**: advisory-plus:publish-linkedin-pagina
- **ModalitÃ  pubblicazione**: [api_mdp | buffer_fallback | chrome_mcp_manual]
- **Post source**: Output_approvati/02_LinkedIn/2026-XX-XX_LI-Pagina_[tema]_[variante].md
- **Pillar**: P[N] [Nome]
- **Voce**: [Spiegato Facile / Caso Reale / Analisi]
- **Compliance check T-30min**: ðŸŸ¢ (drift check OK)
- **Permalink**: https://www.linkedin.com/feed/update/urn:li:share:[ID]
- **Screenshot**: 04_Risorse/_log_screenshots/LI-pagina_[YYYY-MM-DD]_HHMM.png
- **Stato calendario editoriale**: aggiornato da `Programmato` â†’ `Pubblicato ðŸŸ¢`
- **Eventuali avvisi**: [nessuno | API quota near-limit | Buffer fallback usato perchÃ© ...]
```

E **calendario editoriale aggiornato** (stato Pubblicato + permalink) via skill `production-editorial-calendar`.

---

## 3. ModalitÃ  di pubblicazione (3 alternative, in ordine di preferenza)

### ModalitÃ  A â€” LinkedIn Pages API ufficiale (target a regime, post-MDP approval)
- **Endpoint**: LinkedIn Pages API `/rest/posts` (UGC Posts API)
- **Auth**: OAuth 2.0 con token long-lived a livello Organization (Pagina Advisory+ ID)
- **Permission required**: `w_organization_social` + `r_organization_social` + `rw_organization_admin`
- **Limite quota**: ~150 post/giorno per pagina (largamente sufficiente per le nostre 2-3/sett)
- **Status**: â³ **PENDENZA CEO** â€” applicazione LinkedIn Marketing Developer Platform da avviare (procedura 2-4 settimane di approvazione)
- **Vantaggi**: pubblicazione nativa, no intermediari, no cost extra
- **Activation**: dopo OK LinkedIn MDP â†’ setup token in `config/email.env` (campo `LINKEDIN_PAGE_TOKEN`)

### ModalitÃ  B â€” Buffer/Publer fallback (transitorio finchÃ© MDP non approvato)
- **Strategia**: pubblicazione via Buffer (o Publer) come ponte tecnico, schedulazione gestita in piattaforma esterna
- **Auth**: API key Buffer/Publer in `config/email.env`
- **Limite quota**: piano Buffer Free 10 post pending + 1 social account Â· piano Buffer Essentials ~6$/mese 1 account 100 post pending
- **Status**: âœ… **DISPONIBILE IMMEDIATAMENTE** (richiede solo iscrizione Buffer + connessione Pagina LinkedIn + API key â€” ~15min setup CEO)
- **Vantaggi**: zero attesa, scheduling robusto
- **Svantaggi**: piccolo overhead di costo Buffer Essentials, ulteriore intermediario nella catena
- **Activation**: account Buffer Free o Essentials + connessione Pagina + API key in `config/email.env`

### ModalitÃ  C â€” Chrome MCP semi-manuale (emergency fallback)
- **Strategia**: Chrome MCP apre LinkedIn, naviga a Pagina Advisory+, prepara post nel composer, invia notifica via email al CEO per click finale "Pubblica"
- **Auth**: nessuna (CEO Ã¨ giÃ  loggato sul suo browser)
- **Status**: âœ… **DISPONIBILE COME ULTIMA RISORSA**
- **Svantaggi**: richiede sempre il click manuale del CEO â†’ NO automazione vera
- **Quando usarla**: solo se ModalitÃ  A non approvata + ModalitÃ  B non funzionante per qualche ragione tecnica + post urgente non posticipabile

### Selezione modalitÃ  (logica)
1. Se `config/email.env` ha `LINKEDIN_PAGE_TOKEN` valido e MDP approvato: usa ModalitÃ  A
2. Se `config/email.env` ha `BUFFER_API_KEY` valida: usa ModalitÃ  B
3. Altrimenti: invoca ModalitÃ  C (Chrome MCP) + invia email warning al CEO ("modalitÃ  manuale attivata, considera attivare Buffer")

---

## 4. Pre-publish check (T-30 minuti, automatico)

Schedulato 30 minuti prima del timestamp programmato. Esegue:

### 4.1 Compliance drift check
Re-invoca `advisory-plus:compliance-gate-doppio` (Compliance Officer + Brand Strategist) sul post finale:
- Verifica che nulla sia cambiato tra T-30min e ora di scrittura (es. denominazione mandatarie ancora corretta, no claim ðŸ”´ introdotti)
- Verifica AI disclosure se applicabile
- Verifica disclaimer RUI integrale o compatto a seconda del canale (Pagina LinkedIn: disclaimer bio fa copertura per post brand â€” Brand Book v1.2 sez. 7)

**Esiti**:
- ðŸŸ¢ â†’ procede con publish
- ðŸŸ¡ â†’ notifica MM + breve pausa fino a riformulazione (max 1 iterazione)
- ðŸ”´ â†’ blocco immediato + email alert CEO entro 1h + post rimane in stato `Bloccato` nel calendario

### 4.2 Brand Strategist coerenza check
- Pillar dichiarato vs contenuto effettivo
- Voce dichiarata vs voce effettiva
- Tetto Badvisor 20% mensile cumulato (se voce Badvisor)
- Ratio firma 80/20 (non applicabile per Pagina, applicabile per profili personali â€” vedi publish-linkedin-daniele)
- Mai Badvisor su Pagina brand (Brand Book v1.2 sez. 5)

### 4.3 Health check tecnico
- Quota API disponibile (ModalitÃ  A: <80% quota giornaliera Â· ModalitÃ  B: <80% quota Buffer pending)
- Token validitÃ  (LinkedIn token long-lived scade ogni 60gg â†’ refresh proattivo)
- Network reachability (skip se rete down â€” riprogramma di 15 min)

### 4.4 Kill switch & Crisis check
- `config/AUTOMAZIONE_ATTIVA = false` â†’ STOP, nessuna pubblicazione (post resta `Programmato` finchÃ© flag torna `true`)
- Crisis mode globale attivo â†’ STOP + email alert CEO
- Vacation mode totale â†’ STOP

---

## 5. Logica di esecuzione â€” passo-passo

1. **Schedulazione T-30min** (cron via scheduled-tasks MCP) attiva pre-publish check
2. **Pre-publish check** (sez. 4): se ðŸ”´ o blocco â†’ exit + log
3. **Selezione modalitÃ ** (sez. 3): A Â· B Â· C
4. **Leggere post finale** da `Output_approvati/02_LinkedIn/[file].md`
5. **Estrarre payload**: testo + hashtag + URL primo commento (se presente) + UTM parameter aggiunti automaticamente (`utm_source=linkedin_page&utm_medium=organic&utm_campaign=P[N]_[tema]`)
6. **Invocare script** `scripts/publish-linkedin.sh [modalitÃ ] [post-id] [payload-json]` (Sessione 7 script)
7. **Ricevere response**:
   - ModalitÃ  A: post URN + permalink immediato
   - ModalitÃ  B: Buffer scheduled ID + Buffer dashboard link
   - ModalitÃ  C: Chrome MCP screenshot composer + email CEO
8. **Attesa T+2min** per assicurarsi che il post sia visibile pubblicamente (rilevante per ModalitÃ  A â€” puÃ² esserci delay 30s-2min)
9. **Invocare script** `scripts/log-publish.sh [canale] [permalink]` per screenshot via Chrome MCP + salvataggio in `/04_Risorse/_log_screenshots/`
10. **Aggiornare log** `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md` (append entry)
11. **Aggiornare calendario editoriale** via `production-editorial-calendar`: stato Pubblicato + permalink + screenshot path
12. **Notificare MM** (sintetico, no email â€” solo log calendario) con esito

---

## 6. Casi particolari

### Post con hashtag #LavoroVersilia o #Apuana
**MAI**. Brand Book v1.2 sez. 2 â€” posizionamento nazionale. Compliance gate-doppio blocca con ðŸ”´ se rilevati.

### Post con loghi mandatarie nel body
**MAI**. Vincolo IVASS hard. Loghi solo in disclosure footer. Compliance gate-doppio blocca con ðŸ”´.

### Post con voce Badvisor
**MAI su Pagina brand** (Brand Book v1.2 sez. 5). Badvisor Ã¨ ammesso solo su profili personali (LI Daniele) o IG/Reel. Compliance gate-doppio blocca con ðŸ”´.

### Pubblicazione richiesta in finestra "Vacation mode parziale"
Vacation mode parziale (riduzione frequenza 50%) â†’ publish-linkedin-pagina rispetta frequenza ridotta. Se il post in calendario Ã¨ in finestra Vacation â†’ skip + notifica MM "post posticipato a fine vacation".

### Post in attesa di asset visivo
Se il post ha `visual_brief.cover_blog = pending` o equivalente â†’ blocco temporaneo + notifica MM + Art Director invocato per generazione asset (handoff a `visual/cover-blog` o `visual/image-static-nano-banana`).

### Quota API esaurita (ModalitÃ  A)
Se LinkedIn API quota >80% â†’ switch automatico a ModalitÃ  B (Buffer) per ridurre carico API.

### Big bet con approvazione CEO esplicita
Big bet (Brand Book v1.2 sez. 13) ha stato calendario `Approvato CEO âœ…` â†’ bypass del pre-publish check Compliance (giÃ  approvato esplicitamente dal CEO) ma mantiene health check tecnico + kill switch.

---

## 7. KPI publish-linkedin-pagina (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Tasso di successo pubblicazione (no errori) | â‰¥99% |
| Latency tra timestamp programmato e pubblicazione effettiva | <2 min |
| Compliance drift check fallito (ðŸ”´) | <1% pubblicazioni |
| Screenshot caricato con successo entro T+5min | â‰¥98% |
| Kill switch attivato in emergenza | <1 volta/anno (auspicabile mai) |

---

## 8. Compliance & sicurezza

âœ… **Doppio gate Compliance**: alla scrittura (skill content-*) + T-30min drift check (questa skill)
âœ… **Screenshot post-publish** in `/04_Risorse/_log_screenshots/` per audit trail
âœ… **Permalink loggato** in `/05_Calendario_editoriale/Log_pubblicati/`
âœ… **Kill switch globale** rispettato in ogni invocazione
âœ… **Token sicurezza**: `config/email.env` mai committato in git (gitignored)
âœ… **UTM parameter** aggiunti per attribution model (`data-attribution-model` Sessione 5)
âœ… **Posizionamento nazionale**: blocco automatico su #LavoroVersilia/#Apuana/Toscana default
âœ… **No claim ðŸ”´**: blocco automatico (gate-doppio)
âœ… **No loghi mandatarie body**: blocco automatico
âœ… **No Badvisor su Pagina brand**: blocco automatico

âŒ **Mai**:
- Pubblicazione senza pre-publish check
- Pubblicazione senza screenshot + log
- Pubblicazione di big bet senza OK CEO esplicito documentato
- Modifica del payload tra approvazione e pubblicazione (rischio drift)
- Push commerciale aggressivo (CTA non vincolante, sempre)

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pubblicare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia LinkedIn Â· sez. 7 Compliance Â· sez. 13 MM Decision Authority)
2. `/01_Team/03_Social_Media_Manager.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (LinkedIn Pagina ID, mandatarie, claim ammessi/vietati, Posizionamento nazionale)
4. `config/email.env` (LINKEDIN_PAGE_TOKEN o BUFFER_API_KEY)
5. `config/AUTOMAZIONE_ATTIVA` (kill switch)
6. Post sorgente in `Output_approvati/02_LinkedIn/`
7. Calendario editoriale corrente per slot + dipendenze
8. Log pubblicazioni recenti per evitare duplicati

---

## 10. Cosa NON fare mai

- âŒ **Pubblicare senza pre-publish check** (Compliance drift T-30min Â· health check Â· kill switch)
- âŒ **Pubblicare Badvisor su Pagina brand** (Brand Book v1.2 sez. 5)
- âŒ **Pubblicare con loghi mandatarie nel body** (vincolo IVASS hard)
- âŒ **Modificare payload tra approvazione e pubblicazione** (drift = rischio compliance)
- âŒ **Ignorare kill switch** (`config/AUTOMAZIONE_ATTIVA = false` â†’ STOP non negoziabile)
- âŒ **Skip screenshot post-publish** (audit trail obbligatorio)
- âŒ **Pubblicare in Crisis mode** o vacation mode totale
- âŒ **Refresh token automatico** senza notifica CEO (token expire ogni 60gg â†’ preavviso 7gg)
- âŒ **Hashtag territoriali** (Versilia/Apuana/Toscana default vietati)
- âŒ **Push commerciale aggressivo** (Brand Book v1.2 sez. 4 â€” consulenza non vendita)

---

*SKILL v1.0 â€” advisory-plus:publish-linkedin-pagina â€” Sessione 7 Plugin Build â€” 2026-05-22*

