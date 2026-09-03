<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/does-metadefender-core-support-elliptic-curve--ec--private-key-a -->

# Does MetaDefender Core support Elliptic Curve (EC) Private Key and Certificate for enabling HTTPS?

Yes, MetaDefender Core supports Elliptic Curve private key and certificate for enabling HTTPS.

**Example: PEM-encoded EC private key format**

HtmlCopy-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIFXkB9C7UeznRzZKj...
-----END EC PRIVATE KEY-----
### [🔍Supported Curves](/docs/mdcore/knowledge-base/does-metadefender-core-support-elliptic-curve--ec--private-key-a#supported-curves)

Elliptic Curve Cryptography (ECC) offers many different curve sets. You can list all supported curves using the following command:

HtmlCopyopenssl ecparam -list_curves

However, most modern browsers only support **P-256** and **P-384**.

Therefore, we recommend using P-256 (also known as `prime256v1`) or P-384 for HTTPS with MetaDefender Core.

### [🔧 How to Verify Your EC Private Key](/docs/mdcore/knowledge-base/does-metadefender-core-support-elliptic-curve--ec--private-key-a#-how-to-verify-your-ec-private-key)

To inspect your EC private key, use the following command:

HtmlCopyopenssl ec -in yourkey.key -text -noout
### [Explanation:](/docs/mdcore/knowledge-base/does-metadefender-core-support-elliptic-curve--ec--private-key-a#explanation)

- `-in ec_private.key`: Path to your EC private key file (PEM format).
- `-text`: Prints a human-readable summary of the key (including public and private components).
- `-noout`: Suppresses output of the encoded key.

### [Example Output:](/docs/mdcore/knowledge-base/does-metadefender-core-support-elliptic-curve--ec--private-key-a#example-output)

HtmlCopyread EC key
Private-Key: (256 bit)
priv:
73:a1:34:...
pub:
04:51:88:...
ASN1 OID: prime256v1
NIST CURVE: P-256Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
