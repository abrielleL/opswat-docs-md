<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/manager-ntp -->

# NTP (Manager)

Manager setting (per host). Set a value for each Manager host that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Manager settings → NTP

Set the Network Time Protocol (NTP) servers that keep the host clock accurate. Accurate time is necessary for correct alerts and logs.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Ntp Server 1 Host** | NTP Server I. | — | text | Required, Restart needed |
| **Ntp Server 1 Key** | NTP Server I Key. | — | text | Required, Sensitive (hidden), Restart needed |
| **Ntp Server 2 Host** | NTP Server II. | — | text | Required, Restart needed |
| **Ntp Server 2 Key** | NTP Server II Key. | — | text | Required, Sensitive (hidden), Restart needed |
| **Ntp Client Password** | NTP Client Password. | — | text | Required, Sensitive (hidden), Restart needed |

**Related:** [Manager configuration](/docs/mdndr/operating-guide/manager-configuration)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
