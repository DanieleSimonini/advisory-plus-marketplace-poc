---
name: modalita
description: Switch della modalità operativa del sistema marketing Advisory+ (normale, ferie, crisi). Lancialo senza argomenti per leggere lo stato corrente, oppure con argomenti per cambiarlo. Aggiorna il file di stato persistente sul workspace.
argument-hint: [normale | ferie YYYY-MM-DD YYYY-MM-DD [light|full] | crisi [motivo="..."]]
---

# /modalita — Switch modalità operativa Advisory+

Quando vieni invocato con `/modalita`, esegui SUBITO le istruzioni qui sotto. Non aspettare ulteriori input dal CEO. Non chiedere conferme.

## Step 1 — Localizza o crea il file di stato

Il file di stato canonico è:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\04_Risorse\Stato_Sistema\modalita.json
```

Procedi così:
1. Usa il tool **Read** sul path. Se restituisce errore "file not found":
   - Crea la cartella `Stato_Sistema` se non esiste
   - Crea il file con questo contenuto iniziale (usa il timestamp ISO 8601 corrente — se non sai l'ora precisa usa `bash: date -Iseconds`, altrimenti la data odierna fornita nell'env con ora `12:00:00+02:00`):

```json
{
  "stato": "normale",
  "since": "<timestamp ISO 8601>",
  "end_date": null,
  "variante": null,
  "motivo": null
}
```

2. Se il file esiste, parsa il JSON.

## Step 2 — Parse argomenti `$ARGUMENTS`

Identifica il pattern degli argomenti ricevuti:

| Pattern | Azione |
|---|---|
| (vuoto, nessun argomento) | **READ-ONLY**: mostra solo lo stato corrente, NON scrivere il file |
| `normale` | Set: `stato=normale`, `end_date=null`, `variante=null`, `motivo=null`, aggiorna `since` |
| `ferie YYYY-MM-DD YYYY-MM-DD` | Set: `stato=ferie`, `variante=light`, `end_date=secondo arg`, aggiorna `since` |
| `ferie YYYY-MM-DD YYYY-MM-DD light` | Idem ma `variante=light` esplicito |
| `ferie YYYY-MM-DD YYYY-MM-DD full` | Idem ma `variante=full` |
| `crisi` | Set: `stato=crisi`, `motivo=null`, `end_date=null`, aggiorna `since` |
| `crisi motivo="testo"` | Idem ma `motivo=testo` (estratto da virgolette) |
| altro / malformato | NON scrivere. Mostra messaggio errore con sintassi corretta (vedi Step 4). |

Per gli aggiornamenti: usa il tool **Write** sul path canonico con il JSON aggiornato. `since` deve essere il timestamp ISO 8601 corrente.

## Step 3 — Output al CEO

Scegli il formato in base a cosa hai fatto:

### Caso A — Solo READ (nessun argomento ricevuto)

Mostra esattamente questo blocco (sostituisci i valori tra parentesi quadre):

```
MODALITÀ CORRENTE: [STATO_MAIUSCOLO] [emoji]
─────────────────────────────────
Attiva dal: [since formattata italiano breve, es. "21 mag 2026 ore 16:42"]
[SE stato=ferie:] Fine prevista: [end_date formattata, es. "22 ago 2026"] · Variante: [variante]
[SE stato=crisi:] Motivo: [motivo OPPURE "(non specificato)" se null]

Per cambiare digita una delle sintassi qui sotto:
/modalita normale
/modalita ferie 2026-08-08 2026-08-22 [light|full]
/modalita crisi [motivo="testo"]
```

Mapping emoji: `normale` → 🟢, `ferie` → 🌴, `crisi` → 🚨.

### Caso B — WRITE (modalità cambiata)

Mostra esattamente questo blocco:

```
✅ MODALITÀ AGGIORNATA: [NUOVO_STATO_MAIUSCOLO] [emoji]
─────────────────────────────────
Attiva dal: [nuovo since formattato]
[SE stato=ferie:] Fine prevista: [end_date] · Variante: [variante]
[SE stato=crisi:] Motivo: [motivo OPPURE "(non specificato)"]

Stato persistito in 04_Risorse/Stato_Sistema/modalita.json
```

### Caso C — Errore di parse argomenti

NON scrivere il file. Mostra:

```
❌ Sintassi non riconosciuta: "[argomenti ricevuti]"

Stato corrente NON modificato: [stato corrente in MAIUSCOLO]

Sintassi valide:
  /modalita                                  → leggi stato corrente
  /modalita normale                          → torna a normale
  /modalita ferie 2026-08-08 2026-08-22       → ferie 8-22 ago (light)
  /modalita ferie 2026-08-08 2026-08-22 full  → ferie full stop
  /modalita crisi                            → crisi immediata
  /modalita crisi motivo="ispezione IVASS"   → crisi con motivo
```

## Step 4 — Vincoli di stile

- **Output massimo 12 righe.** Niente preamboli ("Procedo...", "Ho capito che vuoi..."), niente postambolo ("Fatto!", "Tutto a posto!").
- **Niente disclaimer compliance** in questo output (è command interno, non contenuto pubblico).
- **Niente domande di follow-up.** Esegui e basta.
- **Niente uso di tool Skill** durante l'esecuzione di questo command — è self-contained.

---

*Slash command v1.1 — Plugin Build Sessione 22 — 2026-05-21 — refactor da documentazione descrittiva a istruzione imperativa self-contained.*
