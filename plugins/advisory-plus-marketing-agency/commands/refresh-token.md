---
name: refresh-token
description: Pre-flight check delle scadenze token API del sistema marketing Advisory+ (Meta, Gemini, HeyGen, Brevo, LinkedIn). Se entro 7gg dalla scadenza, guida o esegue il refresh. Usalo manualmente o lascia che il cron settimanale lo faccia.
argument-hint: [opzionale: meta | gemini | heygen | brevo | linkedin | all (default all)]
---

# /refresh-token — Token health check & refresh

## Cosa fa

Esegue health check di tutti i token API critici. Per ogni token:

1. Legge `secrets.local.md` + `config/*.env`
2. Verifica scadenza dichiarata
3. Se scadenza > 30gg → 🟢 OK
4. Se scadenza 7-30gg → 🟡 ALERT (comunica scadenza)
5. Se scadenza < 7gg → 🔴 URGENT (guida refresh)
6. Se scaduto → 🔴 BLOCCO (sistema non può più pubblicare su quel canale)

## Sintassi

```
/refresh-token                → check all (default)
/refresh-token meta           → solo Meta
/refresh-token meta gemini    → multipli
/refresh-token meta --execute → check + esegui refresh se possibile
```

## Skill innescata

`skills/process/maintenance/refresh-token/SKILL.md`

## Output formato fisso

```
🔑 TOKEN HEALTH CHECK — 18 mag 2026
─────────────────────────────────

🟢 GEMINI API
   Format: AQ.* v2 bound service account
   Service Account: cc-nano-banana-sa@advisoryplus-marketing-plugin.iam
   Scadenza: nessuna (rotazione 90gg consigliata, prossima 22 ago)
   Stato: OPERATIVO

🟢 META PAGE TOKEN (long-lived)
   App ID: 842859785529983
   Page: Advisory+ (106410181429611)
   IG Business: 17841463441876023
   Scadenza: 17 lug 2026 (60gg)
   Stato: OPERATIVO

🟢 HEYGEN OAuth
   Plan: Creator $24/mese (15 min video/mese)
   Auto-refresh: ✅ via MCP OAuth
   Stato: OPERATIVO

🟢 BREVO API v3
   Scadenza: no expiry
   Stato: OPERATIVO

🟡 LINKEDIN MDP
   Stato: PENDING APPLICATION
   Action richiesta: avviare application su developer.linkedin.com (2-4 settimane approval)

─────────────────────────────────
🟢 4 token OK · 🟡 1 attention · 🔴 0 critici
Prossimo refresh proattivo: 10 lug 2026 (Meta, 7gg pre-scadenza)
```

## Comportamento

### Meta token refresh (procedura)
Quando entro 7gg dalla scadenza:

```
🔴 META TOKEN — REFRESH RICHIESTO ENTRO 7gg

Procedura guidata:
1. Apri https://developers.facebook.com/tools/explorer/
2. Seleziona App: Advisory Plus Marketing Plugin (842859785529983)
3. Genera User Access Token con permission: pages_show_list, pages_manage_posts, pages_read_engagement, pages_manage_metadata, instagram_basic, instagram_content_publish, public_profile
4. Copia il short-lived
5. Vai su https://developers.facebook.com/tools/debug/accesstoken/?q=[TOKEN]
6. Click "Extend Access Token" → long-lived 60gg
7. Incolla nel chat: /refresh-token meta --paste [NEW_TOKEN]

Vuoi che apra Graph API Explorer adesso? [SÌ/NO]
```

### Gemini key rotation (procedura)
Ogni 90gg, alert per rotazione preventiva:

```
🟡 GEMINI KEY — ROTAZIONE CONSIGLIATA (90gg)

Procedura:
1. console.cloud.google.com → APIs & Services → Credentials
2. Seleziona "Plugin AdvisoryPlus - cc-nano-banana"
3. Click "Regenerate key"
4. Conferma → nuova key generata
5. Incolla nel chat: /refresh-token gemini --paste [NEW_KEY]
6. La vecchia key viene revocata automaticamente dopo 7gg di overlap

Vuoi che apra Cloud Console adesso? [SÌ/NO]
```

## Compliance

I token sono **segreti**. Output sempre **mascherato** (mostra solo primi 8 char + ultimi 4):
```
AQ.Ab8R...NeWG (mascherato per security)
```

Il token completo va SOLO in `secrets.local.md` (Nextcloud locale CEO), mai in chat.

## Scheduled task associated

Un cron settimanale (lun 09:00) esegue `/refresh-token` in modalità silent e notifica via email solo se 🟡 o 🔴.

Cron: `0 9 * * 1` → ogni lunedì 09:00

---

*Slash command v1.0 — Plugin Build Sessione 8 — 2026-05-18*
