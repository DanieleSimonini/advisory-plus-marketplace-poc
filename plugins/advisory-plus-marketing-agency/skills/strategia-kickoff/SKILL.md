---
name: strategia-kickoff
description: Esegue la cascata di contesto obbligatoria all'apertura di QUALSIASI nuova sessione operativa Cowork nel workspace ClaudeCoWork_TeamMarketing. Legge in ordine README, Brand Book v1.2, persona Marketing Manager (presidente di stanza), personas degli specialisti titolari della chat corrente (in base a Istruzioni_chat.md), Istruzioni_chat.md della chat, Verbale.md per intero (STATO ATTUALE + ultime 2-3 sessioni in cronologia). A lettura completata, conferma il caricamento con un report sintetico di 3 bullet ("Stato sintetico") + "Pronto." e attende le istruzioni operative del CEO o il prompt operativo dal Comitato di Direzione. Triggera all'apertura di ogni nuova chat Cowork del workspace Advisory+ (Comitato di Direzione + 9 chat operative + chat temporanee come Plugin Build). Senza kickoff, la sessione riparte cieca e perde la memoria del sistema.
---
# ðŸš€ Skill kickoff â€” Apertura sessione Cowork Advisory+

> **La prima cosa che fa Cowork in ogni sessione, prima di qualsiasi altra azione. Senza kickoff, niente memoria di sistema.**

---

## 1. Quando triggera

- **Sempre** all'apertura di una nuova sessione Cowork nel workspace `ClaudeCoWork_TeamMarketing`
- **Sempre** quando il CEO incolla un prompt operativo in una chat (sia Comitato sia chat operativa o temporanea)
- **Sempre** quando il MM apre autonomamente una sessione per esecuzione di un'automazione schedulata (week-fri, week-mon, month-plan)

Se non triggera o viene saltato, il Marketing Manager risponderÃ  cieco rispetto al contesto di workspace e di chat â†’ output potenzialmente off-brand, off-strategia, off-compliance.

---

## 2. Output finale atteso

Una sola risposta, esattamente in questa forma:

```
Contesto chat [NomeChat] caricato.
Sessione corrente: [N] di [Totale se applicabile].
Stato sintetico:
- [bullet 1 â€” pendenza/decisione piÃ¹ rilevante]
- [bullet 2 â€” ultimo deliverable approvato o prossimo passo pianificato]
- [bullet 3 â€” eventuale criticitÃ  o anticipo/ritardo su roadmap]
Pronto.
```

Senza preamboli. Senza commenti aggiuntivi. Senza emoji decorative.

**Solo dopo questa conferma**, Cowork attende le istruzioni del CEO o il prompt operativo successivo.

---

## 3. Cascata di contesto â€” ordine di lettura

L'ordine Ã¨ **obbligatorio e non riordinabile**. PiÃ¹ si scende, piÃ¹ il contesto si stringe sulla chat specifica.

### Livello 1 â€” Workspace (sempre)
1. `/00_README.md` â€” regole generali del workspace, gerarchia, naming, struttura cartelle
2. `/00_Brand_Book_v1.2.md` â€” identitÃ , posizionamento nazionale, 5 pilastri, Pillar Map 12, 4 voci editoriali, compliance, design system, MM Decision Authority, AI Act

### Livello 2 â€” Team (sempre Marketing Manager + titolari di stanza)
3. `/01_Team/00_Marketing_Manager.md` â€” sempre, Ã¨ presidente di ogni stanza
4. File personas dei **titolari di stanza** della chat corrente (mappa nel README sez. 5)

| Chat | Titolari da leggere |
|---|---|
| 02 Comitato di Direzione | solo Marketing Manager |
| 03/01 Strategia | Brand Strategist + Data Analyst + SEO Specialist |
| 03/02 LinkedIn | Copywriter + Social Media Manager |
| 03/03 Instagram & Facebook | Social Media Manager + Art Director |
| 03/04 Blog THE ADVISOR | Copywriter + SEO Specialist |
| 03/05 Brochure & Stampa | Art Director + Copywriter |
| 03/06 Email & CRM | CRM & Lead Manager + Copywriter |
| 03/07 WhatsApp Business | Copywriter + Compliance Officer |
| 03/08 Performance & Analytics | Data Analyst |
| 03/09 Brand Identity | Brand Strategist + Art Director |
| 03/10 Plugin Build (temporanea) | Brand Strategist + Compliance Officer |

### Livello 3 â€” Chat (sempre)
5. `Istruzioni_chat.md` della chat corrente â€” prompt standard di apertura, scope, regole locali, output naming
6. `Verbale.md` della chat corrente â€” **STATO ATTUALE per intero** + **ultime 2-3 sessioni della cronologia in dettaglio** + titoli delle sessioni piÃ¹ vecchie (come indice)

### Livello 4 â€” Specifico (condizionale)
- Se Istruzioni_chat.md cita documenti fondativi (es. architettura sistema, scheda strategica) â†’ leggerli
- Se il brief operativo cita Output_approvati passati â†’ leggerli

---

## 4. Costruzione dei 3 bullet "Stato sintetico"

I 3 bullet devono coprire:

1. **Decisioni o pendenze piÃ¹ rilevanti** dal STATO ATTUALE del Verbale
2. **Ultimo deliverable approvato** o **prossimo passo pianificato** (con data se disponibile)
3. **Eventuali criticitÃ , anticipi o ritardi** rispetto alla roadmap (se nessuno â†’ secondo bullet di stato)

Ogni bullet: max 2-3 righe, tono operativo, niente fronzoli.

---

## 5. Casi particolari

### Prima sessione di una chat nuova (Verbale.md non esiste o Ã¨ vuoto)
- Leggi tutto il resto della cascata
- Nei 3 bullet: "Chat di nuova apertura Â· nessuna sessione precedente Â· pronto per setup iniziale"

### Sessione automatizzata (week-fri/week-mon/month-plan)
- Skipped output verbale visibile (il MM non risponde a un umano, esegue un task)
- Ma la cascata di contesto va comunque eseguita per qualitÃ  di output

### Sessione di chat temporanea (es. Plugin Build chat 10)
- Comprende numero progressivo "Sessione corrente: N di Totale"
- Bullet 1 = ultimo blocco completato, bullet 2 = prossimo blocco, bullet 3 = scostamento da roadmap se rilevante

### Sessione del Comitato di Direzione (chat 02)
- Solo Marketing Manager come persona
- Leggere **TUTTI** i Verbale.md delle chat operative? No: solo STATO ATTUALE di ciascuna chat operativa (lettura veloce indice)

---

## 6. Cosa NON fare mai

- âŒ Saltare la cascata "perchÃ© sembra giÃ  tutto chiaro" (Ã¨ la causa #1 di drift cross-sessione)
- âŒ Rispondere a una domanda del CEO PRIMA di aver completato la cascata
- âŒ Aggiungere commenti, riassunti estesi o opinioni alla conferma di apertura (il formato Ã¨ rigido: solo "Contesto caricato. Pronto." + 3 bullet)
- âŒ Confondere i 3 bullet con un report generale (sono solo "memoria operativa di apertura")
- âŒ Leggere Verbale.md "in diagonale" o saltare le ultime sessioni â€” quelle hanno il contesto fresco
- âŒ Auto-decidere di leggere personas extra non titolari della chat (rallenta inutilmente)

---

## 7. Tempo target di esecuzione

Cascata + sintesi: **<90 secondi**. Se la chat ha un Verbale molto lungo (>20 sessioni), il tempo puÃ² salire a 2 minuti â€” accettabile.

---

## 8. Cascata di contesto obbligatoria (meta-rule)

Questa skill **definisce** la cascata. Se invocata, applica la sez. 3 di questo file. Punto.

In casi rarissimi (chat in stato corrotto, file mancanti), segnala al CEO: "Contesto NON completo. Mancano: [file X, Y]. Procedo comunque con quanto leggibile o blocco?" e attendi istruzione esplicita.

---

*SKILL v1.0 â€” advisory-plus:kickoff â€” Sessione 2 Plugin Build â€” 2026-05-17*

