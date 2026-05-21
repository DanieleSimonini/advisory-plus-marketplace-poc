---
name: publish-linkedin-daniele
description: Pubblicazione SEMI-MANUALE LinkedIn profilo personale Daniele Simonini (decisione CEO 2026-05-16 etica: voce personale richiede click finale di Daniele, NO automazione completa). Skill prepara il post pronto, esegue gate-doppio Compliance, poi apre Chrome MCP su LinkedIn (profilo Daniele giÃ  loggato), incolla il testo nel composer, NON clicca pubblica â€” invia email/notifica a Daniele "post pronto, rileggi e clicca". Dopo conferma Daniele clicca â†’ skill rileva il post live entro 5 min via Chrome MCP scraping permalink + screenshot + log. Caso unico nel plugin: tutti gli altri canali sono automatici, questo Ã¨ semi-manuale per principio etico autorialitÃ . Stesso pattern applicabile in futuro per altri profili personali soci se richiesto.
---
# ðŸ‘¤ Skill publish-linkedin-daniele â€” Pubblicazione SEMI-MANUALE LinkedIn personale Daniele

> **Etica voce personale = click finale di Daniele. Plugin prepara, Daniele autorizza. Mai bypassare.**

---

## 1. Quando triggera

- Programmata da calendario editoriale ogni volta che un post LinkedIn Daniele Ã¨ in stato `Approvato CEO âœ…` (Daniele Ã¨ il CEO, "approvato CEO" Ã¨ esplicito qui)
- Slot ricorrente settimanale: lun 08:00 (Pillar 2 Voce CEO always-on) + 1 slot rotante mid-week (pillar di mese)
- Invocata on-demand per post autoriali ad-hoc richiesti da Daniele
- Mai trigger se kill switch `config/AUTOMAZIONE_ATTIVA = false`
- Mai trigger se Crisis mode o Vacation mode totale attivo

Tempo target di esecuzione: **2-5 minuti** preparazione + tempo umano di Daniele per rileggere e cliccare (variabile, tipicamente 5-30 min).

---

## 2. Decisione etica del CEO (Brand Book v1.2 + decisione 2026-05-16)

> **"La voce personale del CEO richiede sempre un click finale del CEO. Non per controllo dell'output (la skill content-linkedin-post-daniele Ã¨ giÃ  stata approvata in fase di scrittura), ma per principio di paternitÃ : ciÃ² che esce a mio nome lo pubblico io, anche se Ã¨ scritto dal Marketing Manager."**
> â€” CEO Daniele Simonini, decisione 2026-05-16

Questa skill **NON automatizza la pubblicazione finale**. Automatizza tutto il pre-publish (preparazione, gate-doppio, drift check, apertura composer), MA il click "Pubblica" Ã¨ di Daniele.

In caso di indisponibilitÃ  prolungata di Daniele (>48h):
- Sistema di rinvio automatico al lun successivo (Pillar 2 always-on tollera 1 slot saltato/mese)
- Notifica MM "post Daniele in pending da >48h" via Friday Email Protocol sez. D
- Mai pubblicazione delegata ad altri soci a nome di Daniele (Brand Book v1.2 sez. 7 â€” no testimonial/firma senza consenso esplicito persona-per-persona)

---

## 3. Output finale atteso

**Log entry** in `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`:

```markdown
## Pubblicazione 2026-XX-XX HH:MM â€” LinkedIn Daniele Simonini

- **Skill chiamante**: advisory-plus:publish-linkedin-daniele
- **ModalitÃ **: SEMI-MANUALE (click finale di Daniele)
- **Post source**: Output_approvati/02_LinkedIn/2026-XX-XX_LI-Daniele_[tema]_[variante].md
- **Pillar**: P[N] [Nome]
- **Voce**: [Voce CEO autoriale / Spiegato Facile / Analisi / Caso Reale]
- **Compliance check T-30min**: ðŸŸ¢ (drift check OK)
- **Composer aperto Chrome MCP**: HH:MM
- **Notifica inviata a Daniele**: HH:MM (email/WhatsApp utility)
- **Daniele click "Pubblica"**: HH:MM (T+X min)
- **Permalink**: https://www.linkedin.com/posts/daniele-simonini_[slug]-activity-[ID]
- **Screenshot**: 04_Risorse/_log_screenshots/LI-daniele_[YYYY-MM-DD]_HHMM.png
- **Stato calendario editoriale**: aggiornato da `Programmato` â†’ `Pubblicato ðŸŸ¢`
- **Ratio firma 80/20 aggiornato**: [N post Daniele / N post altri soci nel mese]
- **Tetto Badvisor cumulato**: [N% mensile Â· in range â‰¤20%]
- **Eventuali avvisi**: [nessuno | pending Daniele >X min | rinvio applicato]
```

---

## 4. Flusso semi-manuale (passo-passo)

### Step 1 â€” Pre-publish check (T-30min, automatico)
Come `publish-linkedin-pagina` sez. 4 ma con verifiche specifiche profilo personale:
- âœ… Ratio firma 80/20: questo post incrementa quota Daniele â†’ verifica che non sbordi >85%
- âœ… Tetto Badvisor mensile cumulato (se voce Badvisor su Daniele â†’ conta nella quota 20%)
- âœ… Firma "Agent, Admin & Advisor" verificata (mai "CEO" â€” Brand Book v1.2 sez. 1 + Compagine Voci)
- âœ… Tag @Advisory+ presente massimo 1 volta in chiusura (Brand Book v1.2 sez. 5)
- âœ… NO visual allegato (LI personale premia dwell-time testo nudo â€” Brand Book v1.2 sez. 5)
- âœ… NO claim ðŸ”´ vietati (compliance gate-doppio standard)
- âœ… Pillar 2 Voce CEO always-on rispettato (settimanale)
- ðŸŸ¢/ðŸŸ¡/ðŸ”´ esito gate-doppio

### Step 2 â€” Apertura Chrome MCP su LinkedIn (T-0, immediata)
Skill apre browser via Claude in Chrome MCP:
```
mcp__claude-in-chrome__navigate(url: "https://www.linkedin.com/feed/?focusInput=composer", tabId: [tab_id])
```
Daniele deve essere giÃ  loggato sul suo browser (Cowork riusa la sessione esistente).

### Step 3 â€” Compilazione composer (automatica)
```
mcp__claude-in-chrome__form_input(ref: [composer_textarea_ref], value: [post_payload], tabId: ...)
```
Payload include: testo completo + hashtag in coda + nessun visual (LI personale puro testo).

### Step 4 â€” NO click pubblica + notifica Daniele
Skill **NON clicca** il bottone "Pubblica" o "Post". Si ferma con composer aperto.

Invia notifica Daniele (canale di default email Â· canale alternativo WhatsApp utility):
```
Subject: [Plugin] Post LinkedIn pronto per pubblicazione
Body:
Ciao Daniele,
ho preparato il tuo post LinkedIn settimanale (Pillar [N]).
Il composer Ã¨ aperto nel tuo Chrome.
Rileggilo, fai eventuali modifiche minime, poi clicca "Pubblica" quando ti va bene.
Se NON vuoi pubblicarlo: chiudi il composer e rispondi "STOP" a questa email.
Se vuoi rinviarlo: rispondi "RINVIA [data]".
Anteprima del post:
[primi 200 char]
Pillar: [N]
Voce: [...]
Compliance check: ðŸŸ¢
Ratio 80/20 corrente: [Daniele X% / altri Y%]
```

### Step 5 â€” Polling permalink (background, max 60 min)
Skill esegue polling Chrome MCP ogni 5 minuti sul profilo di Daniele per rilevare nuovo post:
```
mcp__claude-in-chrome__find(query: "ultimo post di Daniele Simonini", tabId: ...)
```
Confronta timestamp/contenuto con quello del payload.

### Step 6 â€” Permalink rilevato â†’ log + screenshot
Quando skill rileva post live (entro 60 min dall'apertura composer):
- Estrae permalink
- Esegue screenshot via Chrome MCP
- Salva in `/04_Risorse/_log_screenshots/`
- Aggiorna log + calendario editoriale (stato Pubblicato)

### Step 7 â€” Timeout 60 min â†’ escalation
Se entro 60 min Daniele non ha cliccato:
- Skill chiude composer senza pubblicare (per evitare residui)
- Aggiorna calendario editoriale: stato `Pending Daniele`
- Notifica MM: "Post Daniele pending â€” verifica disponibilitÃ "
- Auto-rinvio al prossimo slot settimanale Pillar 2 (lun successivo) se non c'Ã¨ risposta entro 48h

### Step 8 â€” Daniele risponde STOP â†’ archivio
Daniele risponde "STOP" â†’ calendario stato `Bloccato ðŸ”´` + post archiviato in `/99_Archivio/post_LI_daniele_non_pubblicati/[YYYY-MM-DD]_[tema].md` per audit + revisione futura voce/tema.

### Step 9 â€” Daniele risponde RINVIA [data] â†’ reschedule
Calendario stato `Rinviato ðŸ”„` + nuova data + ragione documentata.

---

## 5. Casi particolari

### Voce Badvisor su Daniele
Ammessa entro tetto 20% mensile (cumulato su tutti i canali). Skill verifica:
- Quota Badvisor mensile prima dell'invocazione
- Se >18% (warning) â†’ notifica MM + scelta MM di procedere o no
- Se >20% (hard) â†’ blocco + Compliance Officer riformulazione voce alternativa

### Voce Caso Reale su Daniele profilo personale
Disclaimer "Caso reale, nomi di fantasia" sempre obbligatorio (Brand Book v1.2 sez. 4). Compliance gate-doppio verifica presenza.

### Pillar 2 always-on saltato (Daniele indisponibile)
Pillar 2 Voce CEO Ã¨ always-on settimanale. Se Daniele non clicca entro 48h â†’ auto-rinvio al lun successivo. Massimo 1 slot saltato/mese (Brand Book v1.2 sez. 6 â€” always-on resta always-on, sotto 3 mesi di salti consecutivi flag MM per revisione).

### Big bet con OK CEO esplicito
Daniele Ã¨ il CEO, "big bet" qui significa post che ha richiesto specifica direzione strategica del CEO durante il drafting. Stato calendario `Approvato CEO âœ…` con doppia approvazione (CEO come strategia + CEO come pubblicatore). Flusso identico, due livelli di verifica.

### Ratio 80/20 fuori range
- Se Daniele >85% nei 12 mesi rolling â†’ notifica MM ridurre cadenza Daniele e aumentare altri soci
- Se Daniele <75% nei 12 mesi rolling â†’ notifica MM aumentare cadenza Daniele Pillar 2 always-on potrebbe essere stato sospeso troppo

### Pubblicazione richiesta in finestra Vacation
Vacation mode parziale = Pillar 2 always-on continua se Daniele Ã¨ disponibile per click. Se Daniele in vacation totale â†’ modalitÃ  "Daniele OOO" attiva, post in calendario rinviati al rientro.

---

## 6. KPI publish-linkedin-daniele (riferimento data-kpi-channel-baseline)

| KPI | Target a regime |
|---|---|
| Tasso di successo pubblicazione (Daniele clicca entro 60min) | â‰¥80% |
| Latency tra composer aperto e click Daniele | <30 min mediana |
| Slot Pillar 2 saltati/mese | <1 |
| Ratio 80/20 firma rispettato (range 75-85%) | 100% mensile |
| Tetto Badvisor 20% mensile | rispettato 100% |
| Compliance drift check fallito | <1% |

---

## 7. Compliance & sicurezza

âœ… **Mai pubblicazione automatica** del post finale (decisione etica CEO 2026-05-16)
âœ… **Mai delega ad altri soci** firma Daniele
âœ… **Doppio gate Compliance** (scrittura + drift T-30min)
âœ… **Screenshot + permalink** post-publish
âœ… **Ratio 80/20 monitoraggio** continuo
âœ… **Tetto Badvisor 20%** verifica cumulata
âœ… **Firma "Agent, Admin & Advisor"** mai "CEO" (Brand Book v1.2 sez. 1)
âœ… **Tag @Advisory+ max 1 volta** in chiusura post
âœ… **NO visual allegato** (testo nudo premia LI personale)
âœ… **Kill switch** rispettato
âœ… **GDPR**: nessun dato personale di terzi senza consenso

âŒ **Mai**:
- Pubblicazione automatica finale
- Firma di Daniele su contenuti generati senza sua review
- Bypass del click finale "perchÃ© Daniele Ã¨ in viaggio"
- Auto-rinvio >30 giorni (oltre = revisione MM)
- Pubblicazione di post Daniele su Pagina brand confondendo i livelli
- Voci non autoriali (mai Spiegato Facile generico senza personalizzazione Daniele)
- Doppia pubblicazione (Daniele clicca â†’ skill non ri-clicca mai)

---

## 8. Logica di esecuzione â€” passo-passo (riassunta)

1. Trigger schedulato T-30min da calendario editoriale
2. Pre-publish check (sez. 4 step 1) â†’ ðŸŸ¢/ðŸŸ¡/ðŸ”´
3. Se ðŸŸ¢: Chrome MCP apre LinkedIn composer + compila payload (sez. 4 step 2-3)
4. Notifica Daniele (sez. 4 step 4)
5. Polling permalink ogni 5 min per 60 min (sez. 4 step 5)
6. Rilevamento â†’ log + screenshot + calendario update (sez. 4 step 6)
7. Se timeout 60min: escalation + auto-rinvio (sez. 4 step 7)
8. Se STOP da Daniele: archivio (sez. 4 step 8)
9. Se RINVIA: reschedule (sez. 4 step 9)
10. Aggiornare ratio 80/20 + tetto Badvisor + KPI in `Output_approvati/data/`

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pubblicare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 1 identitÃ  Daniele Â· sez. 4 voci Â· sez. 5 strategia LI personali Â· sez. 6 Pillar 2 always-on Â· sez. 7 Compliance Â· sez. 13 MM Decision Authority)
2. `/01_Team/03_Social_Media_Manager.md` + `/01_Team/02_Copywriter.md` + `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` + `config/compagine.json` (firma Daniele "Agent, Admin & Advisor")
4. `config/email.env` (canale notifica Daniele) + `config/AUTOMAZIONE_ATTIVA`
5. Post sorgente in `Output_approvati/02_LinkedIn/`
6. Calendario editoriale + ratio 80/20 + tetto Badvisor mensile cumulati
7. Log pubblicazioni recenti

---

## 10. Cosa NON fare mai

- âŒ **Cliccare "Pubblica"** al posto di Daniele (decisione etica hard)
- âŒ **Firmare con "CEO"** (Brand Book v1.2 sez. 1)
- âŒ **Pubblicare con visual allegato** (testo nudo, Brand Book v1.2 sez. 5)
- âŒ **Tag @Advisory+ piÃ¹ di 1 volta** in chiusura post
- âŒ **Bypass del polling** (mai assumere pubblicato senza verifica permalink)
- âŒ **Auto-rinvio >30 giorni** senza revisione MM
- âŒ **Doppia pubblicazione** (race condition tra polling e click Daniele)
- âŒ **Pubblicazione di big bet** senza doppia approvazione (CEO strategia + CEO click)
- âŒ **Bypass kill switch o Crisis mode**
- âŒ **Profilazione comportamenti di Daniele** ("Daniele clicca sempre dopo 23 min" â€” info utile a MM, mai dato esportato)

---

*SKILL v1.0 â€” advisory-plus:publish-linkedin-daniele â€” Sessione 7 Plugin Build â€” 2026-05-22*

