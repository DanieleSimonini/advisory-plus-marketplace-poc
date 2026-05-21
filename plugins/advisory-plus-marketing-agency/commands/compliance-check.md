---
name: compliance-check
description: Forza un pass del Compliance Officer su un draft specifico (file, snippet, URL). Restituisce semaforo 🟢🟡🔴 + lista issue IVASS/RUI + fix proposti. Usalo prima di promuovere un contenuto sensibile o quando hai dubbi.
argument-hint: [path file | snippet inline tra virgolette]
---

# /compliance-check — Force pass Compliance Officer

## Cosa fa

Esegue il **Compliance Officer** (subagent persona) su un draft specifico, **fuori dal flusso publish**. Utile per:

- Validare un draft prima di passarlo al pubblico
- Rivedere un articolo blog già pubblicato (audit retroattivo)
- Controllare un post LinkedIn scritto a mano dal CEO
- Pre-screenare un commento prima di rispondere

## Sintassi

```
/compliance-check /05_Calendario_editoriale/draft_W21_post_lun.md
/compliance-check "La nostra polizza ti garantisce un rendimento del 4% l'anno"
/compliance-check https://advisoryplus.it/blog/ltc-versilia
/compliance-check ultimo                  → ultimo draft generato dal piano corrente
```

## Skill innescata

`skills/process/compliance/forced-check/SKILL.md` — che a sua volta convoca il subagent `agents/compliance-officer.md`.

## Output formato fisso

```
⚖️ COMPLIANCE CHECK
─────────────────────────────────
Oggetto: [file/snippet/URL]
Voce identificata: [Spiegato Facile | Badvisor | Caso Reale | Analisi]
Canale target: [LinkedIn | IG | Blog | Email | ...]

SEMAFORO: 🟢 / 🟡 / 🟡 / 🔴

ISSUE RILEVATE:
1. [🔴 CRITICA] Claim "rendimento garantito 4%"
   → Vietato IVASS art. 167 + Reg. 41/2018
   → FIX: "il rendimento storico medio è stato del X% (fonte Y, periodo Z) — i rendimenti passati non sono indicativi di quelli futuri"

2. [🟡 ATTENZIONE] Caso reale "Maria" con dettagli identificativi
   → GDPR art. 6
   → FIX: cambiare nome fantasia + età approssimativa + omettere RSA specifica

3. [🟢 OK] Disclaimer RUI presente in footer

ESITO: 🔴 BLOCCO
Procedi solo dopo correzione issue #1.

Nota MM: la versione corretta del claim è già pronta? Vuoi che il Copywriter la rielabori?
```

## Comportamento

- **Mai approvare a metà**: se anche un solo 🔴 → blocco totale
- **Sempre suggerire fix concreti**, non solo "riformulare"
- **Compagnia mandataria check**: se il claim cita "Generali", verifica che sia "Generali Italia – Cattolica Assicurazioni" (denominazione corretta)
- **Logging**: ogni check è loggato in `/03_Aree_di_lavoro/03_Compliance/Log_compliance.md` con timestamp + esito
- **Storico**: `/compliance-check` di un draft già pubblicato → audit storico, non bloccante (loggato, no publish revert)

## Severity guide (per riferimento CEO)

- 🔴 **Blocco**: IVASS hard rule violata (rendimento garantito, denigrazione, prezzo specifico senza contesto, testimonial senza consenso, dato inventato)
- 🟡 **Attenzione**: violazione soft o ambiguità interpretativa (anonimizzazione mancante, tono troppo aggressivo Badvisor, disclaimer omesso su canale che lo richiede)
- 🟢 **OK**: conforme + tono in linea + disclaimer presenti

## Compliance check ≠ Brand check

- Compliance = IVASS/RUI/GDPR/AI Act
- Brand = coerenza voce/posizionamento/Design System

Per brand check usa `marketing:brand-review` (skill esterna del plugin marketing standard).

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
