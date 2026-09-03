<!-- source: https://www.opswat.com/docs/cm/configurations/secure-connection -->

# Secure Connection

## Requirements

In order to enable HTTPS on My OPSWAT Central Management, a trusted certificate issued by a certificate authority provider or a self-signed certificate along with their private key and password (if needed) files must be provided.

> **Limitation**
>
> To enable HTTPS, switch to a **Custom Domain** or **Proxy URL,** using **IP addresses** is *not* supported**.**

## Using IP Address

For temporary setups or internal networks where security isn't a primary concern. Uses the current IP address of the server (e.g., `http://10.40.160.238`).

![](https://uploads.developerhub.io/prod/97qW/4h86gdjil90hnt9of4sjoupvpy3w16yyuxbbbv2c4iux8ri3g2cpnibyf6lp2owr.png)

## Using Custom Domain

Uses a domain name such as `your-company-domain.com` to access the server securely via HTTPS.

![](https://uploads.developerhub.io/prod/97qW/mngy429q4rv619rie8z4e4q8ockrhu0he5bvnryi3a6eg5zoosnuoql6r90vg1cb.png)

**Steps**:

1. Select the Custom Domain option.
2. Enter your full domain URL (e.g., `https://portal.company.com`).
3. Click on **Update** to upload an SSL certificate.

**Uploading SSL Certificate**

![](https://uploads.developerhub.io/prod/97qW/42fwhe2p7gavom2fayy9kh91np4q3iv6vernjjjxavl19dvv3sv70ynzvp837o85.png)

When prompted to upload a certificate:

- **Certificate (.crt)**: The public certificate file issued by a Certificate Authority.
- **Private Key (.key)**: The private key file that matches the certificate.

✅ After selecting both files, click **Import** to apply them.

⚠️ Ensure that the certificate is valid and matches the domain.

## Using Proxy URL

**Description**: Uses a reverse proxy setup with a specified secure domain (e.g., `https://proxy.company.com`).

![](https://uploads.developerhub.io/prod/97qW/dkg7w2yl9dirdu8b7g65r8ymbayegv9ikwtmb4c4a8jmpf0s0hoqrly31jo5fvzh.png)

**Use case**: Use this option when your system is hosted behind a proxy server that handles HTTPS and routing.

**Step**:

- Enter the full proxy domain in the input field.

> **Tips & Notes**
>
> - To enable HTTPS, you must use a domain or proxy, not an IP address.
> - Ensure DNS is properly configured to point your domain to the server.
> - SSL certificates must be valid and issued for the domain name you use.
> - After any change, remember to Save the configuration and restart services if required.
