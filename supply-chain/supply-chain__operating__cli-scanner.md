<!-- source: https://www.opswat.com/docs/supply-chain/operating/cli-scanner -->

# CLI Scanner

## MDSSC Scanner Docker Container

The MDSSC Scanner is a lightweight Docker container that enables you to scan files and directories remotely using the MetaDefender Software Supply Chain (MDSSC) API, without requiring UI access.

This makes it ideal for CI/CD pipelines, automated scanning, and command-line workflows.

### Prerequisites

- Docker installed and running
- MDSSC server URL
- MDSSC API key (see [Configuring an API Key](https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key))
- Docker image: `opswat/mdssc-scanner:latest`

### Quick Start

#### Scan a Single File

```bash
FILE="package-lock.json"

docker run --rm \
  -e MDSSC_SERVER="your-mdssc-url" \
  -e MDSSC_API_KEY="your-api-key" \
  -v $(pwd)/$FILE:/scan/$FILE \
  opswat/mdssc-scanner \
  /scan/$FILE
```

> **Warning**
>
> - **API Key Security**: Never commit API keys to version control. Use environment variables or secret management systems in CI/CD pipelines.
> - **File Size Limits**: Large files may take longer to scan. Adjust `SCAN_TIMEOUT`  accordingly.
> - **Network Access**: The container requires network access to communicate with your MDSSC server.

#### Scan all files in a directory

```bash
DIR="project-folder"

docker run --rm \
  -e MDSSC_SERVER="your-mdssc-url" \
  -e MDSSC_API_KEY="your-api-key" \
  -v $(pwd)/$DIR:/scan \
  opswat/mdssc-scanner:latest
```

#### Environment Variables

| Variable | Required | Default | Description |
| ---- | ---- | ---- | ---- |
| `MDSSC_SERVER` | Yes | -  | Your MDSSC server URL (e.g., `https://mdssc.com` ) |
| `MDSSC_API_KEY` | Yes | -  | API key for authentication |
| `WORKFLOW_ID` | No | -  | Specific workflow ID to use for scanning |
| `SCAN_TIMEOUT` | No | `300` | Maximum time to wait for scan completion (seconds) |
| `POLL_INTERVAL` | No | `5` | Interval between status checks (seconds) |
| `FAIL_ON_VULNERABILITIES` | No | `false` | Exit with error code 2 if vulnerabilities found |
| `VULNERABILITY_THRESHOLD` | No | `high` | Minimum severity to fail on:`critical` , `high` , `medium`, `low` |

## Configuring direct-upload size limits (API + nginx)

Direct-file uploads are bounded by two limits that must agree:

- **API limit**: `DIRECT_FILE_UPLOAD_SIZE_MB`
- **Web server limit (nginx)**: `client_max_body_size`

### 1) Set the API limit

To change the API limit, edit `/etc/mdssc/customer.env` and set the maximum file size (in MB) for direct uploads:

```bash
DIRECT_FILE_UPLOAD_SIZE_MB=2048
```

Default: **2048 MB (2 GB)**.

### 2) Ensure nginx allows the same (or higher) limit

Ceiling for the default flow: **2 GB**. The bundled nginx config caps `/api/v1/scans/direct` and `/api/v1/monitored-files` at `client_max_body_size 2048M`, so files larger than 2 GB are rejected with **HTTP 413** even if `DIRECT_FILE_UPLOAD_SIZE_MB` is set higher.

To allow uploads larger than 2 GB, you must also raise the nginx limit. Edit `/etc/mdssc/webclient/default.conf` and set `client_max_body_size` on the `/api/v1/scans/direct` and `/api/v1/monitored-files` locations to match your `DIRECT_FILE_UPLOAD_SIZE_MB` (for example, `4096M`).

After changing either value, restart the MDSSC service for the new configuration to take effect:

```bash
mdssc -c restart
```

Always align these values with your organization's requirements and security policies.
