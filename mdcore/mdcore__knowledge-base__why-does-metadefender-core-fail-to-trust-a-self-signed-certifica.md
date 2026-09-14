<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica -->

# Why does MetaDefender Core fail to trust a self-signed certificate in Kubernetes?

When MetaDefender Core connects to an HTTPS application, it validates the SSL/TLS certificate presented by the remote endpoint. If that application uses a self-signed certificate, or a certificate issued by an internal Certificate Authority that MetaDefender Core does not trust, the connection can fail during certificate validation.

A typical error looks similar to this:

[WARNING] 2026.07.14 10:15:28.608: (common.communication) SSL error,
error='The certificate is self-signed, and untrusted',
errorCode='"The certificate is self-signed, and untrusted"' [msgid: 497]

This article explains why the error occurs and how to configure MetaDefender Core running in Kubernetes to trust the required certificate by mounting it into the container from a Kubernetes Secret.

Use the correct certificate for the trust relationship. If the remote application is truly self-signed, use that certificate. If the remote application was issued by a private or internal CA, trust the relevant CA certificate or chain instead of trusting only the leaf certificate.

# [**Symptoms**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#symptoms)

You may observe one or more of the following:

- MetaDefender Core cannot connect to an HTTPS application that uses a self-signed or privately issued certificate.
- Logs show an SSL/TLS validation failure stating that the certificate is self-signed and untrusted.
- Connectivity tests to the same endpoint succeed only when certificate validation is bypassed outside MetaDefender Core.

# [**Resolution**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#resolution)

To make MetaDefender Core trust the certificate in Kubernetes, store the certificate in a Kubernetes Secret and mount it into the MetaDefender Core pod as a file.

## [**1. Select the correct certificate**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#1-select-the-correct-certificate)

Choose the certificate based on how the remote endpoint was issued:

- **Self-signed endpoint certificate:** use that self-signed certificate.
- **Certificate issued by an internal or private CA:** use the applicable CA certificate, which may include the root CA and one or more intermediate CA certificates.

The remote application should also present the full chain during the TLS handshake where applicable.

## [**2. Prepare the certificate file**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#2-prepare-the-certificate-file)

Ensure the certificate file meets these requirements:

- PEM format
- `.crt` file extension
- Contains only the public certificate data
- Does not include the private key

A PEM certificate normally looks like this:

-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----

In the example below, the file name is `selfsigned.crt`.

## [**3. Create the Kubernetes Secret**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#3-create-the-kubernetes-secret)

Create a Secret in the same namespace where MetaDefender Core is deployed:

kubectl create secret generic selfsigned \
--from-file=selfsigned.crt=./selfsigned.crt \
--namespace <mdcore-namespace>

In this command, `selfsigned.crt=./selfsigned.crt` means:

- `selfsigned.crt` before the equals sign is the key name stored in the Secret.
- `./selfsigned.crt` after the equals sign is the local file path.

You can verify the Secret contents with either of the following commands:

kubectl get secret selfsigned \
--namespace <mdcore-namespace> \
-o jsonpath='{.data}'kubectl get secret selfsigned \
--namespace <mdcore-namespace> \
-o json | jq -r '.data | keys[]'

The output should include `selfsigned.crt`.

## [**4. Mount the Secret into the MetaDefender Core pod**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#4-mount-the-secret-into-the-metadefender-core-pod)

Update the MetaDefender Core Helm values to define an extra volume sourced from the Secret:

extraVolumes:
- name: selfsigned
secret:
secretName: selfsigned
items:
- key: selfsigned.crt
path: selfsigned.crt

Then mount that file into the container:

extraVolumeMounts:
- name: selfsigned
mountPath: /etc/ssl/certs/selfsigned.crt
subPath: selfsigned.crt
readOnly: true

Complete example:

extraVolumes:
- name: selfsigned
secret:
secretName: selfsigned
items:
- key: selfsigned.crt
path: selfsigned.crt
extraVolumeMounts:
- name: selfsigned
mountPath: /etc/ssl/certs/selfsigned.crt
subPath: selfsigned.crt
readOnly: true

**Additional mount required for LDAP/AD directory connections:** The mount path `/etc/ssl/certs/selfsigned.crt` is sufficient for most MetaDefender Core HTTPS features. However, the **Add directory** feature with type **LDAP/AD** reads certificates from the system CA bundle file rather than individual `.crt` files in the directory. If you use LDAP/AD directory integration with a self-signed or internally issued certificate, you must also mount the certificate into the system CA bundle path. See Step 4a below.

## [**4a. Additional mount for LDAP/AD directory connections**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#4a-additional-mount-for-ldapad-directory-connections)

MetaDefender Core's LDAP/AD directory feature validates certificates against the system CA bundle file rather than scanning individual certificate files in `/etc/ssl/certs/`. If you configure an LDAP/AD directory that uses a self-signed or privately issued certificate, the certificate must also be present in the system CA bundle.

The relevant CA bundle path depends on the container base image:

| Container base image | CA bundle path |
| --- | --- |
| CentOS / RHEL (primary for MetaDefender Core) | `/etc/pki/tls/certs/ca-bundle.crt` |
| Debian / Ubuntu | `/etc/ssl/certs/ca-certificates.crt` |

The Secret key name, the `items[].key` value, the `items[].path` value, and the `subPath` value must match the intended mounted filename. If they do not match, Kubernetes can fail the mount with an error such as `references non-existent secret key`.

## [**5. Apply the Helm change**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#5-apply-the-helm-change)

Apply the updated values using the Helm upgrade command used in your environment. Example:

helm upgrade <release-name> <chart-name> \
--namespace <mdcore-namespace> \
--reuse-values \
-f values.yaml

If the values were updated but the pod was not recreated yet, restart the deployment:

kubectl rollout restart deployment/<mdcore-deployment> \
--namespace <mdcore-namespace>

Then monitor rollout progress:

kubectl rollout status deployment/<mdcore-deployment> \
--namespace <mdcore-namespace>

## [**6. Verify the certificate mount**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#6-verify-the-certificate-mount)

After the new pod starts, confirm the file exists in the container.

kubectl get pods --namespace <mdcore-namespace>kubectl exec \
--namespace <mdcore-namespace> \
<mdcore-pod-name> \
-- ls -l /etc/ssl/certs/selfsigned.crt

The file should be present at `/etc/ssl/certs/selfsigned.crt`.

## [**7. Test the connection again**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#7-test-the-connection-again)

Retry the MetaDefender Core connection to the remote HTTPS application. After the certificate is mounted correctly and the pod is running with the updated configuration, the previous SSL error should no longer appear.

You can also test directly:

kubectl exec \
--namespace <mdcore-namespace> \
<mdcore-pod-name> \
-- curl -v https://<application-hostname>:<port>/

Use the same hostname and port that MetaDefender Core uses. This is important because TLS hostname validation depends on the server name used for the connection.

# [**Important considerations**](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-trust-a-self-signed-certifica#important-considerations)

- **Virtual machine deployments:** if MetaDefender Core is installed directly on a VM instead of Kubernetes, add the certificate to the operating system trust store, restart the MetaDefender Core service, and test again.
- **Use of Secrets vs ConfigMaps:** a public certificate or CA certificate does not normally contain sensitive material, so a ConfigMap can also be technically valid for distribution. A Secret may still be preferred to align with internal security policy or deployment standards.
- **subPath behavior:** mounting a single file with `subPath` preserves the rest of the existing `/etc/ssl/certs` directory. This avoids replacing the whole directory with only Secret contents.
- **Certificate updates:** when a Secret-backed file is mounted using `subPath`, updates are not automatically reflected inside an already running container. Restart the pod or rollout the deployment after certificate changes.
- **LDAP/AD directory trust path:** the LDAP/AD directory feature in MetaDefender Core reads from the system CA bundle file, not from individual files in `/etc/ssl/certs/`. If you use LDAP/AD with a self-signed or internal CA certificate, follow Step 4a to mount the certificate into the CA bundle path.
- **Private key handling:** do not include the certificate's private key in the trust file. Trust configuration requires only the public certificate or CA certificate.

**FAQ: Can I use a ConfigMap instead of a Secret for the certificate?**

> Yes, for a public certificate or CA certificate, a ConfigMap is generally technically sufficient because the content is not normally confidential. However, many organizations standardize on Secrets for certificates, and MetaDefender Core can use either pattern if the file is mounted correctly.

**FAQ: What certificate should I use if the remote server certificate was issued by an internal CA?**

> Use the relevant CA certificate or certificate chain rather than trusting only the leaf server certificate. In many environments that means the root CA certificate and, if applicable, one or more intermediate CA certificates.

**FAQ: Why does the LDAP/AD directory connection still fail after mounting the certificate?**

> The **Add directory** feature with type **LDAP/AD** reads the system CA bundle file, `/etc/pki/tls/certs/ca-bundle.crt` on CentOS/RHEL or `/etc/ssl/certs/ca-certificates.crt` on Debian, rather than individual `.crt` files in `/etc/ssl/certs/`. Ensure the certificate is appended to the CA bundle as described in Step 4a. Restart the pod after making changes.

**FAQ: Will the certificate update automatically if I replace the Secret?**

> Not reliably when the file is mounted via `subPath`. Restart or recreate the pod after updating the Secret so the new certificate file is picked up.

**FAQ: What if MetaDefender Core is installed on a virtual machine instead of Kubernetes?**

> Install the certificate into the operating system trust store used by that host, restart the MetaDefender Core service, and then test the HTTPS connection again.
