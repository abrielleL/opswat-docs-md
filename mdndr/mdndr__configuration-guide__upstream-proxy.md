<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/upstream-proxy -->

# Upstream proxy

Manager setting (per host). Set a value for each Manager host that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Manager settings → Upstream proxy

Set the outbound proxy for the host. Services that reach the internet use this proxy.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Host** | Upstream Proxy Host. | — | text | Restart needed |
| **Port** | Upstream Proxy Port. | — | number | Restart needed |
| **Username** | Upstream Proxy Username. | *(empty)* | text | Restart needed |
| **Password** | Upstream Proxy Password. | *(empty)* | text | Sensitive (hidden), Restart needed |

**Related:** [Manager configuration](/docs/mdndr/operating-guide/manager-configuration)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
