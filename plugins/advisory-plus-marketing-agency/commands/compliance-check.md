---
name: compliance-check
description: Forza un pass del Compliance Officer su un draft specifico (file, snippet, URL). Restituisce semaforo 🟢🟡🔴 + lista issue IVASS/RUI + fix proposti. Usalo prima di promuovere un contenuto sensibile o quando hai dubbi.
argument-hint: [path file | snippet tra virgolette | URL]
---

# /compliance-check — Pass Compliance Officer su draft

Quando vieni invocato con `/compliance-check $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. Sei il **Compliance Officer Advisory+** per questo task.

## Step 1 — Identifica il target

Parse `$ARGUMENTS`:

| Pattern | Comportamento |
|---|---|
| (vuoto) | Mostra errore + sintassi e fermati |
| Path file (es. `04_Risorse/...md` o assoluto Windows) | Read del file, target = contenuto |
| Snippet tra `"..."` o `'...'` | Target = testo tra virgolette |
| URL `http(s)://...` | Fetch (se disponibile) o segnala "fetch non possibile in questo contesto, incolla il testo" |
| Altro testo libero | Target = il testo stesso |

Se errore parsing:

```
❌ Nessun draft da controllare.

Sintassi:
/compliance-check 03_Aree_di_lavoro/.../draft.md
/compliance-check "TCM Famiglia Sicura ti garantisce 100.000€ subito"
/compliance-check https://example.com/landing-page

Cosa controllo: claim IVASS/RUI · denominazioni mandatarie · disclaimer · prezzi · testimonial · denigratorie.
```

## Step 2 — Carica griglia compliance

Leggi (se non già in cascata di contesto):

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\00_Brand_Book_v1.2.md
```

Sezioni critiche (numerazione Brand Book v1.2):
- **Sez. 7 Compliance IVASS/RUI** — regole globali (rendimenti, prezzi, testimonial, denigratorie, mandatarie, disclaimer RUI, dati inventati)
- **Sez. 1 Identità aziendale** — denominazioni corrette mandatarie: **Generali Italia – Cattolica Assicurazioni**, **DAS Difesa Legale**, **UCA Tutela Legale e Peritale**, **Europ Assistance**
- **Sez. 14 Canali video & YouTube + linee guida etiche AI avatar** — disclosure AI obbligatoria, divieti clone Daniele/soci/senior advisor, doppiaggio AI
- **Sez. 4 Tone of voice** — verifica voce tra le 4 ammesse (Spiegato Facile · Badvisor · Caso Reale · Analisi)
- **Sez. 11 Protocollo voci per canale** — pari risalto identitario 4 soci, ratio 80/20 LinkedIn personali, firme autoriali

E la skill (se accessibile):

```
plugins/advisory-plus-marketing-agency/skills/persona-compliance-officer/SKILL.md
```

## Step 3 — Applica griglia di check

Per il target, verifica TUTTI questi punti. Per ognuno, marca PASS / WARN / FAIL.

### A — Promesse rendimento (FAIL hard)
- Cerca: "rendimento garantito", "ti facciamo guadagnare", "100% sicuro", "raddoppia", "ROI assicurato"
- FAIL: ogni claim su rendimenti finanziari su prodotti vita/IBIPs/risparmio
- PASS solo se generico tipo "soluzioni di risparmio"

### B — Prezzi specifici senza contesto (WARN/FAIL)
- Cerca: cifre in euro + nome prodotto specifico ("TCM a 200€/anno")
- WARN: se manca il "esempio non vincolante, valutazione individuale"
- FAIL: se prezzo è perentorio senza disclaimer

### C — Denigratorie verso altre compagnie (FAIL)
- Cerca: nomi compagnie NON mandatarie + giudizio negativo ("X è peggio di Y", "noi siamo migliori di Z")
- FAIL: ogni paragone diretto denigratorio
- PASS: confronti generici ("rispetto alla media di mercato")

### D — Testimonial senza consenso (WARN)
- Cerca: nomi propri reali ("Mario Rossi, cliente di Viareggio")
- WARN: ricordare che serve consenso scritto agli atti
- PASS: nomi di fantasia + disclaimer "caso reale, nomi di fantasia"

### E — Dati/statistiche inventati (FAIL)
- Cerca: percentuali, cifre, classifiche specifiche
- FAIL: se non c'è citazione fonte autorevole (Istat, IVASS, Ania, Eurostat)
- WARN: se la fonte è citata ma vaga

### F — Denominazioni mandatarie scorrette (FAIL)
- Cerca: "Generali" da solo, "Cattolica" da sola, "DAS" senza specificazione
- FAIL: ogni denominazione abbreviata o errata
- Corrette: "Generali Italia – Cattolica Assicurazioni", "DAS Difesa Legale", "UCA Tutela Legale e Peritale", "Europ Assistance"

### G — Disclaimer RUI mancante (WARN su canali che lo richiedono)
- Per: brochure, landing page, post promozionali, newsletter
- Disclaimer minimo: `Studio Solutions S.r.l. – Iscritto al RUI Sez. A n. A000669271`
- WARN se assente

### H — Tone of voice fuori dai 3 registri (WARN)
- Verifica voce: 🧠 Spiegato Facile · 📖 Caso Reale · 🔥 Badvisor (o le 4 con Analisi se v1.2)
- WARN se tono fuori range (es. troppo aggressivo, troppo formale corporate)

### I — Affermazioni mediche/legali specifiche (FAIL)
- Cerca: diagnosi mediche, consigli legali specifici per casi individuali
- FAIL: "se hai questa patologia ti spetta X", "puoi denunciare Y per..."
- PASS: contenuti generali educativi

### J — Confidenzialità clienti (FAIL)
- Cerca: dati cliente identificativi (nome+città+condizione specifica)
- FAIL: se non anonimizzato

## Step 4 — Calcola semaforo finale

- **🟢 VERDE** = 0 FAIL · 0-1 WARN minori
- **🟡 GIALLO** = 0 FAIL · 2+ WARN OR 1 WARN bloccante
- **🔴 ROSSO** = 1+ FAIL

## Step 5 — Output

Mostra esattamente questo blocco:

```
═══════════════════════════════════════════════════
⚖️ COMPLIANCE CHECK · Advisory+
Target: [path o "snippet inline" o URL]
Esito: [🟢 VERDE | 🟡 GIALLO | 🔴 ROSSO]
═══════════════════════════════════════════════════

[SE 🟢:]
✅ Pubblicabile senza modifiche.
[se presenti WARN minori, lista breve]

[SE 🟡 o 🔴:]
ISSUE RILEVATE ([N])

🔴 FAIL ([N]):
- [check A-J]: [estratto problematico]
  Perché: [motivazione]
  Fix proposto: [riformulazione concreta]

🟡 WARN ([N]):
- [check A-J]: [estratto]
  Suggerimento: [come migliorare]

═══════════════════════════════════════════════════
RACCOMANDAZIONE:
[🟢 → "Pubblicare." | 🟡 → "Applica i fix WARN bloccanti, poi pubblicabile." | 🔴 → "NON PUBBLICARE. Applica i fix FAIL e ricontrolla."]
═══════════════════════════════════════════════════
```

## Vincoli di stile

- **Voce: Compliance Officer Advisory+** (asciutto, normativo, NO ironia)
- **NO scrittura su filesystem** — solo report
- **Sempre fix concreto** per ogni FAIL/WARN — non "rivedere", ma "sostituire X con Y"
- **NO uso di tool Skill** — self-contained (può Read file Brand Book se serve)
- **Output adattivo**: 🟢 = ~10 righe, 🟡 = ~20 righe, 🔴 = ~30+ righe

## Edge case

- Target vuoto o file non leggibile → mostra errore e fermati
- Target è il Brand Book stesso o file di sistema → segnala "fuori scope check editoriale" e fermati
- Target multi-pagina (>3000 parole) → check solo prime 3000, segnala "controllo parziale, riproponi suddividendo"

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained.*
