<!-- source: https://www.opswat.com/docs/supply-chain/configuration/custom-configuration -->

# Custom Configuration

## How to edit the configuration file on Linux

Custom application configuration can be achieved by editing the ***customer.env***  environment file.

The following steps are required to change different parameters in this file:

- Navigate to ***/etc/mdssc/customer.env*** and open the file
- If the parameter that needs to be changed is not present, add the new parameter with the desired value. If it already exists, just edit the value.

```bash
CONFIGURATION_PROPERTY_NAME=VALUE
```

- Save the file
- In order for the changes to apply, please restart the application by running the following command:

```bash
sudo mdssc -c restart
```

## Changing certificate validation

This environment variable controls certificate validation for **MetaDefender** **Software Supply chain** integrations during HTTP(S) requests. It is useful when comes  the needing to accept a partially valid certificate chain or a self-signed certificate.

```bash
MD_CORE_CERTIFICATE_VALIDATION=VALUE
```

`VALUE` can be one of the following:

- **Default** → Invalid certificate instances can't be integrated into MetaDefender Software Supply Chain
- **IgnoreChainErrors** → Instances with certificate chain errors can be integrated
- **IgnoreAllErrors** → Instances with invalid certificate can be integrated

## Showing Direct Upload Scans in Results

When enabled, direct file upload scans are included in connection views and scan results.

Default value to this environment variable is **true**.

```bash
MDSSC_INCLUDE_DIRECT_SCANS_IN_VIEWS=true
```

## Saving Archive Scan Results

When enabled, scan results for archive contents are stored for later access, default value is **true**.

```bash
STORE_ARCHIVE_SCAN_RESULTS=true
```

## Waiting for Archive Extraction to Complete

When enabled, the scan process waits until archive extraction is fully completed before continuing. Default value is **true**.

```bash
SCAN_WAITS_FOR_ARCHIVE_COMPLETION=true
```

## Waiting for External Processing to Finish

When enabled, the scan process waits for external processing to complete before finalizing. Default value is **true**.

```bash
SCAN_WAITS_FOR_EXTERNAL_PROCESSING=true
```

## How Connection Status Is Kept Up to Date

Sets the interval, in milliseconds, for sending heartbeat signals over SignalR connections. This value is also used to throttle status updates for cross-domain transfers.

Default value is **2000 ms**.

```bash
MDSSC_HEARTBEAT_INTERVAL_MS=2000
```

## Archive Scan Performance Mode

When enabled, archive scanning prioritizes speed over detailed inventory results (thinner file inventory inside archives).

Default value is **false**.

```bash
ARCHIVE_PERFORMANCE_MODE=false
```

Use this if archive scans feel slow. Setting `ARCHIVE_PERFORMANCE_MODE=true` typically makes results arrive noticeably faster, with the trade-off of less detailed archive contents.

## Maximum Concurrent Discoveries

Controls scan parallelism by allowing more discovery jobs to run at the same time.

Default value is **4**.

```bash
MDSSC_MAX_CONCURRENT_DISCOVERIES=4
```

Use this if small scans wait behind one large scan. Increase the value to process more scans in parallel, but ensure you have enough CPU and memory headroom.

## RabbitMQ Scanning Prefetch Count

Controls scan message throughput by defining how many scan messages a worker can prefetch and hold at once.

Default value is **30**.

```bash
RABBITMQ_SCANNING_PREFETCH_COUNT=30
```

Use this if overall scan throughput is low on strong hardware. Increase the value to let workers pick up more scan work at once. If the system becomes overloaded, lower it instead.

## Temporary Archive Retention (Seconds)

Controls how long temporary extracted archive files are kept before cleanup.

Default value is **3600** seconds.

```bash
SCAN_TMP_ARCHIVE_RETENTION_SECONDS=3600
```

Use this if disk fills up during heavy archive scanning. Lower the value to clean up temporary extracted files sooner.

## Number of Trusted Proxies

Sets how many proxies in front of the application are trusted to report the client's IP address.

Default value is **1**.

```bash
TRUSTED_PROXY_HOPS=1
```

Use this if MetaDefender Software Supply Chain sits behind a load balancer or ingress. Set the value to 2. Otherwise all users share the load balancer's address and are rate-limited together.

Behind a TLS-terminating load balancer or ingress, you must also set [Allowed Origins](https://www.opswat.com/docs/supply-chain/configuration/custom-configuration#allowed-origins), because `TRUSTED_PROXY_HOPS` alone does not cover the Origin check.

## Allowed Origins

Sets the browser origins that may open real-time SignalR connections to `/api/v1/hubs/*` and enables HTTP CORS for the same origins. Use a comma-separated list of origins in `scheme://host[:port]` format.

Default value is empty. With an empty value, the API accepts only same-origin requests by comparing the browser Origin with the scheme, host and port it sees itself.

For a single origin:

```bash
ALLOWED_ORIGINS=https://mdssc.example.com
```

For multiple origins:

```bash
ALLOWED_ORIGINS=https://mdssc.example.com,https://mdssc-secondary.example.com
```

Use this when a load balancer, reverse proxy or Kubernetes ingress terminates TLS and forwards plain HTTP to MDSSC. The browser sends an `https://` Origin, but the API sees `http`, so the Origin check fails.

On Linux, set `ALLOWED_ORIGINS` in `/etc/mdssc/customer.env`, then apply it:

```bash
sudo mdssc -u update
```

For Kubernetes, set `ALLOWED_ORIGINS` in the `helm_charts/mdssc` chart `values.yaml`. The default is `""`.

If the value is missing or wrong, `/api/v1/hubs/cross-domain-transfer/negotiate` returns HTTP 403. The Cross Domain Transfer Activity Log stays empty and shows a connection error. Other features continue to work because they use REST.

To verify the value, sign in and open the browser developer tools Network tab. The `/api/v1/hubs/cross-domain-transfer/negotiate` request returns HTTP 200 when the value is correct and HTTP 403 when it is missing or wrong.

Installs that serve HTTPS themselves with `sudo mdssc -u enable_https`, or use plain HTTP without a TLS proxy, need no change.

> **Note:** The following limits apply to source code repositories, which are downloaded as ZIP archives. Sizes are given in B, KB, MB, GB or TB, where 1 KB = 1024 bytes. A repository that exceeds a limit is not scanned, and the reason appears in the Scan failed message on its report page.

## Maximum Archive Download Size

Sets the largest repository archive that can be downloaded for scanning. The download stops as soon as the archive exceeds this size.

Default value is **5GB**.

```bash
MDSSC_ARCHIVE_MAX_DOWNLOAD_SIZE=5GB
```

## Maximum Archive Extracted Size

Sets the largest total size a repository archive can expand to when it is extracted.

Default value is **10GB**.

```bash
MDSSC_ARCHIVE_MAX_EXTRACTED_SIZE=10GB
```

Use this if a repository fails to scan because its archive expands beyond the maximum extracted size. Raise the value to allow larger repositories, making sure the host has enough free disk space.

## Maximum Archive File Count

Sets the largest number of files and folders a repository archive can contain.

Default value is **100000**.

```bash
MDSSC_ARCHIVE_MAX_ENTRY_COUNT=100000
```

Use this if a repository fails to scan because its archive contains too many files. Raise the value to allow repositories with more files.

## Maximum Archive Expansion Factor

Sets how many times larger than its compressed size a repository archive can become when extracted.

Default value is **1000**.

```bash
MDSSC_ARCHIVE_MAX_EXPANSION_FACTOR=1000
```

Use this if a repository with highly compressible content fails to scan because it exceeds the expansion factor. Raise the value to allow it.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
