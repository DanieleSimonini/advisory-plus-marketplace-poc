---
name: compliance-citazioni-check
description: Validator dell'apparato citazionale Advisory+ per i contenuti in voce ðŸ“Š Analisi (Brand Book v1.2 sez. 4.4) e del disclaimer obbligatorio "Caso reale, nomi di fantasia" per i contenuti in voce ðŸ“– Caso Reale. Per voce Analisi: verifica che OGNI dato citato (statistiche, percentuali, importi, sentenze, riferimenti normativi) abbia apparato citazionale completo con fonte + anno (IVASS, ANIA, COVIP, ISTAT, Banca d'Italia, Eurostat, Cassazione con n.+data, Regolamenti UE, Codice ass.). Verifica esclusione fonti vietate (giornali generalisti come fonte primaria, blog non firmati, social media, AI-generated, "studi recenti" vaghi). Per voce Caso Reale: verifica presenza disclaimer "Caso reale, nomi di fantasia" (forma esatta, mai varianti creative). Restituisce semaforo ðŸŸ¢/ðŸŸ¡/ðŸ”´ + lista dati senza fonte + lista fonti vietate trovate + lista Casi Reali senza disclaimer + correzioni proposte. Triggera da skill content-* e compliance-gate-doppio.
---
# ðŸ“š Skill compliance-citazioni-check â€” Validator apparato citazionale Analisi + disclaimer Caso Reale

> **Voce Analisi: fonte+anno OBBLIGATORI. Voce Caso Reale: disclaimer "Caso reale, nomi di fantasia" SEMPRE. Zero eccezioni.**

---

## 1. Quando triggera

- **Automatico**: invocata dalle skill content-* (in particolare content-blog-article, content-newsletter, content-youtube-video quando voce Analisi o Caso Reale)
- **Automatico aggregato**: invocata da `compliance-gate-doppio` come sotto-verifica del gate 1
- **Manuale**: invocata via `/adv-citazioni-check [file]` per validare bozza in corso

Tempo target: **30-60 secondi** (scansione testuale + identificazione voce).

---

## 2. Output finale atteso

**Verdetto** consegnato al chiamante:

```markdown
# CITAZIONI CHECK
Voce rilevata: [Analisi / Caso Reale / Altro]
Esito: [ðŸŸ¢ NESSUNA VIOLAZIONE | ðŸŸ¡ VIOLAZIONI MINORI | ðŸ”´ VIOLAZIONI GRAVI]

## Voce Analisi â€” apparato citazionale (se applicabile)
### Dati citati rilevati: [N]
[Lista dati Â· forma Â· fonte associata se presente]

### Dati senza fonte+anno (violazioni)
[Lista Â· posizione nel file Â· proposta fonte da aggiungere o riformulazione qualitativa]

### Fonti vietate rilevate (violazioni)
[Lista Â· tipo fonte vietata Â· proposta sostituzione con fonte primaria autorevole]

## Voce Caso Reale â€” disclaimer (se applicabile)
### Disclaimer presente: [SÃŒ/NO]
### Forma del disclaimer trovato: [stringa esatta]
### ConformitÃ  alla forma standard: [SÃŒ/NO â€” la forma standard Ã¨ "Caso reale, nomi di fantasia"]

## Riformulazione proposta
[Testo corretto con apparato citazionale aggiunto o disclaimer corretto Â· ready-to-merge]
```

---

## 3. Voce Analisi â€” apparato citazionale obbligatorio

### Cosa scattare come "dato che richiede fonte"
- **Percentuali, statistiche, importi** (es. "il 12%", "89 miliardi di euro", "+4,3%")
- **Riferimenti a sentenze** (es. "la Cassazione ha stabilito cheâ€¦")
- **Riferimenti a normative** (es. "il Regolamento IVASS imponeâ€¦", "il Codice delle assicurazioni private prevedeâ€¦")
- **Affermazioni quantitative di mercato** (es. "il mercato vita italianoâ€¦", "i fondi pensione hanno resoâ€¦")
- **Confronti storici quantitativi** (es. "negli ultimi 10 anniâ€¦", "dal 2020 al 2024â€¦")
- **Trend dichiarati** (es. "in crescita del 5%", "in calo del 12%")

### Fonti accettate (ordine di preferenza)
1. **IVASS** (Regolamenti, Lettere al Mercato, Statistiche annuali, Indagini)
2. **ANIA** (Relazione annuale, Bollettini settoriali)
3. **COVIP** (Relazione annuale, Bollettini fondi pensione)
4. **ISTAT** (dati demografici, sanitari, reddito, consumi)
5. **Banca d'Italia** (statistiche risparmio, indagine famiglie)
6. **Eurostat** (confronti UE)
7. **Cassazione e tribunali** (sentenze con n. e data: `Cass. civ. n. XXXX/YYYY`)
8. **Codice delle assicurazioni private** (`D.Lgs. 209/2005 art. XX`)
9. **Regolamenti e Direttive UE** (`Reg. UE YYYY/NN`, `Direttiva YYYY/NN/UE`)
10. **Studi/report di centri qualificati** (`Cetif, OAM, AIBA, Mefop` con titolo + anno + URL)

### Fonti vietate (scattare come violazione ðŸ”´)
- âŒ **Articoli giornalistici generalisti** come fonte primaria (Corriere, Repubblica, Sole 24 Ore, etc. â€” possono essere "punto di osservazione" ma il dato deve risalire alla fonte primaria)
- âŒ **Blog di settore non firmati** o senza apparato proprio
- âŒ **Social media** (LinkedIn post, X tweet, Facebook) come fonte primaria
- âŒ **Studi non disponibili pubblicamente** o citati di seconda mano ("come risulta da uno studio internoâ€¦")
- âŒ **AI-generated** (no "secondo ChatGPT/Claudeâ€¦", "ho analizzato con AIâ€¦")
- âŒ **Riferimenti vaghi** ("secondo studi recenti", "alcune ricerche dimostrano", "molti esperti ritengono")
- âŒ **Anno mancante** ("ANIA" senza anno â†’ dato escluso)

### Forma corretta delle citazioni
- **In linea** (inline citation): subito dopo il dato `(IVASS, 2024)` Â· `(ANIA Relazione annuale, 2024)` Â· `(Cass. civ. n. 12345/2023)` Â· `(D.Lgs. 209/2005, art. 121)`
- **In bibliografia** (per articoli lunghi): sezione "Fonti" in calce con elenco completo (autore/ente Â· titolo Â· anno Â· URL ufficiale se disponibile)

---

## 4. Voce Caso Reale â€” disclaimer obbligatorio

### Forma standard (unica accettata)
> **"Caso reale, nomi di fantasia."**

### Forme NON accettate
- âŒ "Storia vera, nomi inventati"
- âŒ "Ispirato a fatti reali"
- âŒ "Tratto da un caso reale"
- âŒ "Episodio realmente accaduto, nomi modificati"
- âŒ Tutte le altre varianti creative

### Posizione del disclaimer
- **In coda** al contenuto Caso Reale (post social, articolo blog, caption Reel, descrizione YouTube)
- **Inline o ridotto** per Stories (anche solo "Caso reale" in slide finale Ã¨ accettabile per limite formato)
- **In corpo** per newsletter quando highlight Ã¨ Caso Reale

### Eccezioni
- Nessuna. Anche su Stories ridotto, la formula deve esserci nel contesto.

---

## 5. Logica di esecuzione â€” passo-passo

1. **Ricevere file** dal chiamante (Markdown completo)
2. **Eseguire kickoff** per contesto workspace
3. **Identificare voce** del contenuto (lettura frontmatter `voce: [...]` o euristica testuale)
4. **Se voce Ã¨ Analisi**:
   - Scansiona testo con regex per percentuali, importi, riferimenti normativi, riferimenti a sentenze, statistiche
   - Per ogni dato rilevato, verifica presenza di `(fonte, anno)` o `(fonte titolo, anno)` o `(D.Lgs. XX/YYYY, art. NN)` o `(Cass. civ. n. XXXX/YYYY)` nelle immediate vicinanze
   - Identifica fonti vietate (grep "secondo studi recenti", "alcune ricerche", "ChatGPT", "Claude", citazione Corriere/Repubblica senza ente primario, ecc.)
   - Aggregare ðŸŸ¢/ðŸŸ¡/ðŸ”´
5. **Se voce Ã¨ Caso Reale**:
   - Verifica presenza disclaimer "Caso reale, nomi di fantasia" (grep esatto)
   - Verifica posizione (in coda, inline per Stories, in corpo per newsletter)
   - Aggregare ðŸŸ¢/ðŸŸ¡/ðŸ”´
6. **Se voce non Ã¨ Analisi nÃ© Caso Reale**:
   - Restituisci ðŸŸ¢ + nota "Voce [X] â€” apparato citazionale e disclaimer Caso Reale non applicabili"
7. **Produrre riformulazione** proposta (se applicabile) con aggiunta apparato/disclaimer
8. **Restituire verdetto** al chiamante

Nessuna scrittura del file originale (solo lettura). Correzione Ã¨ del chiamante.

---

## 6. Casi particolari

### Articolo Analisi su sentenza Cassazione fresca
- Apparato citazionale rigoroso obbligatorio: `Cass. civ. n. XXXX/2024 del [data]`
- Sezione "Fonti" in calce obbligatoria per articolo blog lungo

### Articolo Analisi con dato di mercato citato da articolo giornalistico
- Skill segnala ðŸŸ¡: "Articolo giornalistico come fonte primaria â†’ risali alla fonte originale (ANIA/IVASS/ente)"
- Riformulazione: cerca fonte primaria autorevole, riformula citazione

### Caso Reale con disclaimer "Storia vera, nomi cambiati"
- Skill segnala ðŸŸ¡: "Disclaimer presente ma forma non standard"
- Riformulazione: sostituisci con "Caso reale, nomi di fantasia" esatto

### Caso Reale completamente privo di disclaimer
- Skill segnala ðŸ”´: "Caso Reale senza disclaimer â€” violazione grave"
- Riformulazione: aggiungi disclaimer in coda al contenuto

### Post social misto (es. apertura Caso Reale + chiusura riflessiva Analisi)
- Skill applica entrambi i check
- Se voce primaria Ã¨ Caso Reale (frontmatter) â†’ disclaimer obbligatorio
- Se in chiusura ci sono dati â†’ apparato citazionale obbligatorio per quei dati specifici

### Contenuto con dato "stimato" o "approssimativo"
- Skill segnala ðŸŸ¢ SE Ã¨ chiaramente dichiarato come stima/approssimazione e l'apparato Ã¨ coerente (es. "stima ANIA su dati 2024 â€” circa 89 miliardi")
- Skill segnala ðŸŸ¡ SE la stima non Ã¨ dichiarata come tale (rischio passare per dato certo)

### Caso Reale che cita numeri/importi concreti
- Verifica voce-caso-reale SKILL sez. 4: numeri verosimili e cauti, mai inventati per effetto
- Compliance check passa se numeri sono plausibili e non hanno apparato citazionale come dati di mercato (sono dati narrativi del caso)
- Se sono dati di mercato camuffati da dati narrativi â†’ ðŸŸ¡, richiedi chiarezza al chiamante

---

## 7. Cosa NON fare mai

- âŒ **Auto-aggiungere fonti inventate** (se il chiamante non fornisce, segnalare e attendere)
- âŒ **Accettare "studi recenti dimostrano"** o riferimenti vaghi (sempre nome ente + anno)
- âŒ **Accettare AI-generated come fonte** (mai)
- âŒ **Modificare la forma del disclaimer Caso Reale** (Ã¨ "Caso reale, nomi di fantasia" esatto, non variabile)
- âŒ **Saltare check su Caso Reale** assumendo che il disclaimer ci sia (verifica sempre con grep)
- âŒ **Confondere voce Analisi con Spiegato Facile** (Spiegato Facile NON richiede apparato citazionale per scelta editoriale)
- âŒ **Bypassare check per fretta** (apparato citazionale Ã¨ il punto di credibilitÃ  della voce Analisi â€” saltare un check = pubblicare un dato senza fonte = perdita credibilitÃ  + rischio Compliance)
- âŒ **Validare il proprio output** (segnalare anomalie al chiamante che decide)

---

## 8. Cascata di contesto obbligatoria (pre-esecuzione)

Prima di validare, leggi in ordine:

1. `/00_Brand_Book_v1.2.md` (sez. 4.4 voce Analisi Â· sez. 4.3 voce Caso Reale Â· sez. 7 Compliance)
2. `/01_Team/04_Compliance_Officer.md`
3. `config/brand.json` (sez. `voci_editoriali.analisi.apparato_citazionale` Â· sez. `voci_editoriali.caso_reale.disclaimer_obbligatorio`)

---

*SKILL v1.0 â€” advisory-plus:compliance-citazioni-check â€” Sessione 4 Plugin Build â€” 2026-05-19*

