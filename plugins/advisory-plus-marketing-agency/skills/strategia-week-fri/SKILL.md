---
name: strategia-week-fri
description: Compone il Friday Email Protocol di Advisory+ (Brand Book v1.2 sez. 13.5 — MM Decision Authority Framework) ogni venerdì alle 18:00, in automatico via scheduled task post-deploy. L'email è il canale settimanale principale CEO ↔ Plugin nel modello "MM autonomo + silent approval window 48h + veto-by-exception". Composta da 6 sezioni: (A) Recap settimana appena chiusa — pubblicato vs pianificato, top/bottom performer, compliance, KPI cumulati · (B) Piano settimana successiva — 15-20 contenuti per canale, pillar dominante, always-on, ratio 80/20 · (C) Big bets se ce ne sono — max 3, decision esplicita CEO richiesta · (D) Spunti CEO inbox trattati — lista + destinazione · (E) Cheat sheet di risposta — STOP/MODIFICA/RINVIA #N · (F) Punti di esitazione MM — max 3, attivi nei primi 30 giorni Trust Calibration Window (16 mag → 16 giu 2026). Output: Markdown + render HTML per Brevo/SMTP. Triggera ven 18:00 auto + manualmente da MM/CEO via slash command /adv-friday-email.
---
# 📨 Skill week-fri — Friday Email Protocol Advisory+

> **L'email del venerdì 18:00 è il canale settimanale principale CEO ↔ Plugin. Critica nel modello "MM autonomo + silent approval 48h". Brand Book v1.2 sez. 13.5.**

---

## 1. Quando triggera

- **Automatico**: ogni **venerdì alle 18:00** via scheduled task definito in sessione di setup post-deploy plugin v1.1
- **Manuale**: invocata dal MM o dal CEO con slash command `/adv-friday-email` (per anticipare/posticipare per ferie, eventi)
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false` (kill switch) → email solo manuale dal MM o CEO

---

## 2. Output finale atteso

**Una email pronta da inviare** via SMTP (Brevo) con:

- Subject: `Advisory+ · Friday Email · W[NN] · [data] · [N] big bets, [M] punti esitazione`
- Body: Markdown + render HTML
- Allegati: nessuno (tutto inline; eventuali link a Output_approvati/ via path workspace)

Mittente: `marketing@advisoryplus.it`
Destinatario: `commerciale@advisoryplus.it` (alias forwarding ai 4 soci personali — `daniele.simonini@`, `antonio.agostini@`, `alberto.fappani@`, `michele.barrella@`). Configurato in `config/email.env`.

> **NOTA addendum v1.3 (2026-05-28):** destinatario cambiato da `amministrazione@advisoryplus.it` (solo CEO) a `commerciale@advisoryplus.it` (forwarding ai 4 soci, trasparenza piena del piano editoriale). Autorita decisionale resta interamente al CEO via parser ristretto (vedi skill `strategia-week-mon`). File canonico: `03_Aree_di_lavoro/09_Brand_Identity/Output_approvati/2026-05-28_brand_book_addendum_v1.3_friday_email_protocol_evoluto.md`.

---

## 3. Sei sezioni dell'email — struttura fissa

### Sezione A — Recap settimana appena chiusa (5 righe)

Compatta. Una riga per voce:

```
A. RECAP SETTIMANA W[NN] (dal lun [data] a dom [data])
• Pubblicato: [N]/[M pianificati] contenuti — [%]
• Top performer: [Titolo/canale] — [metrica sintetica]
• Bottom: [Titolo/canale] — [perché secondo MM/Data Analyst]
• Compliance: [N] 🟢 · [M] 🟡 risolti · [K] 🔴 bloccati e perché
• KPI cumulati mese: [reach/eng/CTR/leads/iscritti newsletter — solo se dati disponibili via MCP Supermetrics]
```

Se i KPI non sono ancora disponibili (Onda 3 non ancora completa), scrivi: "KPI: in attesa MCP Supermetrics (Onda 3)".

### Sezione B — Piano settimana successiva (lun-dom)

Tabella o lista strutturata con **15-20 contenuti** distribuiti per canale:

```
B. PIANO W[NN+1] (lun [data] - dom [data])
Pillar dominante: [P# Nome] (45% peso)
Pillar background: [P# Nome] (20%) + [P# Nome] (20%)
Always-on: P1 Educazione · P2 Voce CEO · P3 News
Specialty attiva: [Pillar 10/11/12 se attivo] o "nessuna"
Ratio 80/20 Daniele/altri soci: [verificato OK / da ribilanciare]

#   Data       Ora    Canale            Pillar  Voce              Tema sintetico              Firma
1   Lun [d]    08:00  LinkedIn brand    P1      Spiegato Facile   [tema]                       brand
2   Lun [d]    12:00  Instagram         P4      Caso Reale        [tema]                       brand
3   Lun [d]    18:00  LinkedIn Daniele  P2      Badvisor          [tema]                       Daniele
...
```

Coerente con `config/pillars-of-month.json` + `config/brand.json` frequenze per canale.

### Sezione C — Big bets (max 3 punti)

Solo se ce ne sono. Una big bet è una decisione che richiede **OK esplicito CEO**:
- Nuovo pillar (lancio non in roadmap)
- Campagna con budget >€300
- Crisis comms (sinistro, reputazione, mandataria)
- Post sul profilo personale Daniele Simonini con taglio fuori-standard
- Contenuto 🟡 borderline Compliance dove MM non si sente di decidere da solo

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

### Sezione D — Spunti CEO inbox trattati

Lista degli spunti che il CEO ha lasciato nel canale `Spunti_CEO.md` o via email durante la settimana, e dove sono atterrati:

```
D. SPUNTI CEO TRATTATI

• [Data spunto] [Spunto sintetico] → [Esito: pianificato in W[N], pillar P#, canale X, content #N del piano B]
• [Data spunto] [Spunto sintetico] → [Esito: trattato come big bet C#N — richiede tua decisione]
• [Data spunto] [Spunto sintetico] → [Esito: scartato/rinviato perché [motivo breve]]
```

Se zero spunti: "D. SPUNTI CEO: nessuno nuovo questa settimana."

### Sezione E — Cheat sheet di risposta CEO

Promemoria fisso per il CEO sulla sintassi di risposta:

```
E. CHEAT SHEET RISPOSTA

Subject email speciali:
• "STOP TUTTO" — kill switch globale immediato (tutto in pausa)
• "MODALITÀ FERIE [data fine]" — solo always-on minimi
• "MODALITÀ CRISI" — pausa pubblicazione, solo MM presidia

Reply al piano B / big bets:
• "STOP #N" — blocca contenuto/big bet #N
• "MODIFICA #N: [istruzione]" — modifica con istruzione esplicita
• "RINVIA #N a W[NN+X]" — sposta a settimana successiva

Silent approval window: 48h. Se nessuna reply entro lun 06:00, MM procede col piano da lun 09:00.
```

### Sezione F — Punti di esitazione MM (Trust Calibration Window — primi 30 gg)

Attivo dal **16 maggio 2026** al **16 giugno 2026**. Dopo 16 giugno, se CEO ha vetato <10% → modello validato, sezione F diventa opzionale.

Max 3 punti. Format:

```
F. PUNTI DI ESITAZIONE MM (Trust Calibration — gg [N]/30)

#1 [Decisione presa] · [Perché ho esitato] · [Cosa pensa CEO?]
#2 ...
#3 ...
```

Se zero esitazioni: "F. ESITAZIONI: nessuna questa settimana — MM in modalità autonoma piena."

---

## 4. Logica di costruzione — passo-passo

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
- **Lun 06:00** → skill `advisory-plus:week-mon` legge eventuali reply e applica modifiche/stop/rinvii prima della pubblicazione lun 09:00

---

## 6. Casi particolari

### Modalità Ferie attiva
- Skip Friday Email standard
- Invia solo email essenziale: "Advisory+ in Modalità Ferie fino al [data]. Always-on minimo (P1 Educazione 1 post/sett). Nessuna decisione richiesta."

### Modalità Crisi attiva
- Skip Friday Email standard
- Email manuale del MM: "Crisis mode. MM presidia. Tutto bloccato eccetto comunicazioni di crisi (separate)."

### Plugin in stato AUTOMAZIONE_ATTIVA = false (kill switch)
- Skip auto-send
- MM produce solo bozza Markdown in `/05_Calendario_editoriale/Friday_emails/[YYYY-MM-DD]_friday_DRAFT.md`
- Notifica via WhatsApp/email manuale al CEO

### Big bet di emergenza in settimana
- Non aspettare il venerdì
- Email "Big bet urgente fuori-ciclo" subito, con stessa logica sezione C

---

## 7. Cosa NON fare mai

- ❌ **Inventare KPI** se MCP Supermetrics non risponde — scrivere "in attesa" è meglio di un numero inventato
- ❌ **Saltare la sezione C** anche quando zero big bets (lasciare frase esplicita)
- ❌ **Pianificare contenuti senza compliance check** (almeno gate 1 prima dell'invio)
- ❌ **Sovrastimare la complessità**: l'email deve essere leggibile in <5 minuti dal CEO
- ❌ **Aggiungere allegati pesanti**: tutto inline, link al workspace per dettagli
- ❌ **Inviare oltre le 18:30** senza notifica preventiva al CEO
- ❌ **Modificare il formato cheat sheet sez. E** (deve essere stabile per memoria muscolare CEO)
- ❌ **Lasciare sez. F vuota** in Trust Calibration Window (sostituire con "nessuna" esplicito)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di comporre, leggi in ordine:

1. `/00_README.md`
2. `/00_Brand_Book_v1.2.md` (sez. 13 MM Decision Authority · sez. 13.5 Friday Email Protocol · NOTA addendum v1.3)
3. `/01_Team/00_Marketing_Manager.md`
4. `/02_Comitato_Direzione/Verbale.md` (STATO ATTUALE)
5. `/03_Aree_di_lavoro/09_Brand_Identity/Output_approvati/2026-05-28_brand_book_addendum_v1.3_friday_email_protocol_evoluto.md` (riferimento normativo destinatario `commerciale@` + parser autorità)
6. `/05_Calendario_editoriale/[YYYY-MM]_*.md`
7. `/05_Calendario_editoriale/Log_pubblicati/[YYYY-MM]_log.md`
8. `/05_Calendario_editoriale/Spunti_CEO.md`
9. `config/pillars-of-month.json` · `config/brand.json` · `config/compagine.json` · `config/AUTOMAZIONE_ATTIVA` · `config/email.env`

---

*Plugin v1.1.8 — SKILL v1.1 advisory-plus:week-fri — Sessione 2 Plugin Build 2026-05-17 · cascata addendum v1.3 + ricostruzione sez. 8 Sessione 24 2026-05-28*
