<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand -->

# Why does MDSS installation might fail with “net/http: TLS handshake timeout” when pulling Docker containers?

This article applies to all MDSS releases deployed as a Docker Image.

## [Overview](/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand#overview)

During first start or installation, **MetaDefender Storage Security (MDSS)** pulls multiple Docker images from Docker Hub’s CDN (`production.cloudflare.docker.com`). In some environments, this process fails with errors like:

failed to copy: httpReadSeeker: failed open: failed to do request:
Get "https://production.cloudflare.docker.com/registry-v2/docker/registry/v2/blobs/sha256/...":
net/http: TLS handshake timeout
[emergency] Cannot pull containers

Key observations from the affected systems:

- DNS, ping and `curl` tests to Docker Hub and Cloudflare all worked (TLS handshakes succeeded).
- Pulling **one MDSS image at a time** with `docker pull opswat/<image>:<tag>` worked.
- The error occurred **only when MDSS tried to pull many images in parallel**.

Conclusion: the network itself was healthy, but **too many concurrent image downloads** caused some TLS handshakes to time out (combination of Docker’s defaults, CDN behavior, and/or network limits). This is consistent with Docker’s documented behavior where reducing `max-concurrent-downloads` stabilizes image pulls under load.

---

## [Resolution](/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand#resolution)

### [1. Reduce Docker’s concurrent downloads](/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand#1-reduce-dockers-concurrent-downloads)

**Goal:** Force Docker to pull layers sequentially (or with lower parallelism), reducing pressure on the network and avoiding TLS handshake timeouts.

1. Create or edit /etc/docker/daemon.json on the MDSS host:

{
"max-concurrent-downloads": 1
}

You can later tune this to `2` or `3`, but using `1` is the safest starting point to verify the fix. Docker’s `max-concurrent-downloads` is an officially documented setting controlling concurrent layer downloads.

2. Restart Docker:

`sudo systemctl restart docker`

3. Re-run the MDSS start/activation:

`./mdss.sh -c start`

### [2. Optional: Re-try with a modest concurrency value](/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand#2-optional-re-try-with-a-modest-concurrency-value)

If installation works with `1` but you want faster future upgrades:

1. Adjust `daemon.json`, for example:

{
"max-concurrent-downloads": 2
}

2. Restart Docker and test an image pull or a service update.

If timeouts reappear, reduce back to 1.

### [3. Verify network devices (optional but recommended)](/docs/mdss/4.4.2/knowledge-base/why-does-mdss-installation-might-fail-with----net-http--tls-hand#3-verify-network-devices-optional-but-recommended)

Even with reduced concurrency, it is good practice to verify with the network team that:

- No firewall, IDS/IPS, or TLS-inspection device is limiting or throttling HTTPS connections to:

  - `registry-1.docker.io`
  - `production.cloudflare.docker.com`
- There are no strict connection or rate limits for outbound HTTPS from that host.

Many Docker handshake timeout reports involve some interaction between Docker’s parallel pulls and upstream devices, so confirming this can help avoid future issues.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
