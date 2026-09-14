<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/smtp -->

# SMTP

Manager setting (per host). Set a value for each Manager host that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Manager settings → SMTP

Set the Simple Mail Transfer Protocol (SMTP) server that the system uses to send email notifications.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Host** | SMTP Host. | — | text | Required, Restart needed |
| **Port** | SMTP Port. | — | number; 1 to 65535 | Required, Restart needed |
| **Username** | SMTP Username. | — | text | Required, Restart needed |
| **Password** | SMTP Password. | — | text | Required, Sensitive (hidden), Restart needed |
| **From Address** | SMTP From Address. | — | text | Required, Restart needed |
| **To Address** | SMTP To Address. | — | text | Required, Restart needed |
| **Reply To Address** | SMTP Reply-to Address. | — | text | Required, Restart needed |
| **Tls Enabled** | SMTP TLS Enabled? | — | on/off | Required, Restart needed |

**Related:** [Manager configuration](/docs/mdndr/operating-guide/manager-configuration)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
