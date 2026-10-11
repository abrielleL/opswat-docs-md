<!-- source: https://www.opswat.com/docs/mdss/4.5.2/getting-started/general-system-requirements -->

# General System Requirements

This page outlines the necessary prerequisites for deploying MetaDefender Storage Security (MDSS), covering supported operating systems, system requirements, and specific details for Unix and Windows deployments.

Operating system-specific system requirements are available at:

- [Unix deployment](https://www.opswat.com/docs/mdss/getting-started/unix-deployment)
- [Windows deployment](https://www.opswat.com/docs/mdss/getting-started/windows-deployment)

## Prerequisites

## **Hardware Configurations**

Depending on your deployment type, please ensure your hardware meets the following minimum requirements:

### Basic Deployment (Minimum System Requirements)

| Hardware | MDSS Dedicated Instance | MDSS + MD Core Shared Instance |
| ---- | ---- | ---- |
| CPU | 16 cores (vCPUs) | 32 cores (vCPUs) |
| RAM | 32 GB | 64 GB |
| Free Disk Space | 500 GB* | 900 GB* |

### Advanced Deployment (Minimum System Requirements)

For advanced usage, particularly when you intend to process a very large number of files, it is not recommended to run MD Core on the same machine as MDSS.

| Hardware | MDSS Dedicated Instance | PostgreSQL Database Instance |
| ---- | ---- | ---- |
| CPU | 16 cores (vCPUs) | 16 cores (vCPUs) |
| RAM | 32 GB | 32 GB |
| Free Disk Space | 150 GB* | 380 GB* |

## *** Disk Space Planning (applicable to all deployments)**

> **Info**
>
> Please note that the database disk space requirements outlined in this document are calculated based on processing **10 million files***.
>
> **Important:** If you anticipate discovering and processing more than 10 million files, you will need to allocate additional disk space for the database proportionally.
>
> The disk space requirements for the application and logs remain constant regardless of the number of files processed.
>
> If you need assistance calculating the appropriate database disk size for your specific file volume, please don't hesitate to reach out.
>
> *Each file discovery creates a separate database entry, even if it's the same file.

Careful disk space planning is crucial for the optimal performance and reliability of the MetaDefender Storage Security platform.

- Base Installation (database excluded):
  - MDSS Application: **20 GB**
  - Default install path:
    - Windows: `C:\Program Files\OPSWAT\MetaDefender Storage Security`
    - Linux: `/etc/mdss`
- Operational Requirements
  - A minimum of **100 GB** is recommended for **log retention and analysis**
    - Default install path:
      - Windows:
        - `C:\Program Files\OPSWAT\MetaDefender Storage Security\logs`
        - `C:\Windows\System32\opswat.mdss.windows.service`
        - Installer logs: `C:\Users\<user>\AppData\Local\Temp\`
      - Linux: `/var/log/mdss` and `/etc/mdss/sevices_logs`
  - For the various MDSS services (database included), an additional **380 GB** is required
    - Default install path:
      - Windows: `C:\Program Files\OPSWAT\MetaDefender Storage Security\services`
      - Linux: `/etc/mdss`
- This heavily depends on the actual dataset and configuration in a production environment.
- More details on the exact logging paths can be found at [Logs location](https://www.opswat.com/docs/mdss/where-to-get-help/log-location)

Note: Insufficient disk space may negatively impact system performance and reliability, particularly during high-volume remediation operations. Regular monitoring of disk usage is strongly advised to ensure optimal system performance.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
