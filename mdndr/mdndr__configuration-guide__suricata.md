<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/suricata -->

# Suricata

Sensor setting (per sensor). Set a value for each sensor that needs a different value. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Sensor settings → Suricata

Control the Suricata detection engine on the sensor. The section shows the engine on/off switch and the connection settings (endpoint, port, protocol, and TLS) at the top, then the advanced engine settings below. Change the advanced settings only if you understand the effect.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Default-Log-Dir** | Advanced setting for this service. Change only if you understand the effect. | `/opt/ndr/logs/suricata` | text | Restart needed |
| **Classification-File** | Advanced setting for this service. Change only if you understand the effect. | `/opt/ndr/config/suricata/classification.config` | text | Restart needed |
| **Reference-Config-File** | Advanced setting for this service. Change only if you understand the effect. | `/opt/ndr/config/suricata/reference.config` | text | Restart needed |
| **Default-Rule-Path** | Advanced setting for this service. Change only if you understand the effect. | `/opt/ndr/config/suricata/rules` | text | Restart needed |
| **Rule-Files** | Advanced setting for this service. Change only if you understand the effect. | `["*.rules"]` | list of string | Restart needed |
| **Threshold-File** | Advanced setting for this service. Change only if you understand the effect. | `/opt/ndr/config/suricata/threshold.config` | text | Restart needed |
| **Vars** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Runmode** | Advanced setting for this service. Change only if you understand the effect. | `workers` | text | Restart needed |
| **Max-Pending-Packets** | Advanced setting for this service. Change only if you understand the effect. | `65534` | number; 1 to no maximum | Restart needed |
| **Default-Packet-Size** | Advanced setting for this service. Change only if you understand the effect. | `1514` | number; 68 to no maximum | Restart needed |
| **Logging** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Af-Packet** | Advanced setting for this service. Change only if you understand the effect. | `[{"interface": "ens18", "threads": 8, "cluster-id": 77, "cluster-type": "cluster_flow", "defrag": true, "use-mmap": true, "tpacket-v3": true, "ring-size": 100000, "block-size": 262144, "batchcount": 100, "disable-promisc": false, "checksum-checks": "no", "checksum-checks-offload": true, "mmap-locked": true, "use-emergency-flush": true}]` | list of SuricataCaptureInterface | Restart needed |
| **Pf-Ring** | Advanced setting for this service. Change only if you understand the effect. | — | list of SuricataCaptureInterface | Restart needed |
| **Stats** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **App-layer** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **File-extraction** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Stream** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings; unit: bytes | Restart needed |
| **Flow** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings; unit: bytes | Restart needed |
| **Detection-engine** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Threading** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Outputs** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | `[{"eve-log": {"community-id": true, "community-id-seed": 0, "enabled": true, "filename": "/var/run/suricata/suricata.sock", "filetype": "unix_stream", "prefix": "", "types": [{"stats": {"deltas": false, "threads": false, "totals": true}}, {"alert": {"http": false, "http-body": true, "http-body-printable": true, "metadata": true, "packet": true, "payload": true, "payload-buffer-size": 4096, "payload-printable": true, "ssh": false, "tagged-packets": true, "tls": false}}, {"files": {"enabled": true, "force-hash": ["md5", "sha256"], "force-magic": true}}, {"flow": {"enabled": true}}, {"netflow": {"enabled": true}}, {"http": {"body": false, "body-printable": false, "enabled": true, "extended": true}}, {"dns": {"answer": false, "enabled": true, "extended": true, "full": false, "query": false}}, {"tls": {"enabled": true, "extended": true}}, {"ftp": {"enabled": true}}, {"smb": {"enabled": true, "full": false}}, {"ssh": {"enabled": true, "full": false}}, {"smtp": {"enabled": true, "extended": false}}, {"quic": {"enabled": true, "extended": true}}, {"modbus": {"enabled": false}}, {"dnp3": {"enabled": false}}, {"enip": {"enabled": false}}, {"s7comm": {"enabled": false}}, {"bacnet": {"enabled": false}}, {"iec104": {"enabled": false}}]}}, {"stats": {"append": true, "enabled": true, "filename": "/opt/ndr/logs/suricata/stats.log", "threads": false, "totals": true}}, {"file-store": {"dir": "/opt/ndr/extracted-files", "enabled": true, "force-filestore": false, "max-size": 104857600, "version": 2, "waldo": "file.waldo", "write-fileinfo": true}}]` | list of groups | Restart needed |
| **Unix-command** | Advanced setting for this service. Change only if you understand the effect. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |

#### [Suricata: SuricataConfigVariables sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigvariables-sub-settings)

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Home-Net** | Advanced setting for this service. Change only if you understand the effect. | `["192.168.0.0/16", "10.0.0.0/8", "172.16.0.0/12"]` | list of string | — |
| **External-Net** | Advanced setting for this service. Change only if you understand the effect. | `["!$HOME_NET"]` | list of string | — |
| **Address-Groups** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Port-Groups** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |

#### [Suricata: SuricataLoggingConfig sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataloggingconfig-sub-settings)

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Default Log Level** | Advanced setting for this service. Change only if you understand the effect. | `Notice` | `Emergency`, `Alert`, `Critical`, `Error`, `Warning`, `Notice`, `Info`, `Debug` | — |
| **Outputs** | Advanced setting for this service. Change only if you understand the effect. | `[{"enabled": true}, {"enabled": true, "level": "Info", "filename": "suricata.log"}, {"enabled": false, "facility": "local5"}]` | list of item | — |

#### [Suricata: SuricataConfigStats sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigstats-sub-settings)

*Top-level stats: block configuration.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Advanced setting for this service. Change only if you understand the effect. | On | on/off | — |
| **Interval** | Advanced setting for this service. Change only if you understand the effect. | `15` | number | — |

#### [Suricata: SuricataConfigAppLayer sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigapplayer-sub-settings)

*Application layer configuration for protocol parsing .. note:: DNS, SMTP, and other protocols are enabled by default in Suricata v8 while OT protocol parsers are off by default and must be explicitly enabled.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Protocols** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |

#### [Suricata: SuricataConfigFileExtraction sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigfileextraction-sub-settings)

*Top-level file-extraction: block. Controls whether Suricata extracts files from parsed protocol streams and which hashes/metadata to compute. This is distinct from the file-store output which controls where carved files are written to disk (see :class:SuricataConfigFileStore). Canonical shape:: file-extraction: enabled: yes force-magic: yes force-hash: [md5, sha256].*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Advanced setting for this service. Change only if you understand the effect. | On | on/off | — |
| **Force-Magic** | Advanced setting for this service. Change only if you understand the effect. | On | on/off | — |
| **Force-Hash** | Advanced setting for this service. Change only if you understand the effect. | `["md5", "sha256"]` | list of string | — |

#### [Suricata: SuricataConfigStream sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigstream-sub-settings)

*Stream reassembly configuration for full protocol parsing.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Memcap** | Advanced setting for this service. Change only if you understand the effect. | `4 GiB` | text | — |
| **Depth** | Advanced setting for this service. Change only if you understand the effect. | `8 MiB` | text | — |
| **Reassembly** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |

#### [Suricata: SuricataConfigFlow sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigflow-sub-settings)

*Flow engine configuration for connection tracking.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Memcap** | Advanced setting for this service. Change only if you understand the effect. | `4 GiB` | text | — |
| **Hash-Size** | Advanced setting for this service. Change only if you understand the effect. | `524288` | number; 1024 to no maximum | — |
| **Prealloc** | Advanced setting for this service. Change only if you understand the effect. | `50000` | number; 0 to no maximum | — |
| **Emergency-Recovery** | Advanced setting for this service. Change only if you understand the effect. | `20` | number; 1 to 100 | — |

#### [Suricata: SuricataConfigDetectionEngine sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigdetectionengine-sub-settings)

*Detection engine configuration for rule matching.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Profile** | Advanced setting for this service. Change only if you understand the effect. | `high` | text | — |
| **Sgh-Mpm-Algo** | Advanced setting for this service. Change only if you understand the effect. | `ac` | text | — |

#### [Suricata: SuricataConfigThreading sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigthreading-sub-settings)

*Threading configuration for high traffic environments.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Thread-Init-Timeout** | Advanced setting for this service. Change only if you understand the effect. | `300` | number; 0 to no maximum | — |
| **Set-Cpu-Affinity** | Advanced setting for this service. Change only if you understand the effect. | Off | on/off | — |
| **Detect-Thread-Ratio** | Advanced setting for this service. Change only if you understand the effect. | `1.5` | number; 0.1 to 10.0 | — |
| **Cpu-Affinity** | Advanced setting for this service. Change only if you understand the effect. | — | list of object | — |

#### [Suricata: SuricataConfigOutput sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigoutput-sub-settings)

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Eve-log** | Advanced setting for this service. Change only if you understand the effect. | — | group of settings | — |
| **Stats** | Advanced setting for this service. Change only if you understand the effect. | — | group of settings | — |
| **File-store** | Advanced setting for this service. Change only if you understand the effect. | — | group of settings | — |

#### [Suricata: SuricataConfigUnixCommand sub-settings](/docs/mdndr/configuration-guide/suricata#suricata-suricataconfigunixcommand-sub-settings)

*Unix command socket for runtime control.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Advanced setting for this service. Change only if you understand the effect. | On | on/off | — |
| **Filename** | Advanced setting for this service. Change only if you understand the effect. | `/var/run/suricata/suricata-command.socket` | text | — |

**Related:** [Suricata signatures](/docs/mdndr/operating-guide/suricata-signatures)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
