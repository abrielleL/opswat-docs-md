<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain -->

# OCM Uses a Complete Certificate Chain with a Private Root CA

This section shows how to generate a **root CA**, an **intermediate CA**, and a **server certificate** with a **complete certificate chain**.

In production, these certificates are usually issued by your internal PKI or a public CA. The following example uses self‑generated certificates purely for demonstration and testing.

#### [1. Generate Root CA](/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain#1-generate-root-ca)

The root CA is the top‑level certificate authority in the chain.

`openssl genrsa -out root.key 4096`

`openssl req -x509 -new -nodes -key root.key -sha256 -days 3650 -out root.crt -subj "/CN=MyRootCA"`

This creates:

- `root.key` – private key for the root CA
- `root.crt` – self‑signed root CA certificate (valid for 10 years)

#### [2. Generate Intermediate CA](/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain#2-generate-intermediate-ca)

The intermediate CA is issued by the root CA and will be used to sign the server certificate.

`openssl genrsa -out intermediate.key 4096`

`openssl req -new -key intermediate.key -out intermediate.csr -subj "/CN=MyIntermediateCA"`

`openssl x509 -req -in intermediate.csr -CA root.crt -CAkey root.key -CAcreateserial -out intermediate.crt -days 1825 -sha256 -extfile <(printf "basicConstraints=CA:TRUE\nkeyUsage=critical,keyCertSign,cRLSign")`

This creates:

- `intermediate.key` – private key for the intermediate CA
- `intermediate.crt` – intermediate CA certificate signed by `root.crt`

#### [3. Generate Server Certificate (CN = `myserver.local`)](/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain#3-generate-server-certificate-cn--myserverlocal)

This is the certificate that will be installed on the OCM server.

`openssl genrsa -out server.key 2048`

`openssl req -new -key server.key -out server.csr -subj "/CN=myserver.local"`

`openssl x509 -req -in server.csr -CA intermediate.crt -CAkey intermediate.key -CAcreateserial -out server.crt -days 825 -sha256`

This creates:

- `server.key` – private key used by the server
- `server.crt` – server certificate signed by the intermediate CA

> In a real deployment, replace `myserver.local` with the actual FQDN of your OCM server.

#### [4. Create the Server Certificate Chain File](/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain#4-create-the-server-certificate-chain-file)

Now we build the full chain in the correct order. **The certificate order is important** and must be:

1. Server certificate
2. Intermediate CA certificate
3. Root CA certificate

`cat server.crt intermediate.crt root.crt > server.chain.crt`

Use `server.chain.crt` on the server (OCM) side, **not** `server.crt` alone.

#### [5. Use the Certificates for OCM](/docs/mddrive/v4.4.2a/advanced-usages/ocm-uses-a-server-certificate-with-a-complete-certificate-chain#5-use-the-certificates-for-ocm)

After generating and verifying the chain:

- Use `server.key` (from step 3)
- Use `server.chain.crt` (from step 4)

to configure the TLS/HTTPS certificate on your **OCM on‑prem server**.

Ensure that:

- The server is configured to present the **full certificate chain** (`server.chain.crt`)

  - The private key (`server.key`) matches the server certificate
- The hostname/FQDN in the certificate matches the URL that Drive uses to connect to OCM
