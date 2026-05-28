---
name: publish-linkedin-socio
description: Pubblicazione automatica LinkedIn profilo personale soci Advisory+ (Agostini, Fappani, Barrella, e anche Daniele con nuovo workflow post-2026-05-28) gated da email-approvazione. Trigger post-Friday Email del venerdi 18:00 quando il piano contiene almeno 1 post LinkedIn personale di un socio. Sequenza - (a) MM invia email da `marketing@advisoryplus.it` a `nome.cognome@advisoryplus.it` (mail personale del socio) con draft completo del post + invito a rispondere in linguaggio naturale (no parola chiave rigida) - (b) Polling IMAP ogni 2h fino a publish OR Friday Email successiva (timeout naturale ~7gg) - (c) Interpretazione LLM dell'intent della reply (OK / MODIFICA + istruzione / RINVIA / STOP / ambiguo) - (d) Su OK = publish via API LinkedIn `/v2/ugcPosts` con token specifico del socio (file `04_Risorse/Stato_Sistema/linkedin_tokens_[socio].json`) + email conferma con permalink - (e) Su MODIFICA = ri-elabora draft + ri-invia email (max 3 round) - (f) Su RINVIA = sposta al pillar-of-month successivo - (g) Su STOP = archivia in `99_Archivio/post_LI_personali_non_pubblicati/` - (h) Su silenzio fino a Friday W+1 = rinvio mese successivo con nota in Friday W+1. Parser autorita sul singolo draft = solo il socio destinatario puo decidere sul proprio post (reply da altri sender auto-respinte). Codifica formalmente la revoca della decisione CEO 16 mag "click finale del socio" sostituita da "OK email approvazione + MM esegue publish via API" (decisione CEO 2026-05-28, Big Bet Brand Book v1.2 addendum v1.3 sez. 13.5-bis).
---
# Skill publish-linkedin-socio — Pubblicazione automatica LinkedIn personale soci con email-approvazione

> **Workflow: MM propone draft via email -> socio risponde in linguaggio naturale -> MM interpreta intent + esegue publish o re-elaborazione o archiviazione. Mai publish forzato senza OK esplicito.**

---

## 1. Quando triggera

- **Automatico**: subito dopo l'invio della **Friday Email del venerdi 18:00** se il piano della settimana successiva contiene almeno 1 post LinkedIn personale di un socio (Agostini / Fappani / Barrella / Daniele).
- **Bloccata** se `config/AUTOMAZIONE_ATTIVA = false` (kill switch globale) -> MM produce solo draft Markdown e notifica al CEO manualmente.

---

## 2. Output finale atteso

Per ogni post LinkedIn personale socio nel piano:

1. **Email approvazione** inviata via Brevo SMTP da `marketing@advisoryplus.it` a `nome.cognome@advisoryplus.it`
2. **Post pubblicato** via LinkedIn API `/v2/ugcPosts` con token del socio (solo dopo OK del socio)
3. **Email conferma** con permalink + screenshot al socio (post-publish)
4. **Log** in `05_Calendario_editoriale/Post_LI_soci/[YYYY-MM-DD]_[socio]_log.md`

---

## 3. Struttura email approvazione

**Subject**: `[Advisory+] Approvazione post LinkedIn settimana W[NN] - [titolo breve]`

**Sender**: `marketing@advisoryplus.it`
**Destinatario**: `nome.cognome@advisoryplus.it` (mail personale del socio, **non** `commerciale@`)

**Body**:

```
Ciao [Nome],

Per la settimana W[NN] il piano editoriale include un post LinkedIn a tuo
nome sul pillar P[X] [titolo pillar].

DRAFT PROPOSTO:

---
[testo completo del post, max 1.300 caratteri LinkedIn]
---

Per autorizzare la pubblicazione, rispondi a questa email in linguaggio
naturale. Esempi:

  - "OK pubblica" / "vai pure" / "mi piace, manda"     -> pubblico subito
  - "modifica: rendi piu diretto il primo paragrafo"   -> ri-elaboro + ri-invio
  - "non ora, rimandiamo al mese prossimo"             -> rinvio slot mese successivo
  - "no, archivia"                                      -> archivio draft

Se non ricevo risposta entro venerdi prossimo 18:00 il post viene rinviato
al pillar-of-month successivo (nessuna pubblicazione forzata).

Compliance check: gate-doppio gia passato (Compliance Officer + Brand
Strategist). Pillar di pertinenza assegnato in base a Brand Book sez. 11.4
ratio 80/20.

A presto,
- Marketing Manager Advisory+ (sistema automatico)
```

---

## 4. Polling reply socio

- **Frequenza**: ogni 2 ore via Cloud Scheduler GCP (free tier)
- **Inbox**: `marketing@advisoryplus.it` (IMAP `mail.advisoryplus.it:993 SSL`)
- **Filtro**: thread email approvazione del singolo post (Message-ID tracking)
- **Stop condizioni** (qualsiasi delle 2):
  1. Pubblicazione avvenuta (= OK socio + publish API riuscita + log)
  2. Invio della Friday Email successiva (= ~7 giorni elapsed, timeout naturale)

---

## 5. Parser autorita sul draft

Solo il **socio destinatario** della singola email approvazione e autorizzato a decidere sul proprio post.

| Sender della reply | Comportamento MM |
|---|---|
| Socio destinatario (es. `alberto.fappani@advisoryplus.it` per post Fappani) | OK — interpreta intent |
| Altri 3 soci | Auto-reply: "Solo [nome socio destinatario] puo decidere su questo post. Inoltragli osservazioni se vuoi siano applicate." |
| Sender sconosciuto | Notifica MM + escalation CEO |

---

## 6. Interpretazione LLM intent (linguaggio naturale, no parola chiave)

| Intent | Esempi reply socio | Azione MM |
|---|---|---|
| **OK** | "OK", "approvato", "vai", "pubblica", "d'accordo", "mi piace, manda" | Publish immediato via API + email conferma con permalink |
| **MODIFICA + istruzione** | "modifica: rendi piu diretto", "cambia: aggiungi un esempio concreto", "rivedi: il claim sul ROI e troppo forte" | Ri-elabora draft applicando istruzione + ri-invia email approvazione. Max 3 round prima di escalation CEO. |
| **RINVIA** | "non ora", "rimandiamo", "la prossima settimana", "mese prossimo" | Rinvia slot al pillar-of-month successivo + nota nel calendario editoriale |
| **STOP** | "no", "non mi convince", "archivia", "lascia perdere", "scarta" | Archivia draft in `99_Archivio/post_LI_personali_non_pubblicati/` + nota nel Verbale chat 02 LinkedIn |
| **Ambiguo / non parseabile** | qualsiasi reply non chiara | Auto-reply: "Non ho capito il tuo intent. Puoi chiarire? OK pubblica / MODIFICA + istruzione / RINVIA / STOP." + notifica MM |

---

## 7. Publish API LinkedIn

**Endpoint**: `POST https://api.linkedin.com/v2/ugcPosts`

**Auth**: `Authorization: Bearer [access_token]` dal file token del socio:
- Daniele: `10_Plugin_Advisory_Plus_Build/secrets.local.md` sez. LinkedIn Developer App
- Fappani: `04_Risorse/Stato_Sistema/linkedin_tokens_fappani.json`
- Agostini: `04_Risorse/Stato_Sistema/linkedin_tokens_agostini.json`
- Barrella: `04_Risorse/Stato_Sistema/linkedin_tokens_barrella.json`

**Pre-check**: legge `tokens.json` per verificare `expires_at` > now. Se < 7gg da scadenza, notifica MM con istruzione rinnovo OAuth (`setup-linkedin-socio-token.ps1 -SocioName [Nome]`).

**Body** (UGC Post API):

```json
{
  "author": "urn:li:person:[socio_urn]",
  "lifecycleState": "PUBLISHED",
  "specificContent": {
    "com.linkedin.ugc.ShareContent": {
      "shareCommentary": { "text": "[testo post]" },
      "shareMediaCategory": "NONE"
    }
  },
  "visibility": { "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC" }
}
```

**Post-publish**:
- Estrai `id` dalla response (es. `urn:li:share:1234567890`)
- Costruisci permalink: `https://www.linkedin.com/feed/update/[id]/`
- Screenshot via Chrome MCP (opzionale, post-MVP)
- Email conferma al socio: "Post live: [permalink]"
- Log in `05_Calendario_editoriale/Post_LI_soci/[YYYY-MM-DD]_[socio]_log.md`

---

## 8. Timeout: silenzio fino a Friday W+1

Se a Friday W+1 18:00 il socio non ha risposto:

1. Rinvia il post al pillar-of-month successivo (calendario editoriale)
2. Nota nella Friday Email W+1: "Post LinkedIn [socio] su pillar P[X] rinviato per silenzio (non risposta entro 7gg)"
3. NESSUN publish forzato. Conservatore.

---

## 9. Eccezioni

### Token scaduto / 401 LinkedIn API
- Notifica MM via email Brevo: "Token [socio] scaduto, rinnovo necessario"
- Email al socio: "Per pubblicare devo rinnovare l'autorizzazione LinkedIn. Daniele te lo chiedera nel prossimo Friday Email."
- Archivia draft in pending fino a rinnovo token

### Rate limit LinkedIn API
- Retry con backoff esponenziale (max 3 tentativi: 60s, 300s, 1800s)
- Se fallisce tutti i retry: notifica MM + archivia in pending

### Modalita Ferie / Crisi
- Skill bloccata: NESSUN invio email approvazione
- Draft restano in pending fino a riattivazione

---

## 10. Cosa NON fare

- NON pubblicare senza OK esplicito del socio destinatario. Mai. Anche se "sembra ovvio" che il socio approverebbe.
- NON inviare email approvazione a `commerciale@advisoryplus.it` (= sender wrong, alias gruppo). Deve essere mail personale del singolo socio.
- NON applicare reply al draft da socio diverso dal destinatario (es. Fappani non puo decidere su un post di Agostini).
- NON forzare publish per silenzio. Rinvio mese successivo e la regola.
- NON modificare il draft senza istruzione esplicita del socio (su MODIFICA serve istruzione, no auto-modifica).
- NON pubblicare se compliance check post-modifica diventa rosso. Re-loop su Compliance Officer prima.

---

## 11. Workflow tech reference

**Script PowerShell associato**: `04_Risorse/Stato_Sistema/scripts/publish-linkedin-socio.ps1` (cron lanciato da Cloud Scheduler GCP)

**Trigger**: post-Friday Email del venerdi (subito dopo invio SMTP `strategia-week-fri`)

**Cloud Scheduler entry**: `linkedin-socio-polling` (frequency `0 */2 * * 5-7,1`, timezone Europe/Rome)

**File di stato per ogni post pending**: `04_Risorse/Stato_Sistema/li_socio_pending/[YYYY-MM-DD]_[socio]_[hash].json` con campi `socio`, `pillar`, `draft_versions[]`, `email_sent_at`, `last_poll_at`, `status` (`pending` | `modifica_round_N` | `published` | `archived` | `timeout`).

---

## 12. Riferimenti incrociati

- Brand Book v1.2 sez. 13.5 + addendum v1.3 (workflow LinkedIn soci formalizzato)
- File addendum canonico: `03_Aree_di_lavoro/09_Brand_Identity/Output_approvati/2026-05-28_brand_book_addendum_v1.3_friday_email_protocol_evoluto.md`
- Skill `publish-linkedin-daniele` (deprecata 2026-05-28, sostituita da questa skill anche per Daniele con nuovo workflow OK email)
- Memoria persistente: `reference_friday_email_protocol_v1_3` + `reference_linkedin_developer_app`
- Token LinkedIn soci: `04_Risorse/Stato_Sistema/linkedin_tokens_*.json` + `tokens.json`
- Config IMAP/SMTP: `10_Plugin_Advisory_Plus_Build/secrets.local.md` + `config/email.env`
- Brevo API per invio email approvazione: `reference_brevo_setup_advisoryplus`

---

*Plugin v1.1.8 - Skill creata 2026-05-28 a seguito Big Bet Brand Book v1.2 addendum v1.3 sez. 13.5-bis - rilasciata in plugin v1.1.8 Sessione 24 chat 10 stesso giorno*
