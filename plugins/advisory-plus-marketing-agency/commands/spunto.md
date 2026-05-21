---
name: spunto
description: Salva uno spunto editoriale del CEO in Spunti_CEO.md con timestamp e tag. Usalo quando hai un'idea, una notizia, un caso cliente, una riflessione da girare al team marketing per la prossima settimana.
argument-hint: [testo dello spunto, eventualmente prefisso [news|tema|push|domanda|veto|idea|contatto]]
---

# /spunto — Ingest spunto editoriale CEO

Quando vieni invocato con `/spunto $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. Non aspettare ulteriori input. Non chiedere conferme. Fire-and-forget.

## Step 1 — Validazione argomenti

Se `$ARGUMENTS` è vuoto: mostra messaggio errore e fermati.

```
❌ Nessuno spunto fornito.

Sintassi: /spunto [testo dello spunto]

Esempi:
/spunto [news] https://www.ilsole24ore.com/art/articolo-x → da commentare in pillar Risparmio Sensato
/spunto [idea] serie video sui falsi miti delle polizze RC Auto
/spunto LTC: cliente raccontava zia 78 anni costa 2800€/mese RSA Camaiore. Caso reale, anonimizzare.
```

## Step 2 — Localizza file Spunti_CEO

Path canonico:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\05_Calendario_editoriale\Spunti_CEO.md
```

Usa Read tool. Se il file non esiste:

1. Crea cartella `05_Calendario_editoriale` se manca
2. Crea il file con questo header minimo:

```markdown
# 💡 Spunti dal CEO — Input al Marketing Manager

## 📋 DA TRATTARE

## 📦 ARCHIVIATI

```

## Step 3 — Inferenza metadati spunto

Analizza `$ARGUMENTS` per inferire:

### Tag prefisso (se non già fornito tra `[...]` all'inizio)
Keyword matching breve:
- contiene "https://" o "http://" → `[news]`
- contiene "veto" / "non pubblicare" / "stop" → `[veto]`
- contiene "domanda" / "?" all'inizio → `[domanda]`
- contiene "tema" / "approfondire" → `[tema]`
- contiene "settembre"/"ottobre"/etc. + "pillar" → `[push]`
- contiene "contatto" / "partner" / "studio " → `[contatto]`
- altrimenti → `[idea]`

### Pillar Brand Book v1.2 inferito
Match keyword sui 12 pillar (dal Brand Book sez. 6 + 6bis). Se ambiguo: `[da-classificare]`.

Esempi rapidi:
- "TCM" / "famiglia che protegge" / "vedova" → `Pillar 1 La famiglia che protegge`
- "LTC" / "RSA" / "anziano" / "dopo di noi" → `Pillar 2 Il dopo di noi, il dopo di loro`
- "previdenza" / "PIP" / "risparmio" → `Pillar 3 Risparmio sensato`
- "tutela legale" / "UCA" / "DAS" → `Pillar 4 Tutela legale invisibile`
- "Viareggio" / "Massa" / "Carrara" / "territorio" → `Pillar 5 Territorio Advisory+`

### Voce editoriale inferita
- contiene "raccontava" / "cliente Maria" / "vedova" / "caso" → `📖 Caso Reale`
- contiene "paradosso" / "ironico" / "tanto a me" → `🔥 Badvisor`
- contiene "spiegare" / "come funziona" / "cosa è" → `🧠 Spiegato Facile`
- contiene "analisi" / "dati" / "Istat" / "studio" → `📊 Analisi`
- altrimenti → lascia vuoto

### Flag anonimizzazione
- contiene nomi reali tipo "Maria"/"Luigi"/"Mario"/"Anna" + contesto cliente → `🟡 anonimizzazione richiesta`
- contiene "anonimizzare" → `🟡 anonimizzazione richiesta`
- altrimenti → nessun flag

## Step 4 — Auto-deduplica 72h

Leggi le ultime 3 sezioni `## YYYY-MM-DD` sotto `## 📋 DA TRATTARE`. Se trovi uno spunto con testo identico (case-insensitive, primo 80% del testo):
- NON appendere
- Output: `⚠️ Spunto duplicato (già presente in [data]). Non aggiunto.` e fermati.

## Step 5 — Append entry

Trova la sezione `## 📋 DA TRATTARE` nel file. Sotto di essa:

1. Se esiste già una sezione `## YYYY-MM-DD` con la data odierna (formato ISO): aggiungi una nuova bullet sotto quella sezione.
2. Se non esiste: crea nuova sezione `## YYYY-MM-DD` (data odierna dall'env) appena sotto `## 📋 DA TRATTARE`, prima di eventuali altre date più vecchie.

Formato bullet:

```
- [tag_prefisso] [testo originale dello spunto] · Pillar: [pillar_inferito] · Voce: [voce_inferita o "—"] · [flag anonimizzazione se presente]
```

Usa Edit tool sul file Spunti_CEO.md per inserire (preserva struttura esistente, non sovrascrivere il file intero).

## Step 6 — Conta numero progressivo

Conta quanti bullet ci sono sotto `## 📋 DA TRATTARE` in totale (incluso quello appena aggiunto). Il numero è `N`.

## Step 7 — Output al CEO

Mostra esattamente questo blocco (max 6 righe):

```
✅ Spunto #[N] salvato in Spunti_CEO.md
Tag: [tag_prefisso]
Pillar inferito: [pillar_inferito]
Voce inferita: [voce_inferita o "—"]
[se flag presente:] Flag: 🟡 anonimizzazione richiesta
Sarà valutato dal MM nel prossimo Friday Email (ven 18:00).
```

## Vincoli di stile

- **Mai chiedere conferme** al CEO — fire-and-forget
- **Mai aprire conversazione** sul contenuto dello spunto — solo conferma asciutta
- **NO uso di tool Skill** — self-contained
- **Output massimo 7 righe**
- **Niente compliance check** in questo step (è ingest, non publish)

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained.*
