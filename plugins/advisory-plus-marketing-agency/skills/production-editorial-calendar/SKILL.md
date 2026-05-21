---
name: production-editorial-calendar
description: Gestisce il calendario editoriale settimanale + mensile di Advisory+ (pipeline contenuti su 8 canali Â· slot fissi per canale Â· stato bozza/in-revisione/approvato/programmato/pubblicato Â· scadenze Â· dipendenze cross-canale come repurposing blogâ†’newsletterâ†’LIâ†’IG). Output: file Markdown calendario in `/05_Calendario_editoriale/[YYYY-MM]_calendario.md` + sync bidirezionale con Google Calendar via MCP (Sessione 8 wiring). Trigger: aggiornato dopo ogni piano settimanale (Friday Email Â· strategia-week-fri) e dopo ogni approvazione CEO. Read-write su `/05_Calendario_editoriale/`. Integra con strategia-month-plan come fonte di pillar dominante del mese + rotazione pillar-of-month. Compliance Officer monitora che la pianificazione rispetti tetto Badvisor 20% mensile, regola 45/30/20/5 pillar mix, ratio 80/20 firma personale Daniele.
---
# ðŸ“… Skill production-editorial-calendar â€” Calendario editoriale settimanale + mensile

> **Pipeline 8 canali Â· stato workflow Â· sync Google Calendar MCP Â· monitor tetti Brand Book v1.2.**

---

## 1. Quando triggera

- Invocata da `advisory-plus:strategia-week-fri` ogni venerdÃ¬ 18:00 dopo composizione piano settimanale â†’ aggiorna calendario settimana successiva
- Invocata da `advisory-plus:strategia-month-plan` ultimo venerdÃ¬ del mese â†’ compila calendario mensile completo
- Invocata da `advisory-plus:strategia-week-mon` ogni lunedÃ¬ 06:00 per status digest mattutino (consultazione, read-only sezione)
- Invocata dopo ogni approvazione CEO su singolo contenuto â†’ update stato `approvato`
- Invocata dopo ogni pubblicazione effettiva (hook post-publish, Sessione 7) â†’ update stato `pubblicato` + log permalink
- Invocata on-demand dal MM per riallineamento ad-hoc (rinvii, urgenze, big bets approvati)

Tempo target di esecuzione: **10-20 minuti** per aggiornamento settimanale, **30-45 min** per setup mensile.

---

## 2. Output finale atteso

**File Markdown** in `/05_Calendario_editoriale/[YYYY-MM]_calendario.md`:

```markdown
---
mese: YYYY-MM
versione: vN (incrementale ad ogni aggiornamento)
pillar_dominante_mese: P[N] [Nome]
pillar_background: [P[A], P[B]]
specialty_attiva: [P10/P11/P12 o "nessuna"]
totale_contenuti_pianificati: N
distribuzione_pillar: [P[N]: X% Â· always-on: Y% Â· specialty: Z%]
ratio_firma_daniele: X/100 (target 80/20)
quota_badvisor_mensile: X% (target â‰¤20% Brand Book v1.2)
ultima_modifica: YYYY-MM-DD HH:MM
---

## A. Vista mensile (tabella)

| Data | Giorno | Canale | Formato | Pillar | Voce | Titolo/Tema | Firma | Stato | Compliance | Note |
|---|---|---|---|---|---|---|---|---|---|---|
| 2026-05-21 | Gio 09:00 | LI Pagina | Post brand | P1 | Spiegato Facile | "Differenza tra X e Y" | Brand | ðŸŸ¢ Pubblicato | ðŸŸ¢ | URL: [...] |
| 2026-05-22 | Ven 18:00 | Email | Friday Email | n/a | n/a | Recap settimana | MM | â³ In coda | ðŸŸ¢ | auto |
| 2026-05-23 | Sab 10:00 | LI Daniele | Post personale | P2 | Voce CEO | "IdentitÃ  del consulente" | Daniele | ðŸ“ Bozza | ðŸŸ¡ in check | semi-manuale |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

## B. Vista per canale (8 sezioni)

### B.1 LinkedIn Pagina (target 2-3/sett)
[Lista contenuti del mese su questo canale]

### B.2 LinkedIn Profili Personali (target 8-10/mese aggregato, ratio 80/20)
[...]

### B.3 Instagram (target 3/sett + Stories)
[...]

### B.4 Facebook (target 2/sett)
[...]

### B.5 Blog THE ADVISOR (target 2-3/mese)
[...]

### B.6 Newsletter (target 1/mese + sintesi pillar)
[...]

### B.7 YouTube (target 1-2/mese fase calibrazione giu-lug)
[...]

### B.8 WhatsApp utility
[trigger event-driven, non calendario]

## C. Dashboard tetti Brand Book v1.2

| Vincolo | Target | Stato attuale | Status |
|---|---|---|---|
| Quota Badvisor mensile | â‰¤20% | X% | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Distribuzione 45/30/20/5 (pillar-of-month/always-on/background/specialty) | 45/30/20/5 | XX/XX/XX/XX | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Ratio firma personale (Daniele 80% / altri soci 20%) | 80/20 Â±5% | XX/XX | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Frequenza per canale | Brand Book sez. 5 | rispettato? | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Disclaimer RUI canali che lo richiedono | 100% | XX% | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| AI disclosure (video AI post-launch YouTube) | 100% | XX% | ðŸŸ¢/ðŸŸ¡/ðŸ”´ |

## D. Big bets approvati (mese)

[Lista contenuti "big bets" che hanno richiesto OK esplicito CEO Brand Book v1.2 sez. 13]

## E. Pendenze e dipendenze

[Contenuti in attesa di asset visivo Â· contenuti in attesa Compliance Â· ricorrenze ed eventi]

## F. FestivitÃ  + scadenze IVASS/ANIA/COVIP del mese

[Eventi esterni che impattano la pianificazione]
```

---

## 3. Stati del workflow contenuto

| Stato | Emoji | Descrizione | Owner | Next action |
|---|---|---|---|---|
| Pipeline | ðŸ’¡ | Idea inserita dal MM, non ancora prodotta | MM | Brief alla skill content-* |
| Bozza | ðŸ“ | Contenuto prodotto da skill content-*, in attesa Compliance | Skill | Invoca gate-doppio |
| In revisione | ðŸ” | Compliance check in corso o riformulazione ðŸŸ¡ | Compliance Officer | Decisione ðŸŸ¢/ðŸŸ¡/ðŸ”´ |
| Approvato CEO | âœ… | Big bet o caso speciale con OK CEO esplicito | CEO | Schedulato per pubblicazione |
| Programmato | â³ | In coda di pubblicazione (Brevo/MCP automation) | Plugin automation | Pubblicazione automatica |
| Pubblicato | ðŸŸ¢ | Pubblicato con successo, log + permalink + screenshot | Plugin post-hook | Misurazione KPI |
| Bloccato | ðŸ”´ | Compliance ðŸ”´ o decisione MM/CEO di stop | MM/CEO | Re-design o archiviazione |
| Rinviato | ðŸ”„ | Spostato di X giorni (ragione documentata) | MM | Nuova data nel calendario |
| Archiviato | ðŸ“¦ | Idea non piÃ¹ rilevante, archiviata | MM | Spostamento `99_Archivio/` |

---

## 4. Slot fissi per canale (default Â· personalizzabile da MM)

### LinkedIn Pagina Aziendale
- Mar 09:00 Â· Mer 09:00 Â· Gio 09:00 (2-3 slot/sett, picco engagement B2B)

### LinkedIn Profili Personali (Daniele 80% + altri 20%)
- Daniele: Lun 08:00 (sempre Pillar 2 Voce CEO always-on) + 1 slot rotante mid-week sul pillar di mese
- Altri soci: Mer o Ven 10:00 (su pertinenza pillar â€” Barrella P5/P6, Agostini P9, Fappani P7/P12)

### Instagram
- Mar 11:00 Â· Gio 11:00 Â· Sab 10:00 (3 slot/sett Â· 1 Reel idealmente)
- Stories: ad-hoc, almeno 2-3 set permanenti highlight + 1-2 set ad-hoc/sett (sez. 14 highlight permanenti consolidati Sessione 4)

### Facebook
- Mer 14:00 Â· Sab 10:00 (2 slot/sett, riuso IG)

### Blog THE ADVISOR
- Mar 09:00 Â· Gio 09:00 (1-2 articoli/sett a regime Â· 2-3/mese in fase calibrazione)

### Newsletter
- Ultimo venerdÃ¬ del mese 17:00 (sintesi pillar di mese + always-on)

### YouTube (canale nuovo Â· go-live giugno 2026)
- Mese 1-2 (giu-lug): 1-2 video/mese Â· slot mar mattino quando possibile
- Mese 3+ (ago+): 2-3 video/mese Â· cadenza piÃ¹ regolare

### WhatsApp utility
- Trigger event-driven (scadenze polizze, auguri, novitÃ  contrattuali) â€” non slot calendario

âš ï¸ **Slot personalizzabili** da MM se A/B test su orari rivela pattern diverso (skill `data-ab-test-design`).

---

## 5. Vincoli Brand Book v1.2 da monitorare automaticamente

### 5.1 Tetto Badvisor 20% mensile (decisione CEO 2026-05-17)
La skill conta i contenuti pianificati con voce `badvisor` su totale mensile. Se >18% (warning ðŸŸ¡) o >20% (block ðŸ”´) â†’ notifica MM + suggerimento alternative.

### 5.2 Regola 45/30/20/5 (pillar mix Brand Book v1.2 sez. 6)
- Pillar-of-month dominante: 45% del totale mensile
- Always-on (P1 + P2 + P3): 30%
- Background pillar (altri 2 rotanti): 20%
- Specialty (se attiva quel trimestre): 5-10%

Se distribuzione fuori range â†’ suggerimento riallocazione.

### 5.3 Ratio firma 80/20 (Daniele/altri soci)
- Daniele: ~80% dei contenuti a firma personale
- Altri soci: ~20% combinato (Agostini Â· Barrella Â· Fappani)

Se ratio scende sotto 75/25 o sale sopra 85/15 â†’ notifica per riallineamento.

### 5.4 Frequenza per canale (Brand Book v1.2 sez. 5)
Range minimo-massimo per canale rispettato. Sotto-frequenza segnala canale "morto", sopra-frequenza rischio spam follower.

### 5.5 Disclaimer RUI sui canali che lo richiedono (blog, newsletter, brochure, sito, YouTube descrizione)
Skill verifica che ogni contenuto su questi canali abbia il flag `disclaimer_rui_presente = true` nel frontmatter prima di passare allo stato Approvato.

### 5.6 AI disclosure (video con HeyGen avatar post-launch YouTube)
Verifica flag `ai_disclosure_presente = true` per ogni contenuto video AI.

---

## 6. Sync Google Calendar MCP (Sessione 8 wiring)

### Direzione 1 â€” Plugin â†’ Google Calendar
Ogni contenuto in stato `Programmato` viene creato come evento Google Calendar nel calendario dedicato "Advisory+ Editorial Calendar":
- Titolo evento: `[Canale] [Pillar] Â· [Titolo contenuto]`
- Data/ora: slot pianificato
- Descrizione: link a file Markdown contenuto + voce + firma + stato Compliance
- Color coding: per canale (LinkedIn navy Â· Instagram teal Â· Blog ink Â· Newsletter graphite Â· YouTube ocra)

### Direzione 2 â€” Google Calendar â†’ Plugin
Eventi creati manualmente da CEO/MM su Google Calendar (es. evento fiera, sponsorizzazione) vengono importati come `Big bet` nel calendario editoriale e generano placeholder content brief.

### Sync frequency
- Push: real-time ad ogni cambio stato
- Pull: mattutino 07:00 daily per importare eventi manuali esterni

---

## 7. Cron schedulati legati al calendario

| Cron | Schedule | Azione |
|---|---|---|
| Friday email update | Ven 17:30 | Rigenera calendario settimana successiva |
| Monday status | Lun 06:00 | Pull eventi esterni Google Calendar |
| Pre-publish reminder | T-2h prima pubblicazione | Verifica stato Compliance Â· alert se non Approvato |
| Post-publish log | T+5min dopo pubblicazione | Update stato a Pubblicato Â· log permalink |
| Month closeout | Ultimo gio mese | Snapshot calendario Â· archivio in `/05_Calendario_editoriale/Storico/[YYYY-MM]_chiuso.md` |

---

## 8. Logica di esecuzione â€” passo-passo

1. **Ricevere brief** (skill chiamante Â· MM Â· cron)
2. **Cascata di contesto** (sez. 10)
3. **Determinare modalitÃ **: setup mensile Â· update settimanale Â· update singolo contenuto Â· cron
4. **Lettura calendario corrente** in `/05_Calendario_editoriale/[YYYY-MM]_calendario.md`
5. **Applicare modifiche** secondo modalitÃ :
   - Setup mensile: invoca `strategia/month-plan` via Task â†’ riceve piano mensile completo â†’ popola calendario tabella + viste per canale
   - Update settimanale: integra piano settimana successiva da `strategia/week-fri`
   - Update singolo contenuto: cambia stato + note + permalink se Pubblicato
6. **Verificare vincoli automatici** (sez. 5):
   - Tetto Badvisor 20%
   - Regola 45/30/20/5
   - Ratio firma 80/20
   - Frequenza per canale
   - Disclaimer/AI disclosure flags
7. **Compilare dashboard tetti** (sez. C output)
8. **Identificare pendenze** e dipendenze (sez. E)
9. **Salvare** file aggiornato
10. **Trigger sync Google Calendar** (Sessione 8 MCP wiring) se cambi rilevanti
11. **Notificare MM** se warning su vincoli (ðŸŸ¡) o blocchi (ðŸ”´)

---

## 9. Casi particolari

### Big bet inserito mid-month
- Stato direttamente "Approvato CEO" (skippa pipeline standard)
- Documentato in sez. D Big bets con razionale CEO
- Eventualmente sposta contenuti giÃ  pianificati per fare spazio (notifica MM)

### Crisis mode
- Tutto il calendario va in stato "Bloccato" temporaneamente
- Email alert CEO immediato
- Calendar resta congelato fino a uscita crisis mode

### Vacation mode
- Riduzione automatica frequenza: -50% contenuti always-on, mantieni utility WhatsApp + Friday Email
- Sezione "Vacation mode attivo dal [data] al [data]" in cima al calendario

### Rinvio contenuto
- Cambio stato a "Rinviato" + nuova data + ragione (1-2 righe)
- Se >7gg di rinvio: revisione MM se pertinenza tematica ancora valida
- Se >30gg: probabile archiviazione

### Specialty drop (P10/P11/P12) attivo nel trimestre
- 3-4 settimane consecutive con specialty come pillar background secondario (5-10%)
- Calendario evidenzia "Drop specialty [P[N]] in corso" in sez. C

---

## 10. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di aggiornare calendario, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 5 strategia canali Â· sez. 6 Pillar Map Â· sez. 7 Compliance Â· sez. 13 MM Decision Authority)
2. `/01_Team/00_Marketing_Manager.md` + `/01_Team/09_Content_Producer.md`
3. `config/brand.json` (canali, frequenze, voci, tetti) + `config/pillars-of-month.json`
4. `/05_Calendario_editoriale/[YYYY-MM]_calendario.md` corrente
5. `Output_approvati/` di tutte le chat operative del mese (per stato contenuti)
6. Eventuali eventi Google Calendar manuali importati
7. Il brief operativo del MM o cron schedulato

---

## 11. Cosa NON fare mai

- âŒ **Spostare contenuti senza notifica MM** (calendario Ã¨ pubblico nel team)
- âŒ **Bypassare vincoli Brand Book** (tetto Badvisor, 45/30/20/5, ratio 80/20) â€” sempre warning prima di proseguire
- âŒ **Pianificare contenuti su canali in vacation mode** completo (ridurre frequenza, non spengere completamente â€” eccezione: kill switch globale)
- âŒ **Marcare Pubblicato senza verifica permalink** (rischio falso positivo nel log)
- âŒ **Cancellare contenuti archiviati** (sempre spostamento `99_Archivio/`, mai delete)
- âŒ **Sync Google Calendar in entrambe le direzioni simultaneamente** (race condition Â· usa push + pull alternati con timestamp)
- âŒ **Modificare slot fissi senza A/B test** che giustifichi
- âŒ **Compilare calendario senza considerare festivitÃ /scadenze IVASS/ANIA/COVIP** del mese (sez. F obbligatoria)

---

*SKILL v1.0 â€” advisory-plus:production-editorial-calendar â€” Sessione 6 Plugin Build â€” 2026-05-21*

