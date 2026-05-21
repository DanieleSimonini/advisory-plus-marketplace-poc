---
name: strategia-month-plan
description: Genera il piano editoriale del mese successivo Advisory+ ogni ultimo venerdÃ¬ del mese alle 18:00 via scheduled task. Output: file Markdown in /05_Calendario_editoriale/[YYYY-MM]_[Mese].md con tutti gli slot canale-pillar-voce-firma del mese pianificati. Logica di costruzione: (1) pillar-of-month dominante (output di skill pillar-of-month-setup, 45% peso) Â· (2) 3 always-on attivi sempre (P1 Educazione, P2 Voce CEO, P3 News â€” 30% peso totale) Â· (3) 2 pillar rotanti background (20% peso) Â· (4) Specialty drops se attivi nel mese (5-10% se attivi). Slot canale: LinkedIn brand Ã— frequenza Â· LinkedIn Daniele personale Ã— Â· Instagram Ã— Â· Facebook Ã— Â· YouTube 1-2/mese Â· Blog THE ADVISOR 4-6/mese Â· Newsletter 1/mese. Ratio 80/20 Daniele/altri soci sempre applicato. Considera festivitÃ , scadenze fiscali, scadenze assicurative tipiche del mese. Versionabile e modificabile (il MM puÃ² aggiornarlo settimanalmente via week-fri). Triggera ultimo ven mese 18:00 + manualmente via /adv-month-plan [YYYY-MM].
---
# ðŸ“† Skill month-plan â€” Piano editoriale mensile Advisory+

> **L'architettura mensile. Da qui discende la settimana, dalla settimana il giorno. Brand Book v1.2 sez. 6 Pillar Map + sez. 13 MM Decision Authority.**

---

## 1. Quando triggera

- **Automatico**: ogni **ultimo venerdÃ¬ del mese alle 18:00** via scheduled task
- **Manuale**: `/adv-month-plan [YYYY-MM]` (per ricalcolare un mese esistente o pianificare un mese futuro fuori-ciclo)
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false`

Tempo target di esecuzione: **20-30 minuti** (piÃ¹ lungo di week-fri/mon perchÃ© orizzonte mensile).

---

## 2. Output finale atteso

**Un file Markdown** in `/05_Calendario_editoriale/[YYYY-MM]_[Mese].md` con:

- Header: mese, pillar dominante, pillar background, specialty attive, festivitÃ  rilevanti, scadenze
- Tabella settimana-per-settimana (4-5 settimane del mese) con tutti gli slot
- Sezione "Pipeline ATL" (articoli blog lunghi, video YouTube, newsletter): produzione anticipata necessaria
- Sezione "Coerenza ratio 80/20" (verifica firma soci)
- Sezione "Note del mese" (eventi territoriali, scadenze, opportunitÃ  da intercettare)
- Footer: versione, data ultima modifica, autore (MM o intervento CEO)

**Un riferimento** nel Friday Email della settimana successiva: "Nuovo month-plan pronto in /05_Calendario_editoriale/[YYYY-MM].md".

---

## 3. Logica di costruzione â€” input

### Input strutturali (sempre)
- `/00_Brand_Book_v1.2.md` sez. 6 Pillar Map 12 Â· sez. 9 Compagine voci Â· sez. 13 MM Decision Authority
- `config/brand.json` (frequenze canale, mapping voce-canale-pillar)
- `config/pillars-of-month.json` (pillar dominante + background, output di skill `pillar-of-month-setup`)
- `config/compagine.json` (4 soci + 4 senior advisor + ratio 80/20 + mappa pillarâ†”socio)
- `config/state.json` (modalitÃ  ferie/crisi attive)

### Input dinamici (raccolti runtime)
- **Calendario fissitÃ **: festivitÃ  italiane del mese (sempre), eventuali ponti
- **Scadenze fiscali** del mese: dichiarazione redditi, IMU, bollo auto regionale, scadenze IVASS per intermediari
- **Scadenze assicurative tipiche**: rinnovi auto (giugno-ottobre picco), polizze casa (varia), scadenze previdenziali (fine anno)
- **News di settore programmate**: relazioni annuali ANIA/IVASS/COVIP attese
- **Eventi Advisory+** (se in agenda): open day sedi, webinar, fiere
- **Specialty drops attivi**: se Pillar 10 Mare attivo (giugno-settembre), Pillar 11 Arte (autunno), Pillar 12 Terzo Settore (lancio luglio 2026)
- **Spunti CEO** dal canale `Spunti_CEO.md` pertinenti al mese in pianificazione

---

## 4. Distribuzione pesi pillar (regola del 45/30/20/5)

Su tutti i contenuti del mese:

- **Pillar dominante (P1-P12 a rotazione)**: **45%** del totale
- **3 always-on** (P1 Educazione + P2 Voce CEO + P3 News): **30%** complessivo (10% ciascuno)
- **2 pillar rotanti background**: **20%** complessivo (10% ciascuno)
- **Specialty (P10-P11-P12) se attiva**: **5-10%** (sottrae quota a background o dominante)

### Tabella di esempio per un mese tipico (giugno 2026, pillar dominante P5 LTC, specialty P10 Mare attiva)

| Pillar | Peso target | Contenuti su 60 tot mese |
|---|---|---|
| P5 LTC (dominante) | 45% | 27 |
| P1 Educazione (always-on) | 10% | 6 |
| P2 Voce CEO (always-on) | 10% | 6 |
| P3 News (always-on) | 10% | 6 |
| P4 Famiglia (background) | 8% | 5 |
| P8 Casa (background) | 7% | 4 |
| P10 Mare (specialty attiva) | 10% | 6 |
| **Totale** | **100%** | **60** |

I numeri si adattano alla frequenza effettiva per canale (vedi prossima sez.).

---

## 5. Slot canale â€” frequenza standard

Da `config/brand.json` (sintesi):

| Canale | Frequenza standard | Voci tipiche |
|---|---|---|
| LinkedIn brand Advisory+ | 4-5/sett (~20/mese) | Spiegato Facile + Analisi (news) + Caso Reale |
| LinkedIn Daniele personale (Pillar 2) | 1-2/sett (~6-8/mese) | Voce CEO autoriale (mix Spiegato Facile + Badvisor + Caso Reale + Analisi) |
| Instagram brand | 3-4/sett (~14/mese) | Caso Reale visivi + Spiegato Facile carosello + Badvisor occasionale (Reel) |
| Facebook brand | 3/sett (~12/mese) | Spiegato Facile + Caso Reale + Specialty quando attiva |
| YouTube | 1-2/mese | Explainer Analisi 5-10 min + Case study Caso Reale 4-8 min |
| Blog THE ADVISOR | 1/sett (~4-6/mese) | Spiegato Facile lungo + Analisi lungo + Caso Reale lungo + Specialty deep-dive |
| Newsletter | 1/mese | Recap mensile + 1 articolo originale + sezione "Analisi del mese" |
| Stories IG/FB | quotidiane (~28/mese) | Mix free-form, voci editoriali snelle |
| WhatsApp Business | utility on-demand, mai broadcast acquisitivo | n/a (vedi chat 07) |

**Totale tipico mese (post + caroselli + blog + newsletter, escluse stories)**: ~55-65 contenuti pianificati.

---

## 6. Ratio 80/20 firma â€” verifica automatica

Da `config/compagine.json`:

- **Daniele Simonini (CEO)**: presidio Pillar 2 Voce CEO autoriale â†’ ~5-7 post/mese sul profilo personale
- **Altri 3 soci** (Agostini Â· Barrella Â· Fappani â€” ordine alfabetico): minimo 1 post/mese ciascuno con firma propria su pillar di competenza tematica (mappa in `compagine.json`)
- **4 senior advisor**: presenza occasionale (firma su brochure, eventi, casi reali della loro area)
- **Brand Advisory+** (non firmato): default su LinkedIn brand, IG, FB, blog (firma in calce "Advisory+", non socio specifico)

La skill verifica a fine pianificazione che:
- Daniele non superi il 70% delle firme attribuite (ratio brand-friendly)
- Almeno 1 contenuto/mese per ciascuno degli altri 3 soci
- Senior advisor presenti almeno ogni 2 mesi a rotazione

Se sbilanciato â†’ ribilancia automaticamente o segnala al MM nel Friday Email come big bet.

---

## 7. FestivitÃ  e scadenze â€” calendario di servizio

Per ogni mese, considerare:

### FestivitÃ  italiane standard
- Gennaio: 1 (Capodanno) Â· 6 (Epifania)
- Aprile: Pasqua (variabile) + 25 (Liberazione)
- Maggio: 1 (Lavoratori)
- Giugno: 2 (Repubblica)
- Agosto: 15 (Ferragosto) â€” **ModalitÃ  Ferie da metÃ  luglio a metÃ  agosto raccomandata**
- Novembre: 1 (Tutti i Santi) Â· 4 (Forze Armate)
- Dicembre: 8 (Immacolata) Â· 25 (Natale) Â· 26 (S. Stefano)

### Scadenze assicurative ricorrenti
- Marzo-Maggio: picco rinnovi auto e casa (sensibile per Pillar 4 + 8)
- Giugno: chiusura primo semestre (sensibile per Pillar 9 Imprese reporting)
- Luglio-Agosto: bassa stagione consulenziale â†’ ModalitÃ  Ferie estese
- Ottobre-Novembre: ripresa post-ferie + 1Â° spunto previdenza (Pillar 6 picco)
- Dicembre: 730/redditi anno successivo (Pillar 6 + 9 spunti fiscali)

### Scadenze IVASS/RUI per intermediari (sensibili per Pillar 3 News se diventano notizia)
- Gennaio: scadenza pagamento contributo vigilanza
- Marzo: scadenza adempimenti formazione obbligatoria primo semestre
- Giugno-Luglio: relazione annuale ANIA tipicamente pubblicata
- Ottobre: Relazione annuale IVASS tipicamente
- Novembre: COVIP relazione fondi pensione

Pianificare contenuti Pillar 3 a ridosso delle pubblicazioni annuali â†’ ottima leva voce-analisi.

---

## 8. Pipeline ATL â€” produzione anticipata

Contenuti che richiedono lavorazione anticipata (>1 settimana):

- **Articoli blog 1500-2500p Analisi**: brief 14gg prima della pubblicazione â†’ produzione 7gg prima â†’ pubblicazione
- **Video YouTube explainer 5-10 min**: brief 14gg â†’ produzione (Remotion/HeyGen) 7gg â†’ editing 3gg â†’ pubblicazione
- **Newsletter mensile**: chiusura editoriale 3gg prima invio
- **Brochure stagionali / one-shot**: pipeline 30gg+

Il month-plan flagga questi contenuti come "in pipeline" cosÃ¬ che il week-fri possa ricontrollarli.

---

## 9. Logica di esecuzione â€” passo-passo

1. **Eseguire kickoff** per contesto workspace
2. **Leggere** `config/pillars-of-month.json` per pillar del mese in pianificazione (se non ancora settato, invocare skill `pillar-of-month-setup`)
3. **Leggere** tutti gli input strutturali e dinamici (sez. 3)
4. **Calcolare** distribuzione 45/30/20/5 sul totale stimato contenuti mese
5. **Generare** tabella settimana-per-settimana con assegnazione slot-canale-pillar-voce-firma
6. **Verificare** ratio 80/20 firma; ribilanciare se necessario
7. **Flaggare** pipeline ATL (>1 sett anticipo)
8. **Aggiungere** note del mese (festivitÃ , scadenze, opportunitÃ )
9. **Invocare** Brand Strategist (skill `brand-strategist` persona) per check coerenza pillar/voce/firma
10. **Invocare** Compliance Officer (gate 1) per scan veloce di temi sensibili pianificati
11. **Salvare** Markdown in `/05_Calendario_editoriale/[YYYY-MM]_[Mese].md`
12. **Notificare** MM (e CEO se Ã¨ la prima volta che si pianifica il mese): file pronto, da revisionare in Friday Email della settimana di chiusura

---

## 10. Casi particolari

### ModalitÃ  Ferie programmata (metÃ  luglio - metÃ  agosto)
- Sezione always-on al minimo (1 post P1 Educazione/settimana, 1 newsletter di fine luglio prima della pausa)
- Riprendere pianificazione piena dal 16 agosto

### Lancio specialty drop nuovo (es. Pillar 12 Terzo Settore luglio 2026)
- Allocare 10-15% al mese di lancio
- Mese precedente: 1-2 contenuti teaser sul pillar in arrivo
- Mese successivo: rientro a 5-10% di crociera

### Crisi di settore in corso (es. sinistro grave mandataria)
- ModalitÃ  Crisi attivabile dal CEO con subject email
- month-plan in pausa, MM presidia manualmente

### Sovrapposizione di big-event (es. apertura nuova sede + lancio specialty stesso mese)
- Segnalare al CEO come big bet di pianificazione: "Mese troppo carico, propongo di spostare X a Y"

---

## 11. Cosa NON fare mai

- âŒ **Pubblicare contenuto senza pillar assegnato** (ogni contenuto deve agganciare un pillar)
- âŒ **Sforare 70% firma Daniele** sui contenuti totali del mese
- âŒ **Dimenticare always-on P3 News** anche in mesi pieni di pillar dominante
- âŒ **Pianificare contenuti commerciali aggressivi** in periodi di lutto/festivitÃ  delicate (sensibilitÃ  di brand)
- âŒ **Saltare Pipeline ATL flagging** (causa #1 di scadenze mancate)
- âŒ **Pianificare oltre il mese in lavorazione** (un mese alla volta â€” il mese dopo lo fa il prossimo trigger)
- âŒ **Inventare festivitÃ  o scadenze** non verificate (per Pillar 3 News normativa, verificare sempre fonti)

---

## 12. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di pianificare, leggi in ordine:

1. `/00_README.md`
2. `/00_Brand_Book_v1.2.md` (sez. 6 Pillar Map Â· sez. 9 Compagine Â· sez. 13 MM Decision Authority)
3. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/01_Brand_Strategist.md` (titolare di stanza per validazione)
4. `/05_Calendario_editoriale/Spunti_CEO.md`
5. `/05_Calendario_editoriale/[mese precedente].md` (per coerenza di continuitÃ )
6. `config/pillars-of-month.json` Â· `config/brand.json` Â· `config/compagine.json` Â· `config/state.json`

---

*SKILL v1.0 â€” advisory-plus:month-plan â€” Sessione 2 Plugin Build â€” 2026-05-17*

