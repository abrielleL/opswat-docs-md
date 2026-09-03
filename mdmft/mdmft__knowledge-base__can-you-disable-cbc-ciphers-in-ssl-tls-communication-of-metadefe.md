<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/can-you-disable-cbc-ciphers-in-ssl-tls-communication-of-metadefe -->

# Can you disable CBC Ciphers in SSL/TLS communication of MetaDefender MFT?

Summarize Page    Connect to Cursor Connect to VS Code

**Check Your Version:**

This article applies to all **MetaDefender Managed File Transfer (MFT)** release on Windows.

## [**Why should CBC ciphers be disabled?**](/docs/mdmft/knowledge-base/can-you-disable-cbc-ciphers-in-ssl-tls-communication-of-metadefe#why-should-cbc-ciphers-be-disabled)

Disabling CBC ciphers is a standard security best practice for modern production environments to prevent specific cryptographic attacks:

- **Vulnerability to Attacks:** CBC mode ciphers are susceptible to "Padding Oracle" attacks, such as **Lucky 13** and **POODLE**. These vulnerabilities can allow attackers to decipher sensitive traffic by analyzing timing differences in server responses.
- **Compliance Requirements:** Many security audits and compliance standards (such as PCI-DSS) flag CBC ciphers as "weak" and require their removal to ensure data integrity and confidentiality.

## [**Can you disable CBC Ciphers in MetaDefender MFT?**](/docs/mdmft/knowledge-base/can-you-disable-cbc-ciphers-in-ssl-tls-communication-of-metadefe#can-you-disable-cbc-ciphers-in-metadefender-mft)

Yes, you can disable the use of Cipher Block Chaining (CBC) ciphers for HTTPS/TLS connections on your MetaDefender MFT instance.

To achieve this, we recommend configuring your MFT Server to **strictly enforce TLS v1.3**:

- Navigate to **Settings > Security > Server Configuration** in the Web Console.
- Under the **HTTPS** section, check the box for **TLS v1.3**.
- Uncheck the boxes for **TLS v1.2**, **TLS v1.1**, and **TLS v1.0**.

By enforcing TLS v1.3, you automatically exclude CBC ciphers from your environment.

Before enforcing TLS v1.3, please ensure that all clients connecting to your MFT instance (web browsers, automated agents, or API integrations) support this protocol version. Legacy clients that rely on TLS v1.2 will lose access if you strictly enforce TLS v1.3.

Please also make sure that MD MFT is configured for HTTPS communication: [Server Configuration - MetaDefender Managed File Transfer](https://www.opswat.com/docs/mdmft/configuration/server-configuration#enabling-https).

## [**Why adopt TLS v1.3?**](/docs/mdmft/knowledge-base/can-you-disable-cbc-ciphers-in-ssl-tls-communication-of-metadefe#why-adopt-tls-v13)

TLS v1.3 is the modern standard for secure communications and offers significant improvements over TLS v1.2:

- **Exclusive use of AEAD:** According to [**RFC 8446**](https://datatracker.ietf.org/doc/html/rfc8446), TLS v1.3 removes support for obsolete algorithms. It exclusively uses **Authenticated Encryption with Associated Data (AEAD)** ciphers (e.g., AES-GCM), which do not suffer from the padding vulnerabilities found in CBC.
- **Improved Performance:** TLS v1.3 simplifies the "handshake" process required to establish a secure connection, resulting in faster load times and lower latency for your users.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
