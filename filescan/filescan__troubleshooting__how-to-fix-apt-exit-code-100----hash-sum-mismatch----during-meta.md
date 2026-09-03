<!-- source: https://www.opswat.com/docs/filescan/troubleshooting/how-to-fix-apt-exit-code-100----hash-sum-mismatch----during-meta -->

[MetaDefender Aether(Sandbox)](https://www.opswat.com/docs/filescan)Need Help?
# How to fix apt Exit Code 100 “Hash Sum mismatch” during MetaDefender Sandbox upgrade on Ubuntu?

This article applies to all MetaDefender Sandbox releases deployed on Linux Ubuntu systems.

## [When should you use this?](/docs/filescan/troubleshooting/how-to-fix-apt-exit-code-100----hash-sum-mismatch----during-meta#when-should-you-use-this)

`apt update` fails with “Hash Sum mismatch” and the installer exits with code 100.

- Cleaning /var/lib/apt/lists and caches removes stale metadata that causes checksum mismatches.
- Switching mirrors avoids mid-sync index/hash changes.
- Acquire::* options add retries and send cache-control headers to defeat stale proxies.

## [Likely causes](/docs/filescan/troubleshooting/how-to-fix-apt-exit-code-100----hash-sum-mismatch----during-meta#likely-causes)

- Stale APT metadata or cached indexes
- Mirror drift (repository updated mid-sync)
- Caching proxy serving old indexes

## [How to fix](/docs/filescan/troubleshooting/how-to-fix-apt-exit-code-100----hash-sum-mismatch----during-meta#how-to-fix)

1. **Clean APT metadata & caches, then refresh**

`sudo rm -rf /var/lib/apt/lists/*``sudo apt-get clean``sudo apt-get autoclean`

`sudo apt-get update \``-o Acquire::Retries=5 \``-o Acquire::http::No-Cache=true \``-o Acquire::https::No-Cache=true \``-o Acquire::CompressionTypes::Order::=gz`

2. **Switch to a known-good mirror**

Backup sources list `sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak`

Switch archive + security to Azure (choose any stable, close mirror) `sudo sed -Ei 's|http://(archive|security).ubuntu.com/ubuntu|http://azure.archive.ubuntu.com/ubuntu|g' /etc/apt/sources.list`

Refresh after switching mirrors `sudo rm -rf /var/lib/apt/lists/*``sudo apt-get update`

3. **If behind a Proxy, soft-bypass cache for Ubuntu domains**

`sudo apt-get update \``-o Acquire::http::No-Cache=true \``-o Acquire::http::No-Store=true \``-o Acquire::https::No-Cache=true`

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
