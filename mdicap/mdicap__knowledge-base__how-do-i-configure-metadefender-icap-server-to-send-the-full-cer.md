<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer -->

# How do I configure MetaDefender ICAP Server to send the full certificate chain on the ICAPS interface?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to MetaDefender ICAP Server v4.8.0 and above releases deployed on Windows and Linux systems.

## [**Summary**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#summary)

The MetaDefender ICAP Server Web Management Console exposes only a single **CERTIFICATE PATH** field and a single **PRIVATE KEY PATH** field when defining a certificate inventory object. There is no separate UI option to "send the intermediate certificate" alongside the server certificate on the ICAPS port.

This is by design. The ICAPS interface is terminated by the embedded Nginx, which follows the standard Nginx convention: the **CERTIFICATE PATH** is expected to be a single PEM file containing the server certificate **and** any intermediate certificate(s), concatenated in order. When that file is provided, the server presents the full chain during the TLS handshake.

This article documents how to build and load that bundled PEM correctly for both standard installations and Kubernetes deployments.

---

## [**Applies to**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#applies-to)

| Item | Value |
| --- | --- |
| Product | MetaDefender ICAP Server |
| Version | 4.8.0 and later (the version where stunnel was removed and TLS became native) |
| Interface | ICAPS port (default `11344`) |
| Deployment | Windows / Linux installs, and Kubernetes via the official Helm chart |

---

## [**Symptom**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#symptom)

The client reports one or more of the following:

- ICAP clients reject the TLS handshake with "unable to verify the first certificate" or "self signed certificate in certificate chain."
- `openssl s_client -connect <icap_host>:11344 -showcerts` shows only the server certificate under the `Certificate chain` section — no intermediate(s).
- The client states that internal applications require the full chain to be presented on the ICAPS port and asks whether there is an option to enable this.

---

## [**Background**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#background)

The ICAPS port is served by an embedded Nginx instance inside MetaDefender ICAP Server. Nginx's `ssl_certificate` directive accepts a single file that holds the server certificate optionally followed by the chain certificates, all in PEM format. The Web Management Console's CERTIFICATE PATH field maps to that directive — there is no second field for intermediates because none is needed at the Nginx level.

If the CERTIFICATE PATH points at a file containing only the server certificate, the chain will not be presented and any client that does not already trust the intermediate locally will fail validation.

---

## [**Resolution**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#resolution)

### [**Option A — Standard install (Windows / Linux), Web Management Console**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#option-a--standard-install-windows--linux-web-management-console)

#### [**1. Build the bundled PEM file**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#1-build-the-bundled-pem-file)

The server certificate must come **first**, followed by the intermediate certificate(s), in order from leaf toward root.

Linux:

cat server.crt intermediate.crt > fullchain.pem

If there are multiple intermediates:

cat server.crt intermediate1.crt intermediate2.crt > fullchain.pem

Windows (PowerShell):

Get-Content server.crt, intermediate.crt | Set-Content fullchain.pem

Or open both files in a text editor and paste the contents into a single `.pem` file in the same order.

Each certificate must remain within its own block, with no extra characters between them:

-----BEGIN CERTIFICATE-----
<server certificate content>
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
<intermediate certificate content>
-----END CERTIFICATE-----

The **PRIVATE KEY PATH** still references the server's private key file — unchanged. The private key is **not** added to `fullchain.pem`.

#### [**2. Place the file where the service can read it**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#2-place-the-file-where-the-service-can-read-it)

Make sure the bundled file is in a location readable by the ICAP Server service user. The certificate inventory object will reference this path.

#### [**3. Load the bundle into the certificate inventory**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#3-load-the-bundle-into-the-certificate-inventory)

In the MetaDefender ICAP Server Web Management Console:

1. Go to **Inventory > Certificates**.
2. Either click **ADD NEW CERTIFICATE** and create a new inventory object, or edit the existing one used for ICAPS.
3. Set **CERTIFICATE PATH** to the new `fullchain.pem` file.
4. Set **PRIVATE KEY PATH** to the server's private key file.
5. Click **ADD** / **SAVE**.

#### [**4. Attach the certificate to the ICAPS interface**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#4-attach-the-certificate-to-the-icaps-interface)

1. Go to **Settings > Security > ICAPS configuration > Details**.
2. In the **CERTIFICATE** field, select the updated certificate inventory object.
3. Click **SAVE SETTINGS**.

The ICAP Server service will restart automatically. The ICAPS interface will be briefly unavailable.

---

### [**Option B — Kubernetes deployment (official Helm chart)**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#option-b--kubernetes-deployment-official-helm-chart)

If the deployment uses the OPSWAT Helm chart for MetaDefender ICAP Server, there is no Web Management Console step. The full chain is supplied through a Kubernetes Secret.

#### [**1. Build the bundled PEM file**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#1-build-the-bundled-pem-file)

Same procedure as in Option A, step 1. Produce `icaps-fullchain.pem`.

#### [**2. Create (or replace) the ICAPS TLS Secret**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#2-create-or-replace-the-icaps-tls-secret)

kubectl create secret generic mdicapsrv-icaps-tls-cert \
--from-file=mdicapsrv-icaps.crt=./icaps-fullchain.pem \
-n <YOUR_MDICAP_NAMESPACE>

The private key Secret remains unchanged:

kubectl create secret generic mdicapsrv-icaps-tls-cert-key \
--from-file=mdicapsrv-icaps.key=./icaps-private.key \
-n <YOUR_MDICAP_NAMESPACE>

If a single Secret is in use (e.g., via cert-manager), make sure the `tls.crt` data key inside that Secret holds the full chain, not the leaf alone.

#### [**3. Confirm** `tls.icaps.enabled: true` **in** `values.yaml`](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#3-confirm-tlsicapsenabled-true-in-valuesyaml)

icap_components:
md_icapsrv:
tls:
icaps:
enabled: true
certSecret: mdicapsrv-icaps-tls-cert
certSecretSubPath: mdicapsrv-icaps.crt
certKeySecret: mdicapsrv-icaps-tls-cert-key
certKeySecretSubPath: mdicapsrv-icaps.key
#### [**4. Apply the change**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#4-apply-the-change)

helm upgrade --install mdicapsrv ./helm_charts/ -n <YOUR_MDICAP_NAMESPACE> -f your-values.yaml

---

## [**Verification**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#verification)

After the service restart, confirm the full chain is being presented from any host that can reach the ICAPS port:

openssl s_client -connect <icap_server_host>:11344 -showcerts

In the output, the **Certificate chain** section at the top should list every certificate in the bundle — server certificate first, then each intermediate, each on its own numbered line (`0 s:... / i:...`, `1 s:... / i:...`, …).

If only entry `0` (the server certificate) appears, the chain is still not being presented and one of the steps above was not applied correctly.

---

## [**Troubleshooting**](/docs/mdicap/knowledge-base/how-do-i-configure-metadefender-icap-server-to-send-the-full-cer#troubleshooting)

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `openssl s_client` still shows only the server certificate | Order of certs in `fullchain.pem` is wrong (root or intermediate placed before the server cert) | Rebuild the file with server cert first, then intermediate(s) toward root |
| Service fails to start, or ICAPS port refuses connections after the change | PEM file has trailing characters, missing `-----END CERTIFICATE-----`, or contains non-PEM (DER) content | Open each source certificate, confirm it is PEM-encoded, and rebuild the bundle |
| Change appears to be saved but client behavior is unchanged | The service was not restarted (e.g., the configuration was saved but the restart prompt was skipped) | Restart the ICAP Server service manually |
| Kubernetes: the pod is still serving the old certificate | The pod was not restarted after the Secret was replaced | Roll the deployment: `kubectl rollout restart deploy/<md-icapsrv-deployment> -n <NS>` |
| Linux: service cannot read the file | File permissions / SELinux | Ensure the service user has read access; check that the file's path is not under a directory the service cannot traverse |

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
