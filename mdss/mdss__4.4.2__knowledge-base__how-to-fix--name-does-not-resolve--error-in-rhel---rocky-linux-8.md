<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8 -->

# How to fix 'Name does not resolve' error in RHEL / Rocky Linux 8 with Podman

## [Overview](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#overview)

By default, **Rocky Linux / RHEL 8.x** uses the **CNI DNS plugin** as its container networking DNS backend (most common with Podman + CNI). This can cause services to fail to communicate with the database or external network.

**Rocky Linux / RHEL 9.x** ships with **aardvark-dns** and **netavark**, Podman's modern network stack, which resolves these issues.

Info

**Long-term recommendation: Upgrade to Rocky Linux / RHEL 9.** The steps below are a workaround for systems that cannot yet be upgraded.

## [Temporary solution: Change DNS library](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#temporary-solution-change-dns-library)

Info

⚠️ Note: This procedure requires an active internet connection and must be performed with `sudo` (root) privileges.

### [Step 1: Stop MDSS](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-1-stop-mdss)

BashCopysudo mdss -c stop
### [Step 2 — Install `netavark` and `aardvark-dns`](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-2--install-netavark-and-aardvark-dns)

BashCopysudo dnf install -y netavark aardvark-dns
### [Step 3 — Configure Podman to Use the new network backend](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-3--configure-podman-to-use-the-new-network-backend)

Edit `/etc/containers/containers.conf` and add the following section:

[network]
network_backend = "netavark"
dns_enabled = trueInfo

If the file does not exist, create it at `/etc/containers/containers.conf`.

### [Step 4 — Clean Up Old Podman Configuration](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-4--clean-up-old-podman-configuration)

Remove the old CNI network configuration and restart Podman:

BashCopysudo podman container prune -f
sudo podman network prune -f
sudo rm -rf /etc/cni/net.d/*
sudo rm -rf /var/lib/cni/networks/*
sudo systemctl restart podman
### [Step 5 - Validate the new DNS library is used](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-5---validate-the-new-dns-library-is-used)

Run these commands:

BashCopyecho "Network Backend: $(sudo podman info --format '{{.Host.NetworkBackend}}')"
echo "DNS Packages: $(rpm -qa | grep -E 'dnsname|netavark|aardvark')"

You should see something like this:

BashCopyNetwork Backend: netavark
DNS Packages: aardvark-dns-1.16.0-1.el9.x86_64
### [Step 6 — Start MDSS](/docs/mdss/4.4.2/knowledge-base/how-to-fix--name-does-not-resolve--error-in-rhel---rocky-linux-8#step-6--start-mdss)

BashCopysudo mdss -c start

It should now work as expected.
