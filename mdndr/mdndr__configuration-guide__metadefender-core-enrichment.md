<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/metadefender-core-enrichment -->

# MetaDefender Core enrichment

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → MetaDefender Core enrichment

Scan files that the sensor carves from network traffic. Use MetaDefender Cloud or an on-premises MetaDefender Core deployment.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable this enrichment service. | On | on/off | — |
| **Delete After Scan** | Delete source files after successful scanning. | On | on/off | — |
| **Delete Only Clean Files** | Only delete files that scanned clean (no threats). | Off | on/off | — |
| **Storage Enabled** | Enable saving scanned files to long-term S3/MinIO storage. | Off | on/off | — |
| **Storage Only Threats** | Only store files containing threats. | Off | on/off | — |
| **MetaDefender Mode** | MetaDefender deployment mode. | `cloud` | `cloud`, `core` | Restart needed |
| **Metadefender Cloud Api Key** | API key for MetaDefender Cloud. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Metadefender Cloud Base Url** | MetaDefender Cloud API base URL. | `https://api.metadefender.com/v4` | text; up to 2083 characters | Restart needed |
| **Metadefender Core Api Key** | API key for MetaDefender Core. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Metadefender Core Base Url** | On-premise MetaDefender Core API base URL. | — | text | Restart needed |
| **Metadefender Archive Scan Enabled** | Enable archive extraction during scanning (sends archive password header to MetaDefender). | Off | on/off | — |
| **Metadefender Archive Password** | Password to use for encrypted archive extraction. | `infected` | text | Sensitive (hidden) |
| **Metadefender File Submission Enabled** | Enable actual file submission to MetaDefender. | On | on/off | — |
| **Metadefender Hash Lookup First** | Check hash cache before submitting file for scanning. | On | on/off | — |
| **Metadefender Max Concurrent Scans** | Maximum concurrent scan operations. | `5` | number; 1 to 50; unit: scans | — |
| **Metadefender Max File Size Mb** | Maximum file size in megabytes for scanning (0 = unlimited). | `100` | number; 0 to 36500; unit: megabytes | — |
| **Metadefender Poll Interval Ms** | Milliseconds between poll requests when waiting for scan results. | `30000` | number; 500 to 3600000; unit: milliseconds | — |
| **Metadefender Poll Max Attempts** | Maximum number of poll attempts before giving up on a scan. Combined with metadefender_poll_interval_ms this caps the total time mdcore waits for a MetaDefender scan to complete. | `120` | number; 1 to 10000 | — |
| **Metadefender Rescan After Days** | Rescan if cached result older than N days (0 disables age-based rescan). | `3` | number; 0 to 36500; unit: days | — |
| **Metadefender Skip Mime Types** | MIME types to skip (exact match). | *(empty)* | list of string | — |
| **Metadefender Skip Mime Type Prefixes** | MIME type prefixes to skip. | *(empty)* | list of string | — |
| **Proxy Mode** | Service-level proxy mode: inherit the global upstream proxy, disable proxy use, or use this service's custom proxy settings. | `inherit` | `inherit`, `disabled`, `custom` | Restart needed |
| **Proxy Host** | Custom proxy host for this service when proxy_mode is custom. | — | text | Restart needed |
| **Proxy Port** | Custom proxy port for this service when proxy_mode is custom. | — | number | Restart needed |
| **Proxy Username** | Optional username for the custom service-level proxy. | — | text | Restart needed |
| **Proxy Password** | Optional password for the custom service-level proxy. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy No Proxy** | Hosts, domains, or CIDR ranges that should bypass the custom service-level proxy. | *(empty)* | list of string | Restart needed |
| **Metadefender Core Username** | Username for MetaDefender Core authentication. | *(empty)* | text | Restart needed |
| **Metadefender Core Password** | Password for MetaDefender Core authentication. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Metadefender Scan Rule** | MetaDefender scan profile/rule to use for file submissions. | *(empty)* | text | — |
| **Metadefender Timeout Upload Seconds** | Timeout in seconds for MetaDefender file upload operations. | `120` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Timeout Poll Seconds** | Timeout in seconds for MetaDefender scan result poll requests. | `30` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Timeout Login Seconds** | Timeout in seconds for MetaDefender Core login requests. | `10` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Timeout Hash Lookup Seconds** | Timeout in seconds for MetaDefender hash lookup requests. | `30` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Timeout Api Info Seconds** | Timeout in seconds for MetaDefender API info/reachability requests. | `10` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Retry Attempts** | Maximum attempts for transient MetaDefender request failures. This controls request retries and is separate from scan result polling. | `5` | number; 1 to 100 | — |
| **Metadefender Retry Delay Seconds** | Delay in seconds between transient MetaDefender request retry attempts. This controls retry backoff timing and is separate from poll interval timing. | `60` | number; 1 to 3600; unit: seconds | — |
| **Metadefender Rate Limit Enabled** | Enable concurrency limiting for MetaDefender scan operations. | On | on/off | — |
| **File Source Type** | Where MDCore retrieves carved files for file submission. | `local` | `local`, `s3` | — |
| **File Source Local Path** | Base path for locally carved files. | `/opt/ndr/extracted-files` | text | — |
| **File Mount Path** | Optional dedicated mount path for carved files. | — | text | — |
| **File Source S3 Bucket** | S3/MinIO bucket containing carved source files. | — | text | — |
| **File Source S3 Endpoint** | S3/MinIO endpoint URL for carved source files. | — | text | — |
| **File Source S3 Path Prefix** | Optional S3 key prefix for carved source files. | *(empty)* | text | — |
| **Storage S3 Bucket** | S3/MinIO bucket for long-term scanned file storage. | — | text | — |
| **Storage S3 Endpoint** | S3/MinIO endpoint URL for long-term scanned file storage. | — | text | — |
| **Storage S3 Path Prefix** | S3 key prefix for long-term scanned file storage. | `files/` | text | — |
| **Storage Sharding Strategy** | How scanned files are organized in long-term storage. | `sha256-prefix-2` | `none`, `sha256-prefix-2`, `sha256-prefix-4`, `date`, `date-sha256` | — |

**Related:** [MetaDefender Core file scanning](/docs/mdndr/operating-guide/metadefender-core-file-scanning) · [Integrations](/docs/mdndr/operating-guide/integrations)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
