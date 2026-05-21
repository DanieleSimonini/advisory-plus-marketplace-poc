---
name: refresh-token
description: Pre-flight check delle scadenze token API del sistema marketing Advisory+ (Meta, Gemini, HeyGen, Brevo, LinkedIn, Buffer, WordPress). Se entro 7gg dalla scadenza, guida il refresh con istruzioni step-by-step.
argument-hint: [opzionale: meta | gemini | heygen | brevo | linkedin | buffer | wordpress | all (default all)]
---

# /refresh-token — Check + guida refresh token API

Quando vieni invocato con `/refresh-token $ARGUMENTS`, esegui SUBITO le istruzioni qui sotto. **READ-ONLY su filesystem** — non automatizzi il refresh (richiede credenziali fresh che solo il CEO ha).

## Step 1 — Identifica i token da controllare

Default: tutti. Se `$ARGUMENTS` contiene uno tra `meta`, `gemini`, `heygen`, `brevo`, `linkedin`, `buffer`, `wordpress`, `all` → filtra di conseguenza.

## Step 2 — Leggi tracking scadenze

Path:

```
C:\Users\danie\Nextcloud\Marketing & Communication\ClaudeCoWork_TeamMarketing\04_Risorse\Stato_Sistema\tokens.json
```

Schema atteso:

```json
{
  "meta":      { "type": "long_lived", "obtained_at": "ISO", "expires_at": "ISO", "scopes": ["..."], "notes": "..." },
  "gemini":    { "type": "api_key",     "obtained_at": "ISO", "expires_at": null,  "notes": "API key senza scadenza" },
  "heygen":    { "type": "api_key",     "obtained_at": "ISO", "expires_at": "ISO", "notes": "..." },
  "brevo":     { "type": "api_key",     "obtained_at": "ISO", "expires_at": null,  "notes": "API key v3, no expiry" },
  "linkedin":  { "type": "oauth_user",  "obtained_at": "ISO", "expires_at": "ISO", "scopes": ["..."], "notes": "..." },
  "buffer":    { "type": "oauth_app",   "obtained_at": "ISO", "expires_at": "ISO", "notes": "..." },
  "wordpress": { "type": "app_password","obtained_at": "ISO", "expires_at": null,  "notes": "Application Password, no expiry" }
}
```

Se il file `tokens.json` NON esiste:
- NON crashare
- Mostra header + tabella vuota con "(tracking non inizializzato)" e fermati al Step 5 (skip dei Step 3-4)

## Step 3 — Calcola stato per ogni token

Per ogni token in scope, calcola:

| Campo | Calcolo |
|---|---|
| `giorni_residui` | (`expires_at` - oggi) in giorni. Se `expires_at` null → `∞` |
| `semaforo` | `giorni ≤ 7` → 🔴 · `giorni ≤ 30` → 🟡 · `giorni > 30` → 🟢 · `∞` → 🟢 |
| `azione` | 🔴 = "REFRESH SUBITO" · 🟡 = "Pianifica refresh entro fine settimana" · 🟢 = "OK, nessuna azione" |

## Step 4 — Identifica token urgenti

Marca quelli con `semaforo` 🔴 o 🟡. Per ognuno, prepara la guida refresh (vedi Step 5 mappatura).

## Step 5 — Output: tabella + guide refresh

```
═══════════════════════════════════════════════════
🔑 TOKEN API STATO · Advisory+
oggi: [data IT]
═══════════════════════════════════════════════════

| Servizio  | Tipo          | Residui | Stato | Azione |
|-----------|---------------|---------|-------|--------|
| Meta      | Long-lived    | [N] gg  | 🟢🟡🔴  | [...] |
| Gemini    | API key       | ∞       | 🟢     | OK     |
| HeyGen    | API key       | [N] gg  | 🟢🟡🔴  | [...] |
| Brevo     | API key       | ∞       | 🟢     | OK     |
| LinkedIn  | OAuth user    | [N] gg  | 🟢🟡🔴  | [...] |
| Buffer    | OAuth app     | [N] gg  | 🟢🟡🔴  | [...] |
| WordPress | App password  | ∞       | 🟢     | OK     |

[SE 0 token 🔴/🟡:]
✅ Tutti i token in stato sano. Prossimo check consigliato: tra 7 giorni.

[SE almeno 1 token 🔴 o 🟡:]
⚠️ [N] token richiedono attenzione

[Per ogni token urgente, blocco guida (vedi sotto)]
```

### Guide refresh per servizio

Mostra solo i blocchi dei servizi che richiedono refresh.

**Meta (Facebook + Instagram via Graph API)**

```
🔄 META — Refresh Long-Lived User Access Token (scade ogni 60 giorni)

Step:
1. Vai su https://developers.facebook.com/tools/debug/accesstoken/
2. Login con account admin pagina Advisory+ + account IG business
3. "Generate Token" → seleziona Pagina Advisory+ + IG → copia il token (60gg validi)
4. Aggiorna file: 04_Risorse/Credenziali/secrets.local.md sez. Meta → META_USER_LL_TOKEN
5. Aggiorna 04_Risorse/Stato_Sistema/tokens.json → meta.obtained_at + expires_at (=oggi+60gg)
6. Test smoke: lancia _scratch/smoke_06_meta_buffer.ps1 (o smoke_07_meta_graph.ps1)

Tempo: ~5 min · Frequenza: ogni 60 gg
```

**HeyGen**

```
🔄 HEYGEN — Rotation API Key

Step:
1. Vai su https://app.heygen.com/settings → API
2. "Revoke" la key vecchia (NON farlo prima di averne una nuova!)
3. "Generate new key" → copia
4. Aggiorna secrets.local.md sez. HeyGen → HEYGEN_API_KEY
5. Aggiorna tokens.json → heygen.expires_at (=oggi+365gg, HeyGen non scade ma rotation best practice)

Tempo: ~3 min · Frequenza: ogni 12 mesi (best practice security)
```

**LinkedIn (CEO Daniele personale + Pagina brand)**

```
🔄 LINKEDIN — Refresh Access Token (scade ogni 60 giorni)

NOTA: serve un access token per profilo CEO personale + uno per Pagina brand. Sono separati.

Step (per ciascuno):
1. App https://www.linkedin.com/developers/apps/ → Advisory+ App
2. "Auth tab" → Token in scadenza? "Regenerate access token"
3. Login user owner (CEO per profilo, Page admin per Pagina)
4. Copia nuovo access token
5. Aggiorna secrets.local.md sez. LinkedIn → LINKEDIN_DANIELE_TOKEN / LINKEDIN_PAGE_TOKEN
6. Aggiorna tokens.json → linkedin.expires_at (=oggi+60gg)
7. Test smoke: lancia _scratch/smoke_05_buffer_linkedin.ps1 + smoke_03/04 LinkedIn

Tempo: ~10 min totali · Frequenza: ogni 60 gg
```

**Buffer**

```
🔄 BUFFER — Refresh OAuth App Token

Buffer GraphQL token può durare a lungo, ma in caso di revoca o errore HTTP 401:
1. Login su https://buffer.com → Settings → Apps
2. Re-authorize l'app Advisory+ (se disconnessa)
3. Console GraphQL: rigenera Personal Access Token
4. Aggiorna secrets.local.md sez. Buffer → BUFFER_ACCESS_TOKEN
5. Aggiorna tokens.json → buffer.expires_at

Tempo: ~5 min · Frequenza: on-demand (no scadenza fissa)
```

**Gemini, Brevo, WordPress**

```
ℹ️ Senza scadenza naturale (API key permanenti o app passwords). Rotation best-practice ogni 12 mesi.
```

## Vincoli di stile

- **NO scrittura su tokens.json o secrets.local.md** — il CEO esegue manualmente i passi
- **NO domande di follow-up** — output, basta
- **NO uso di tool Skill** — self-contained
- **Lunghezza output adattiva**: solo header + tabella se tutto verde (~15 righe), aggiungi guide solo per servizi che le richiedono

## Edge case

- `tokens.json` malformato → mostra "🟡 tokens.json malformato — controlla manualmente o reinizializza" e fermati
- Tutti i token con `expires_at` null → mostra ∞ ovunque, nessuna guida, output corto

---

*Slash command v1.1 — refactor Sessione 22 — 2026-05-21 — istruzione imperativa self-contained, READ-ONLY.*
