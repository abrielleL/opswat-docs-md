<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/enabling-https -->

# Configuring HTTPS

MetaDefender Storage Security can be configured to support HTTPS communication when accessing the Web UI and REST API.

### Which method applies to your deployment?

| Deployment type | Method |
| ---- | ---- |
| Linux (Docker-based) | CLI — `mdss -u enable_https` |
| Windows (native services) | CLI — `mdss.ps1 -u enable_https` |
| Any (non-Kubernetes) | UI — Settings → Security tab |
| Kubernetes | See the Kubernetes [deployment guide](https://www.opswat.com/docs/mdss/installation/kubernetes-deployment) |

## Enabling HTTPS from the UI

Enabling HTTPS from the UI is now available for non Kubernetes deployments. On the Settings page, under the Security tab, you can enable HTTPS directly from the UI by entering the certificate file and the key file.  The certificate must be a `.crt` file while the key must be a `.key`  file.

After configuring HTTPS from UI, for the configuration to apply, restarting MDSS manually is required using the `mdss` command on Linux or the `mdss.ps1` script on Windows.

![](https://uploads.developerhub.io/prod/k8zL/6prnnsyzvkvlltzkk5gsx89snmgfyznjc8x9jx4abyzrd93r6157k6hxtobldasb.png)

```bash
sudo mdss -c restart
```

```bash
.\mdss.ps1 -c restart
```

## Enabling HTTPS from the Command Line

#### Prerequisites (both platforms)

- Certificate and private key must be in **PEM format** (`.crt` or `.pem` for the cert, `.key` for the key).
- If your certificate chain includes intermediate certificates, concatenate them into the `.crt` file (server cert first, then intermediates).
- Only one `.crt`/`.pem` and one `.key` file may be present in the certificate directory at a time.
- If no certificate is available, skip the certificate placement steps — the script will auto-generate a self-signed certificate (Linux only; Windows requires a certificate to be provided).

> **Info**
>
> **Self-signed certificates**: Browsers will show a trust warning for self-signed certificates. This is expected in lab or internal environments. To suppress the warning, add the certificate to your browser's or OS's trust store.

### Enable HTTPS on Windows-based deployments

In order to setup HTTPS communication please follow these steps:

1. Place your certificate (`.crt` or `.pem`) and key (`.key`) files in: `C:\Program Files\OPSWAT\MetaDefender Storage Security\config\nginx\certificates` The files can have any name — the script renames them to `ssl.crt` and `ssl.key` automatically.
2. Navigate to the scripts folder: `C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts`
3. Open a PowerShell prompt and run:

```plaintext
PS> .\mdss.ps1 -u enable_https
```

4. The script restarts the services automatically. Verify HTTPS is working by navigating to `https://<your-host>:443` (or the port configured in `WEB_PORT_SSL` in your .env file).
5. Verify that HTTPS is configured correctly by navigating with your browser.

### Disable HTTPS on Windows-based deployments

For disabling HTTPS communication please follow these steps:

1. Navigate to the *scripts* folder (by default, in *C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts)*
2. Run the following command in PowerShell:

```powershell
PS> .\mdss.ps1 -u disable_https
```

3. The script patches the nginx configuration and restarts services automatically. The certificate files remain in `config\nginx\certificates` — they are not deleted.

### Enable HTTPS on Unix-based deployments

In order to setup HTTPS communication please follow these steps:

1. Place your certificate (`.crt` or `.pem`) and key (`.key`) files in `/etc/mdss/webclient/` The files can have any name — the script renames them to `ssl.crt` and `ssl.key` automatically.
2. Run:

```plaintext
sudo mdss -u enable_https
```

3. The script reloads nginx automatically — **no MDSS restart is required**. Verify HTTPS is working by navigating to `https://<your-host>:443` (or the port configured in `WEB_PORT_SSL` in your .env file)
4. Verify that HTTPS is configured correctly by navigating with your browser.

### Disable HTTPS on Unix-based deployments

> **Info**
>
> **Note:** Disabling HTTPS on Linux removes the certificate files from `/etc/mdss/webclient/`. Back up your certificates beforehand if needed.

For disabling HTTPS communication, run the following command:

```bash
sudo mdss -u disable_https
```

The script reloads nginx automatically — no restart required.

### Port configuration

By default, MDSS listens on:

- **HTTP**: port `80`
- **HTTPS**: port `443`

If ports 80 or 443 are unavailable, you can change them in your .env file:

```bash
WEB_PORT=8080
WEB_PORT_SSL=8443
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
