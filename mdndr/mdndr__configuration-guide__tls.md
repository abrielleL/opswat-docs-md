<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/tls -->

# TLS

Manager setting (per host). Set a value for each Manager host that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Manager settings → TLS

Set the Transport Layer Security (TLS) trust options for the host. Add a certificate authority (CA) certificate and set the minimum TLS version.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Cert Pem** | PEM-encoded TLS certificate served by the platform gateway. Include the full chain (leaf certificate first, then any intermediates) so clients can build a trust path. Must be accompanied by the matching key_pem. | — | text | — |
| **Key Pem** | PEM-encoded private key matching cert_pem. Write-only: it is stored as a secret and never returned by the configuration API. | — | text | — |

**Related:** [Manager configuration](/docs/mdndr/operating-guide/manager-configuration)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
