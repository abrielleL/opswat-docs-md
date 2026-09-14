<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/sensor-ntp -->

# NTP (sensor)

Sensor setting (per sensor). Set a value for each sensor that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Sensor settings → NTP

Set the Network Time Protocol (NTP) servers for the sensor. Accurate time keeps sensor data aligned with the Manager.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Ntp Server 1 Host** | NTP Server I. | — | text | Required, Restart needed |
| **Ntp Server 1 Key** | NTP Server I Key. | — | text | Required, Sensitive (hidden), Restart needed |
| **Ntp Server 2 Host** | NTP Server II. | — | text | Required, Restart needed |
| **Ntp Server 2 Key** | NTP Server II Key. | — | text | Required, Sensitive (hidden), Restart needed |
| **Ntp Client Password** | NTP Client Password. | — | text | Required, Sensitive (hidden), Restart needed |

**Related:** [Sensor management](/docs/mdndr/operating-guide/sensor-management)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
