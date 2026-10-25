<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-can-icap-be-configured-to-handle-https-traffic-in-squid-vers -->

# How can ICAP be configured to handle HTTPS traffic in Squid version 7.x?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version**
This article applies to MetaDefender ICAP Server releases deployed on Windows and Linux systems.

## [**Overview**](/docs/mdicap/v5.15.0/knowledge-base/how-can-icap-be-configured-to-handle-https-traffic-in-squid-vers#overview)

After successfully compiling and installing Squid v7 [How to self compile Squid v7 to work with ICAP on Ubuntu Linux? - MetaDefender ICAP Server](https://www.opswat.com/docs/mdicap/knowledge-base/how-to-self-compile-squid-v7-to-work-with-icap-on-ubuntu-linux-2#download-latest-squid-v7-release), additional configuration is required to properly handle HTTPS traffic.

By default, Squid cannot inspect HTTPS traffic unless SSL Bump is configured. This KB provides step-by-step instructions to:

- Generate a Certificate Authority (CA)
- Use the CA as the SSL Bump signing certificate
- Trust the CA on client machines
- Initialize the SSL database
- Enable SSL Bump
- Integrate with ICAP

> **Important:** When `generate-host-certificates=on` is used, Squid signs a certificate on the fly for every intercepted site. The certificate referenced by `cert=` must therefore be a **CA certificate** (with `CA:TRUE` / `keyCertSign`), not a normal leaf/server certificate. This guide uses the CA generated in Step 1 directly as the signing certificate.

### [**Prerequisites**](/docs/mdicap/v5.15.0/knowledge-base/how-can-icap-be-configured-to-handle-https-traffic-in-squid-vers#prerequisites)

- Squid v7.x.x compiled from source with SSL/ICAP support
- Ubuntu 22.04 or later
- Root or sudo privileges

### [**Configuration Steps**](/docs/mdicap/v5.15.0/knowledge-base/how-can-icap-be-configured-to-handle-https-traffic-in-squid-vers#configuration-steps)

**Step 0:** Prepare SSL Directory

sudo mkdir -p /etc/squid/ssl
cd /etc/squid/ssl

**Step 1:** Generate Certificate Authority (CA)

This CA is what Squid uses to sign the certificates it generates for intercepted sites.

sudo openssl genrsa -out myCA.key 4096
sudo openssl req -x509 -new -nodes \
-key myCA.key \
-sha256 -days 3650 \
-out myCA.crt \
-subj "/C=US/ST=LA/L=LA/O=OPSWAT/OU=Lab/CN=Squid-CA"

**Step 2:** Combine CA Certificate and Key

Squid expects the signing certificate and its private key in a single PEM file. This `myCA.pem` is what you will reference in `squid.conf`.

sudo bash -c 'cat myCA.key myCA.crt > myCA.pem'
sudo chmod 400 myCA.pem

**Step 3:** Trust the CA on Client Machines

For clients to browse HTTPS sites through the proxy without certificate warnings, the **CA certificate (**`myCA.crt`) must be trusted on each client device whose traffic is inspected, not only on the Squid host.

- Linux clients:

sudo cp myCA.crt /usr/local/share/ca-certificates/myCA.crt
sudo update-ca-certificates

- Windows clients: import `myCA.crt` into **Trusted Root Certification Authorities** (via `certlm.msc` or Group Policy for domain-wide deployment).
- macOS clients: add `myCA.crt` to the **System** keychain and set it to **Always Trust**.

**Step 4:** Locate the Certificate Generation Helper

Because Squid was compiled from source, the `security_file_certgen` helper is installed under your build prefix (for example `/usr/local/squid/libexec/` or `/usr/local/libexec/`), not the apt path `/usr/lib/squid/`. Locate it first, then use that path in the following steps:

sudo find / -name security_file_certgen 2>/dev/null

In the examples below, replace `/usr/lib/squid/security_file_certgen` with the path returned above if it differs.

**Step 5:** Initialize the SSL Database

sudo mkdir -p /var/lib/squid/ssl_db
sudo /usr/lib/squid/security_file_certgen -c \
-s /var/lib/squid/ssl_db \
-M 4MB

Expected output:

Initialization SSL db...
Done

**Step 6:** Validate SSL DB Initialization

ls -l /var/lib/squid/ssl_db

Expected result: the directory contains an `index.txt` file, a `size` file, and a `certs` subdirectory.

**Step 7:** Configure Squid (squid.conf)

http_port 3128 ssl-bump cert=/etc/squid/ssl/myCA.pem \
generate-host-certificates=on \
dynamic_cert_mem_cache_size=4MB
sslcrtd_program /usr/lib/squid/security_file_certgen \
-s /var/lib/squid/ssl_db -M 4MB
acl step1 at_step SslBump1
ssl_bump peek step1
ssl_bump bump all
> **Note:** `cert=` must point to the CA PEM created in Step 2 (`myCA.pem`), so Squid can sign the certificates it generates. If your Squid build rejects `cert=` with a parsing error, use the equivalent TLS-prefixed directive `tls-cert=` instead. Also update the `sslcrtd_program` path to match the helper location found in Step 4.

Reload Squid to apply the changes:

sudo squid -k reconfigure

**Step 8:** Validate ICAP Integration

- Access the ICAP server UI
- Confirm HTTPS traffic is being received and inspected

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
