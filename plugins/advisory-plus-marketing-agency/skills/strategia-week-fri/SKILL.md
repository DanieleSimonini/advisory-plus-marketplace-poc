---
name: strategia-week-fri
description: Compone il Friday Email Protocol di Advisory+ (Brand Book v1.2 sez. 13.5 â€” MM Decision Authority Framework) ogni venerdÃ¬ alle 18:00, in automatico via scheduled task post-deploy. L'email Ã¨ il canale settimanale principale CEO â†” Plugin nel modello "MM autonomo + silent approval window 48h + veto-by-exception". Composta da 6 sezioni: (A) Recap settimana appena chiusa â€” pubblicato vs pianificato, top/bottom performer, compliance, KPI cumulati Â· (B) Piano settimana successiva â€” 15-20 contenuti per canale, pillar dominante, always-on, ratio 80/20 Â· (C) Big bets se ce ne sono â€” max 3, decision esplicita CEO richiesta Â· (D) Spunti CEO inbox trattati â€” lista + destinazione Â· (E) Cheat sheet di risposta â€” STOP/MODIFICA/RINVIA #N Â· (F) Punti di esitazione MM â€” max 3, attivi nei primi 30 giorni Trust Calibration Window (16 mag â†’ 16 giu 2026). Output: Markdown + render HTML per Brevo/SMTP. Triggera ven 18:00 auto + manualmente da MM/CEO via slash command /adv-friday-email.
---
# ðŸ“¨ Skill week-fri â€” Friday Email Protocol Advisory+

> **L'email del venerdÃ¬ 18:00 Ã¨ il canale settimanale principale CEO â†” Plugin. Critica nel modello "MM autonomo + silent approval 48h". Brand Book v1.2 sez. 13.5.**

---

## 1. Quando triggera

- **Automatico**: ogni **venerdÃ¬ alle 18:00** via scheduled task definito in sessione di setup post-deploy plugin v1.1
- **Manuale**: invocata dal MM o dal CEO con slash command `/adv-friday-email` (per anticipare/posticipare per ferie, eventi)
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false` (kill switch) â†’ email solo manuale dal MM o CEO

---

## 2. Output finale atteso

**Una email pronta da inviare** all'indirizzo del CEO via SMTP (Brevo) con:

- Subject: `Advisory+ Â· Friday Email Â· W[NN] Â· [data] Â· [N] big bets, [M] punti esitazione`
- Body: Markdown + render HTML
- Allegati: nessuno (tutto inline; eventuali link a Output_approvati/ via path workspace)

Mittente: `marketing@advisoryplus.it` (configurato in `config/email.env`).

---

## 3. Sei sezioni dell'email â€” struttura fissa

### Sezione A â€” Recap settimana appena chiusa (5 righe)

Compatta. Una riga per voce:

```
A. RECAP SETTIMANA W[NN] (dal lun [data] a dom [data])
â€¢ Pubblicato: [N]/[M pianificati] contenuti â€” [%]
â€¢ Top performer: [Titolo/canale] â€” [metrica sintetica]
â€¢ Bottom: [Titolo/canale] â€” [perchÃ© secondo MM/Data Analyst]
â€¢ Compliance: [N] ðŸŸ¢ Â· [M] ðŸŸ¡ risolti Â· [K] ðŸ”´ bloccati e perchÃ©
â€¢ KPI cumulati mese: [reach/eng/CTR/leads/iscritti newsletter â€” solo se dati disponibili via MCP Supermetrics]
```

Se i KPI non sono ancora disponibili (Onda 3 non ancora completa), scrivi: "KPI: in attesa MCP Supermetrics (Onda 3)".

### Sezione B â€” Piano settimana successiva (lun-dom)

Tabella o lista strutturata con **15-20 contenuti** distribuiti per canale:

```
B. PIANO W[NN+1] (lun [data] - dom [data])
Pillar dominante: [P# Nome] (45% peso)
Pillar background: [P# Nome] (20%) + [P# Nome] (20%)
Always-on: P1 Educazione Â· P2 Voce CEO Â· P3 News
Specialty attiva: [Pillar 10/11/12 se attivo] o "nessuna"
Ratio 80/20 Daniele/altri soci: [verificato OK / da ribilanciare]

#   Data       Ora    Canale            Pillar  Voce              Tema sintetico              Firma
1   Lun [d]    08:00  LinkedIn brand    P1      Spiegato Facile   [tema]                       brand
2   Lun [d]    12:00  Instagram         P4      Caso Reale        [tema]                       brand
3   Lun [d]    18:00  LinkedIn Daniele  P2      Badvisor          [tema]                       Daniele
...
```

Coerente con `config/pillars-of-month.json` + `config/brand.json` frequenze per canale.

### Sezione C â€” Big bets (max 3 punti)

Solo se ce ne sono. Una big bet Ã¨ una decisione che richiede **OK esplicito CEO**:
- Nuovo pillar (lancio non in roadmap)
- Campagna con budget >â‚¬300
- Crisis comms (sinistro, reputazione, mandataria)
- Post sul profilo personale Daniele Simonini con taglio fuori-standard
- Contenuto ðŸŸ¡ borderline Compliance dove MM non si sente di decidere da solo

Format:
```
C. BIG BETS (richiedono OK CEO entro lun 06:00)

#1 [Titolo]
   Contesto: [3-5 righe]
   Proposta: [taglio raccomandato dal MM]
   Alternative: [taglio B, taglio C]
   Costo/rischio: [esplicito]
   Raccomandazione MM: [opzione + motivo]
   Risposta richiesta: OK #1 / MODIFICA #1 (specificare) / RIFIUTA #1

#2 ...
```

Se zero big bets, scrivi: "C. BIG BETS: nessuno questa settimana. MM procede in autonomia su tutto il piano B."

### Sezione D â€” Spunti CEO inbox trattati

Lista degli spunti che il CEO ha lasciato nel canale `Spunti_CEO.md` o via email durante la settimana, e dove sono atterrati:

```
D. SPUNTI CEO TRATTATI

â€¢ [Data spunto] [Spunto sintetico] â†’ [Esito: pianificato in W[N], pillar P#, canale X, content #N del piano B]
â€¢ [Data spunto] [Spunto sintetico] â†’ [Esito: trattato come big bet C#N â€” richiede tua decisione]
â€¢ [Data spunto] [Spunto sintetico] â†’ [Esito: scartato/rinviato perchÃ© [motivo breve]]
```

Se zero spunti: "D. SPUNTI CEO: nessuno nuovo questa settimana."

### Sezione E â€” Cheat sheet di risposta CEO

Promemoria fisso per il CEO sulla sintassi di risposta:

```
E. CHEAT SHEET RISPOSTA

Subject email speciali:
â€¢ "STOP TUTTO" â€” kill switch globale immediato (tutto in pausa)
â€¢ "MODALITÃ€ FERIE [data fine]" â€” solo always-on minimi
â€¢ "MODALITÃ€ CRISI" â€” pausa pubblicazione, solo MM presidia

Reply al piano B / big bets:
â€¢ "STOP #N" â€” blocca contenuto/big bet #N
â€¢ "MODIFICA #N: [istruzione]" â€” modifica con istruzione esplicita
â€¢ "RINVIA #N a W[NN+X]" â€” sposta a settimana successiva

Silent approval window: 48h. Se nessuna reply entro lun 06:00, MM procede col piano da lun 09:00.
```

### Sezione F â€” Punti di esitazione MM (Trust Calibration Window â€” primi 30 gg)

Attivo dal **16 maggio 2026** al **16 giugno 2026**. Dopo 16 giugno, se CEO ha vetato <10% â†’ modello validato, sezione F diventa opzionale.

Max 3 punti. Format:

```
F. PUNTI DI ESITAZIONE MM (Trust Calibration â€” gg [N]/30)

#1 [Decisione presa] Â· [PerchÃ© ho esitato] Â· [Cosa pensa CEO?]
#2 ...
#3 ...
```

Se zero esitazioni: "F. ESITAZIONI: nessuna questa settimana â€” MM in modalitÃ  autonoma piena."

---

## 4. Logica di costruzione â€” passo-passo

1. **Eseguire kickoff** (skill `advisory-plus:kickoff`) per caricare contesto workspace
2. **Leggere** `/05_Calendario_editoriale/[YYYY-MM]_*.md` (mese corrente)
3. **Leggere** `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md` (se esiste) per recap effettivo
4. **Leggere** `/05_Calendario_editoriale/Spunti_CEO.md` (canonical input CEO)
5. **Interrogare via Bash** (Onda 3) MCP Supermetrics per KPI settimana (se MCP attivo)
6. **Leggere** `config/pillars-of-month.json` per pillar dominante + background
7. **Leggere** `config/brand.json` per frequenze canale e ratio 80/20
8. **Leggere** `config/compagine.json` per firma assegnata per pillar/canale
9. **Comporre** le 6 sezioni
10. **Invocare** Compliance Officer (skill `advisory-plus:compliance-officer` persona) per check sui big bets e sui contenuti pianificati (almeno gate 1)
11. **Render HTML** + commit Markdown in `/05_Calendario_editoriale/Friday_emails/[YYYY-MM-DD]_friday.md`
12. **Inviare via SMTP** (Brevo, libreria shell) all'email CEO
13. **Log** in `/05_Calendario_editoriale/Friday_emails/log.md` con timestamp invio + esito SMTP

---

## 5. Tempistica

- **Compose**: ~5-7 min (con MCP attivo); ~15 min senza KPI Supermetrics
- **Send**: 18:00 sharp
- **CEO ha 48h** per reply (silent approval window)
- **Lun 06:00** â†’ skill `advisory-plus:week-mon` legge eventuali reply e applica modifiche/stop/rinvii prima della pubblicazione lun 09:00

---

## 6. Casi particolari

### ModalitÃ  Ferie attiva
- Skip Friday Email standard
- Invia solo email essenziale: "Advisory+ in ModalitÃ  Ferie fino al [data]. Always-on minimo (P1 Educazione 1 post/sett). Nessuna decisione richiesta."

### ModalitÃ  Crisi attiva
- Skip Friday Email standard
- Email manuale del MM: "Crisis mode. MM presidia. Tutto bloccato eccetto comunicazioni di crisi (separate)."

### Plugin in stato AUTOMAZIONE_ATTIVA = false (kill switch)
- Skip auto-send
- MM produce solo bozza Markdown in `/05_Calendario_editoriale/Friday_emails/[YYYY-MM-DD]_friday_DRAFT.md`
- Notifica via WhatsApp/email manuale al CEO

### Big bet di emergenza in settimana
- Non aspettare il venerdÃ¬
- Email "Big bet urgente fuori-ciclo" subito, con stessa logica sezione C

---

## 7. Cosa NON fare mai

- âŒ **Inventare KPI** se MCP Supermetrics non risponde â€” scrivere "in attesa" Ã¨ meglio di un numero inventato
- âŒ **Saltare la sezione C** anche quando zero big bets (lasciare frase esplicita)
- âŒ **Pianificare contenuti senza compliance check** (almeno gate 1 prima dell'invio)
- âŒ **Sovrastimare la complessitÃ **: l'email deve essere leggibile in <5 minuti dal CEO
- âŒ **Aggiungere allegati pesanti**: tutto inline, link al workspace per dettagli
- âŒ **Inviare oltre le 18:30** senza notifica preventiva al CEO
- âŒ **Modificare il formato cheat sheet sez. E** (deve essere stabile per memoria muscolare CEO)
- âŒ **Lasciare sez. F vuota** in Trust Calibration Window (sostituire con "nessuna" esplicito)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_README.md`
2. `/00_Brand_Book_v1.2.md` (sez. 13 MM Decision Authority Â· sez. 13.5 Friday Email Protocol)
3. `/01_Team/00_Marketing_Manager.md`
4. `/02_Comitato_Direzione/Verbale.md` (STATO ATTUALE)
5. `/05_Calendario_editoriale/[YYYY-MM]_*.md`
6. `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`
7. `/05_Calendario_editoriale/Spunti_CEO.md`
8. `config/pillars-of-month.json` Â· `config/brand.json` Â· `config/compagine.json` Â· `config/AUTOMAZIONE_ATTIVA`

---

*SKILL v1.0 â€” advisory-plus:week-fri â€” Sessione 2 Plugin Build â€” 2026-05-17*

