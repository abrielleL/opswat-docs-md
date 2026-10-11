<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8 -->

# How to fix 'Name does not resolve' error in RHEL / Rocky Linux 8 with Podman

## Overview

By default, **Rocky Linux / RHEL 8.x** uses the **CNI DNS plugin** as its container networking DNS backend (most common with Podman + CNI). This can cause services to fail to communicate with the database or external network.

**Rocky Linux / RHEL 9.x** ships with **aardvark-dns** and **netavark**, Podman's modern network stack, which resolves these issues.

> **Info**
>
> **Long-term recommendation: Upgrade to Rocky Linux / RHEL 9.** The steps below are a workaround for systems that cannot yet be upgraded.

## Temporary solution: Change DNS library

> **Info**
>
> ⚠️ Note: This procedure requires an active internet connection and must be performed with `sudo` (root) privileges.

### Step 1: Stop MDSS

```bash
sudo mdss -c stop
```

### Step 2 — Install `netavark` and `aardvark-dns`

```bash
sudo dnf install -y netavark aardvark-dns
```

### Step 3 — Configure Podman to Use the new network backend

Edit `/etc/containers/containers.conf` and add the following section:

```plaintext
[network]
network_backend = "netavark"
dns_enabled = true
```

> **Info**
>
> If the file does not exist, create it at `/etc/containers/containers.conf`.

### Step 4 — Clean Up Old Podman Configuration

Remove the old CNI network configuration and restart Podman:

```bash
sudo podman container prune -f
sudo podman network prune -f
sudo rm -rf /etc/cni/net.d/*
sudo rm -rf /var/lib/cni/networks/*
sudo systemctl restart podman
```

### Step 5 - Validate the new DNS library is used

Run these commands:

```bash
echo "Network Backend: $(sudo podman info --format '{{.Host.NetworkBackend}}')"
echo "DNS Packages: $(rpm -qa | grep -E 'dnsname|netavark|aardvark')"
```

You should see something like this:

```bash
Network Backend: netavark
DNS Packages: aardvark-dns-1.16.0-1.el9.x86_64
```

### Step 6 — Start MDSS

```bash
sudo mdss -c start
```

It should now work as expected.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
