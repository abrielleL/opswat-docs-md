<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-does-metadefender-storage-security-intermittently-show--lice -->

# Why Does MetaDefender Storage Security Intermittently Show "License Information Is Not Available" on RHEL 8?

> **Check Your Version:**
>
> This article applies to MetaDefender Storage Security deployments on **Red Hat Enterprise Linux (RHEL) 8** using Podman with the **CNI network backend**.

## Issue

Users may intermittently see the following warning in the MetaDefender Storage Security dashboard:

> **Some functionality is disabled because there is a communication issue and license information is not available.**

The warning may disappear after refreshing the dashboard and reappear later.

When this issue occurs, MetaDefender Storage Security services may also intermittently lose communication with the local PostgreSQL database.

For example, the licensing service log may contain an error similar to:

```plaintext
An error occurred using the connection to database 'MDSS'
on server 'tcp://postgres:5432'.
```

Similar database communication or name resolution errors may also appear in other MDSS service logs.

## Main Cause

MetaDefender Storage Security consists of multiple containerized services that communicate with each other using internal hostnames.

On some RHEL 8 environments, Podman uses the legacy **CNI network backend** for container networking and DNS resolution. An intermittent DNS resolution issue may prevent an MDSS service from resolving another container hostname, such as `postgres`.

For example, if the licensing service temporarily cannot resolve the `postgres` hostname, communication with the database is interrupted. The licensing service is then unable to retrieve the required license information, causing MDSS to display the warning in the dashboard.

Once DNS resolution is restored, communication resumes. As a result, the warning may disappear after refreshing the dashboard and reappear when another DNS resolution failure occurs.

This behavior is related to the container networking and DNS environment and does not necessarily indicate an issue with the MDSS license itself.

> **Note:** The warning message alone does not confirm this issue. Other conditions, such as database availability, resource exhaustion, or connectivity issues, may cause similar symptoms.

### Confirm the Podman Network Backend

Run the following command:

```plaintext
sudo podman info --format '{{.Host.NetworkBackend}}'
```

If the output is:

```plaintext
cni
```

the system is using the CNI network backend.

You can also check the installed container networking and DNS packages:

```bash
rpm -qa | grep -E 'dnsname|netavark|aardvark'
```

If the system is using the CNI backend and the MDSS service logs show intermittent database communication or DNS resolution errors, proceed with the resolution below.

## Resolution

### Recommended Long-Term Solution: Upgrade to RHEL 9

For the most stable long-term solution, we recommend upgrading the MDSS host operating system from **RHEL 8 to RHEL 9**.

RHEL 9 uses Podman's newer **netavark** network backend together with **aardvark-dns** by default. This newer networking stack handles the container networking and DNS resolution required for communication between MDSS services and avoids the intermittent CNI DNS behavior described in this article.

Before upgrading, review the supported operating systems and system requirements for your MetaDefender Storage Security version and plan the migration according to your organization's change management requirements.

### Workaround for RHEL 8

If upgrading to RHEL 9 is not currently possible, you can address this issue on the existing RHEL 8 environment by switching Podman's network backend from **CNI** to **netavark + aardvark-dns**.

For detailed instructions, please refer to the following article:

[How to Fix 'Name Does Not Resolve' Error in RHEL / Rocky Linux 8 with Podman](https://www.opswat.com/docs/mdss/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8)

**Note:** This procedure requires restarting MetaDefender Storage Security, which will cause a temporary service interruption. We recommend taking an appropriate system backup or snapshot before applying the workaround.

> **Support:**
>
> If further assistance is required, please [create a support case or chat with our support engineer.](https://my.opswat.com/portal/support-services)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
