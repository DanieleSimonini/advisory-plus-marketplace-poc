---
name: strategia-pillar-of-month-setup
description: Decide il pillar dominante del mese Advisory+ e aggiorna config/pillars-of-month.json. Triggera (a) automaticamente da skill month-plan quando il file config non Ã¨ ancora settato per il mese in pianificazione Â· (b) manualmente dal CEO via slash command /adv-pillar-push [pillar-id] [YYYY-MM] per forzare un pillar specifico in un mese specifico. Logica: default = rotazione dei 6 pillar rotanti P4-P9 (Famiglia Â· AnzianitÃ  & LTC Â· Risparmio Â· Tutela Legale Â· Casa Â· Imprese) secondo sequenza in brand.json. Bilancia il dominante 45% peso con 2 pillar di background al 20% complessivo, sceglie i background per evitare ripetitivitÃ  e per dare continuitÃ  tematica (es. dominante P5 LTC â†’ background suggeriti P4 Famiglia + P6 Risparmio per pattern "tutela patrimoniale del ciclo di vita"). Considera stagionalitÃ  (es. P4 Famiglia primavera, P8 Casa rinnovi, P6 Risparmio fine anno). Verifica specialty drop attiva e aggiusta i pesi se necessario. Aggiorna pillars-of-month.json + notifica MM per propagare al month-plan. NON esegue pianificazione contenuti (compito di month-plan).
---
# ðŸ§­ Skill pillar-of-month-setup â€” Decisore pillar mensile Advisory+

> **Una decisione strategica al mese. Il pillar che orchestra 45% dei contenuti. Brand Book v1.2 sez. 6 Pillar Map.**

---

## 1. Quando triggera

- **Automatico**: invocata da `advisory-plus:month-plan` quando per il mese in pianificazione `config/pillars-of-month.json` non ha ancora un'assegnazione
- **Manuale**: `/adv-pillar-push [pillar-id] [YYYY-MM]` (CEO o MM forzano un pillar specifico per un mese)
- **Manuale ricalcolo**: `/adv-pillar-setup [YYYY-MM]` per ricalcolare un mese giÃ  settato

Tempo target di esecuzione: **5-10 minuti**.

---

## 2. Output finale atteso

**Aggiornamento di** `config/pillars-of-month.json` con la nuova entry per il mese pianificato:

```json
{
  "2026-06": {
    "dominant": { "id": "P5", "name": "AnzianitÃ  & LTC", "weight": 0.45 },
    "background": [
      { "id": "P4", "name": "Famiglia & Vita", "weight": 0.10 },
      { "id": "P8", "name": "Casa & Patrimonio", "weight": 0.10 }
    ],
    "always_on": [
      { "id": "P1", "name": "Educazione assicurativa", "weight": 0.10 },
      { "id": "P2", "name": "Voce CEO autoriale", "weight": 0.10 },
      { "id": "P3", "name": "News di settore", "weight": 0.10 }
    ],
    "specialty_active": [
      { "id": "P10", "name": "Mare & Yacht", "weight": 0.05 }
    ],
    "rationale": "Pillar dominante P5 LTC scelto per stagionalitÃ  inizio estate (focus famiglie su salute anziani prima delle ferie) + completamento rotazione semestre. Background P4 + P8 per pattern 'tutela patrimoniale del ciclo di vita'. Specialty P10 Mare attiva (stagione).",
    "decided_by": "MM auto / CEO manual override",
    "decision_date": "2026-05-30"
  }
}
```

**Notifica al MM** (e CEO via email se override): "pillar-of-month per [mese] settato a P[N]. Continua con month-plan."

---

## 3. I 12 pillar â€” quick reference

(Da Brand Book v1.2 sez. 6 Pillar Map)

### 3 Always-on (sempre attivi, 30% complessivo)
- **P1** Educazione assicurativa â€” voce dominante: Spiegato Facile
- **P2** IdentitÃ  del consulente / Voce CEO autoriale â€” voce mix (presidio Daniele Simonini, profilo LinkedIn personale)
- **P3** News di settore (IVASS, normativa, mandanti) â€” voce dominante: Analisi

### 6 Pillar-of-month rotanti (45% dominante uno per volta)
- **P4** Famiglia & Vita (incl. sotto-tema Salute)
- **P5** AnzianitÃ  & LTC
- **P6** Risparmio & Investimento
- **P7** Tutela Legale
- **P8** Casa & Patrimonio
- **P9** Imprese & Professionisti

### 3 Specialty (trimestrali/eventi, 5-10% quando attive)
- **P10** Mare & Yacht (stagione giugno-settembre)
- **P11** Arte & Patrimonio culturale (autunno)
- **P12** Enti religiosi & Terzo Settore (lancio luglio 2026)

---

## 4. Logica di rotazione default

In assenza di forzature CEO, la rotazione default segue uno **schema semestrale bilanciato**:

| Mese | Pillar dominante (default) | Background suggeriti | Note stagionali |
|---|---|---|---|
| Gen | **P6** Risparmio & Investimento | P9 Imprese + P4 Famiglia | Inizio anno fiscale, scadenze previdenziali |
| Feb | **P7** Tutela Legale | P9 Imprese + P4 Famiglia | Bassa stagione rinnovi, picco coperture professionali |
| Mar | **P4** Famiglia & Vita | P5 LTC + P8 Casa | Inizio rinnovi auto, primavera famiglie |
| Apr | **P8** Casa & Patrimonio | P4 Famiglia + P5 LTC | Picco rinnovi casa, sensibilitÃ  ambiente |
| Mag | **P9** Imprese & Professionisti | P7 Tutela + P6 Risparmio | Chiusura bilanci primo trimestre |
| Giu | **P5** AnzianitÃ  & LTC | P4 Famiglia + P8 Casa | Famiglie pensano alla salute anziani prima delle ferie Â· specialty P10 Mare attiva |
| Lug-Ago | **ModalitÃ  Ferie estesa** | Always-on minimo | Pausa pianificazione, ripresa metÃ  agosto |
| Set | **P6** Risparmio & Investimento | P4 Famiglia + P9 Imprese | Ripresa autunnale, primo spunto previdenza |
| Ott | **P7** Tutela Legale | P9 Imprese + P5 LTC | Picco coperture professionali post-estate |
| Nov | **P5** AnzianitÃ  & LTC | P4 Famiglia + P6 Risparmio | "Mese della previdenza" tradizionale Â· COVIP rel. annuale |
| Dic | **P4** Famiglia & Vita | P6 Risparmio + P8 Casa | Spunti regalo previdenza + chiusura anno + 730 imminente |

**Specialty rotation**:
- P10 Mare: attivo giugno-settembre (5-10%)
- P11 Arte: attivo ottobre-novembre (5%)
- P12 Terzo Settore: lancio luglio 2026, poi attivo a rotazione trimestrale (5%)

---

## 5. Criteri di scelta dei background pillar

Quando si decide il dominante, si scelgono **2 background** seguendo questi criteri (in ordine di prioritÃ ):

1. **ContinuitÃ  tematica**: pillar che fanno "filo conduttore" con il dominante
   - P5 LTC dominante â†’ bg P4 Famiglia (chi pianifica per genitori) + P8 Casa (struttura abitativa per anziani)
   - P9 Imprese dominante â†’ bg P7 Tutela Legale (RC professionale) + P6 Risparmio (previdenza titolari)
   - P4 Famiglia dominante â†’ bg P8 Casa + P7 Tutela Legale (protezione 360Â° famiglia)

2. **Evitare ripetitivitÃ **: non riusare gli stessi background del mese precedente
   - Se il mese precedente aveva dominante P5 con bg P4+P8, e questo mese il dominante Ã¨ P4, evitare di rimettere P5 e P8 come bg â†’ cercare combinazione fresca

3. **StagionalitÃ **: pillar che hanno aggancio stagionale al mese corrente
   - Marzo-maggio: P8 Casa (rinnovi)
   - Settembre-ottobre: P6 Risparmio (ripresa)
   - Novembre-dicembre: P6 Risparmio (anno fiscale)

4. **Specialty bilanciamento**: se una specialty Ã¨ attiva e prende 10%, i background scendono a 8% ciascuno (16% totale invece di 20%) per non sforare il totale

---

## 6. Casi particolari

### CEO override esplicito
Se il CEO invoca `/adv-pillar-push P9 2026-07`, la skill **non discute**: setta P9 come dominante per luglio 2026 e sceglie solo i background coerenti.

Note nel `rationale` della entry: "Forzato da CEO con override esplicito 2026-XX-XX."

### Lancio nuovo specialty (Terzo Settore luglio 2026)
- Allocare specialty al 10-15% (piÃ¹ alto del 5% di crociera)
- Background sottraggono 5% al loro peso normale
- `rationale` esplicito: "Mese di lancio specialty Pillar 12 Terzo Settore â€” peso elevato al 15%, background a 7% ciascuno"

### Trust Calibration Window attiva (primi 30 gg post-go-live plugin)
- Aggiungere campo nella entry: `"trust_calibration": true`
- Aggiungere nota MM per Friday Email sez. F: "Pillar di [mese] scelto in autonomia: [rationale]. CEO conferma?"

### Crisi di settore (es. crisi mandataria, lutto territoriale)
- NON eseguire setup automatico
- Notificare CEO: "Crisi attiva. Setup pillar [mese] sospeso. Attendo direttiva."

### ContinuitÃ  multi-mese (campagna lunga)
- Se Ã¨ attiva una campagna 30/60/90 con un pillar protagonista, **mantenere lo stesso dominante** per la durata della campagna (anche se contraddice la rotazione default)
- Es. campagna recruiting JIA su 90 giorni con focus Pillar 9 Imprese â†’ P9 dominante per 3 mesi consecutivi

---

## 7. Cosa NON fare mai

- âŒ **Inventare pillar non in mappa** (sono 12, esattamente quelli del Brand Book v1.2)
- âŒ **Settare il dominante uguale al mese precedente** senza una ragione strategica forte (es. campagna in corso)
- âŒ **Sforare il 45%** del dominante (rischio mono-tematicitÃ ) o scendere sotto 40% (rischio dispersione)
- âŒ **Saltare gli always-on** (P1+P2+P3 sempre presenti, sempre 30% complessivo)
- âŒ **Attivare specialty fuori stagione** (P10 Mare in dicembre â†’ off-brand)
- âŒ **Modificare retroattivamente** un pillar di un mese giÃ  in esecuzione (rompe il piano del MM e i contenuti giÃ  prodotti)
- âŒ **Settare il pillar oltre il mese successivo** (un mese alla volta â€” la sequenza Ã¨ gestita dalla rotazione default)

---

## 8. Logica di esecuzione â€” passo-passo

1. **Eseguire kickoff**
2. **Leggere** `config/pillars-of-month.json` per stato attuale + ultimi 6 mesi (per evitare ripetitivitÃ )
3. **Leggere** `config/brand.json` sez. pillars per regole di rotazione default
4. **Leggere** `/05_Calendario_editoriale/Campagne/` per verificare campagne attive multi-mese
5. **Verificare** stagionalitÃ  del mese pianificato (tabella sez. 4)
6. **Verificare** specialty potenzialmente attive nel mese pianificato
7. **Applicare logica**:
   - Se CEO override â†’ applica + nota
   - Se campagna attiva multi-mese â†’ continua col dominante della campagna
   - Altrimenti â†’ rotazione default + selezione background per criteri sez. 5
8. **Costruire entry JSON** con dominante + 2 bg + always-on + specialty attive + rationale + decided_by + decision_date
9. **Scrivere** in `config/pillars-of-month.json` (append-only per mese)
10. **Notificare MM** (e CEO se override): pillar settato, prossimo passo `month-plan`

---

## 9. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di decidere, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 6 Pillar Map)
2. `/01_Team/00_Marketing_Manager.md` Â· `/01_Team/01_Brand_Strategist.md`
3. `config/brand.json` (sez. pillars Â· regole rotazione Â· stagionalitÃ )
4. `config/pillars-of-month.json` (storico)
5. `/05_Calendario_editoriale/Campagne/` (campagne attive)
6. `config/state.json` (eventuali modalitÃ  ferie/crisi)

---

*SKILL v1.0 â€” advisory-plus:pillar-of-month-setup â€” Sessione 2 Plugin Build â€” 2026-05-17*

