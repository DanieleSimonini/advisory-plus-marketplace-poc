---
name: spunto
description: Salva uno spunto editoriale del CEO in Spunti_CEO.md con timestamp e tag. Usalo quando hai un'idea, una notizia, un caso cliente, una riflessione da girare al team marketing per la prossima settimana.
argument-hint: [testo dello spunto]
---

# /spunto — Ingest spunto editoriale CEO

## Cosa fa

Acquisisce uno spunto del CEO (idea, notizia, caso cliente, link articolo, riflessione strategica) e lo appende a `/05_Calendario_editoriale/Spunti_CEO.md` con:

- Timestamp ISO 8601
- Tag pillar (auto-inferito dal contesto se possibile, altrimenti `[da-classificare]`)
- Stato `🟦 nuovo` (pending pickup Marketing Manager)

## Sintassi

```
/spunto LTC: cliente raccontava che la zia 78 anni costa 2800€/mese RSA Camaiore. Da raccontare senza nominarla, caso reale ToV.
```

```
/spunto https://www.ilsole24ore.com/art/articolo-x — leggere e valutare se citare in pillar "Risparmio Sensato"
```

```
/spunto [BADVISOR] paradosso del "tanto a me non capita" applicato a tutela legale famiglia. Ironico ma non contro lettore.
```

## Skill innescata

`skills/process/editorial/ingest-spunto/SKILL.md`

## Output atteso

Risposta brevissima, stile Spiegato Facile:

```
✅ Spunto #N salvato in Spunti_CEO.md
Tag inferito: [pillar]
Voce inferita: [voce]
Sarà valutato dal MM nel prossimo piano (Friday Email).
```

## Comportamento attesi

- **Mai chiedere conferme** al CEO — è un fire-and-forget, lo spunto va dentro e basta
- **Inferenza tag pillar**: usa keyword matching su 12 pillar del Brand Book v1.2 (sez. 6 + 6bis)
- **Se ambiguo**: assegna `[da-classificare]`, NON fermarsi per chiedere
- **Auto-deduplica**: se uno spunto identico è già presente nelle ultime 72h, log e segnala (non duplicare)

## Compliance check

L'hook `pre-publish-compliance` NON si applica qui (è solo ingestion, non publish). Però se lo spunto contiene un nome cliente reale → flag `🟡 anonimizzazione richiesta` prima del pickup MM.

## Esempio reale

```
CEO: /spunto incontrato Maria, vedova 62 anni, marito morto improvviso 2 anni fa senza TCM. Lei tira avanti col mutuo addosso. Caso reale potenza ToV "Caso Reale" — anonimizzare.

Output:
✅ Spunto #47 salvato in Spunti_CEO.md
Tag inferito: [Famiglia che protegge — TCM]
Voce inferita: 📖 Caso Reale
Flag: 🟡 anonimizzazione richiesta (nome Maria → fantasia)
Sarà valutato dal MM nel prossimo piano (Friday Email ven 22 mag 18:00).
```

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
