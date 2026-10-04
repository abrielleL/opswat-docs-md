<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/advanced-usages/ocm-https-certificates-self-signed -->

# OCM Uses a Standalone Self-Signed Certificate

This section shows how to generate a **self‑signed server certificate** (without an intermediate/root CA chain).

In production, a self‑signed certificate is **not recommended** and is usually replaced by a certificate issued by your internal PKI or a public CA. The examples below are intended for **testing or lab environments** only.

### [1. Generate a Self‑Signed Server Certificate](/docs/mddrive/v4.4.9/advanced-usages/ocm-https-certificates-self-signed#1-generate-a-selfsigned-server-certificate)

In this scenario, the server certificate is self‑signed and acts as its own CA. There is no separate root CA or intermediate CA.

`openssl genrsa -out server.key 2048`

`openssl req -x509 -new -key server.key -sha256 -days 825 \ -out server.crt \ -subj "/CN=myserver.local"`

This creates:

- `server.key` – private key used by the server
- `server.crt` – self‑signed server certificate (no chain)

> In a real deployment, replace `myserver.local` with the actual FQDN of your OCM server.
>
> ### [2. Use the Self‑Signed Certificate for OCM](/docs/mddrive/v4.4.9/advanced-usages/ocm-https-certificates-self-signed#2-use-the-selfsigned-certificate-for-ocm)
>
> After generating and verifying the self‑signed certificate:
>
> - Use `server.key`
> - Use `server.crt`
>
> to configure the TLS/HTTPS certificate on your **OCM on‑prem server**.
