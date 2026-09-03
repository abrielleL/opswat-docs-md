<!-- source: https://www.opswat.com/docs/mdendpoint/user-guide/how-to-use-urls-allowlisting-in-the-download-protection-feature -->

# How to use URLs Allowlisting in the Download Protection feature?

## What is Allowlisting Download URL?

This feature enables administrators to **specify trusted URLs or domains** from which users can **download internal or approved resources**.

Files downloaded from the allowlisted sources are **automatically trusted** and **exempted from additional scanning**.

## Add an allowlisted URL

1. Go to **Policies** → **Endpoint Security** → **Select an endpoint policy** → **Advanced Endpoint Protection** → **Enable Threat Detection for Windows** → **Secure Download.**
2. Find **Allowlist URLs for File Downloads**
3. Click on the **Add URL** button to enter the value

![](https://uploads.developerhub.io/prod/2x2P/nvzsyg564nnxs350qh5q92adfte3xey9kwldur82g368axv2rah1wh65i1rzwrzb.png)

## Use cases

Choose the most suitable option that satisfies your use case

### Option A — Allowlist a specific domain

Use this when the whole domain is trusted for downloads:

- `*example.com`
- `*downloads.vendor.com`

### Option B — Allowlist a URL using wildcards

![](https://uploads.developerhub.io/prod/2x2P/wl0a0gg8p2i7ve5ulfb5b5ba08evoa7deei48nvqnab2apsjt7ij3eafv1wted0t.png)

### Option C — Allowlist a full URL

Use this when you only want to allow downloads from a specific path:

- `https://samples-files.com/samples/documents/word/sample1.doc`
- `https://ash-speed.hetzner.com/100MB.bin`
