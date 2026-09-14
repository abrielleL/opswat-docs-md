<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures -->

# How can SDK packages be verified using a public key and specific signatures?

To mitigate security risks like Man-in-the-Middle attacks, DNS spoofing, etc., OPSWAT offers a Digital Signature Verification mechanism that you may use to ensure that downloaded SDK packages are authentic and unaltered since OPSWAT created and posted them.

Let's dive into how to obtain the necessary materials for Digital Signature Verification and set it up for you to validate the SDK packages.

## [Obtaining the Public Key](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#obtaining-the-public-key)

The public key is available in the file named `sdk_pubkey_YYYY-MM-vD.gpg`, where:

- `YYYY-MM` represents the creation date of the public key
- `vD` denotes the version number of the public key

This file can be used to verify both Engine and Data packages. It is hosted on the My OPSWAT Portal and the VCR Gateway, allowing you to choose the most suitable method for obtaining the public key based on your needs.

Below are the instructions for acquiring the public key from both the My OPSWAT Portal and VCR Gateway.

#### [Obtaining the public key from My OPSWAT Portal](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#obtaining-the-public-key-from-my-opswat-portal)

1. Login to my.opswat.com with your OEM account
2. Navigate to my.opswat.com/product-downloads
3. Select MetaDefender Endpoint Security SDK
4. Download the current public key (see Figure A below) and note that the downloaded filename will be similar to `sdk_pubkey_YYYY-MM-vD.gpg`
5. Import the public key to your machine using the command below (Figure B below)

**Figure A - Download the public key from the Portal**

#### [Obtaining public key from VCR Gateway](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#obtaining-public-key-from-vcr-gateway)

1. Collect your authorization token (by reaching out to your Admin or Support agent)
2. Download `sdk_pubkey_YYYY-MM.gpg` file by executing the following URL `https://vcr.opswat.com/gw/file/download/sdk_pubkey.gpg?type=1&token=<authorization_token>`
3. Import the public key to your machine using the command below

BashCopy$ gpg --import sdk_pubkey.gpg

**Figure B - Importing the public key**

---

## [Downloading SDK packages](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#downloading-sdk-packages)

#### [Downloading SDK packages from My OPSWAT Portal](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#downloading-sdk-packages-from-my-opswat-portal)

1. Login to my.opswat.com with your OEM account
2. Navigate to my.opswat.com/product-downloads
3. Select MetaDefender Endpoint Security SDK
4. Download your packages and the corresponding signature files

#### [Downloading SDK packages from VCR Gateway](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#downloading-sdk-packages-from-vcr-gateway)

1. Collect your authorization token (by reaching out to your Admin or Support agent)
2. Download your packages by executing the following URL `https://vcr.opswat.com/gw/file/download/<packagename>?type=1&token=<authorization_token>`
3. Download the corresponding signature files for your packages by executing the following URL `https://vcr.opswat.com/gw/file/download/<packagename>.sig?type=1&token=<authorization_token>`

## [Verifying SDK packages](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#verifying-sdk-packages)

Once you've imported the public key and downloaded the SDK packages along with the corresponding signature files to your machine, you can verify the SDK packages by running the following command

BashCopy$ gpg --verify <downloaded_signature_file> <downloaded_package>
## [Expiration](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#expiration)

As per security purposes, the public key is valid for only one year. After that, it must be replaced with a new public key provided by OPSWAT.

A new public key and announcement will be sent 30 days in advance to ensure a smooth transition.

## [Known Issues](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#known-issues)

#### ["Can't check signature: No public key"](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#cant-check-signature-no-public-key)

During the 30-day period from the *first announcement of the new public key update* to the *old public key's expiration date*, you may encounter an warning when validating the package's signature using only one of the two public keys:

BashCopy$ gpg --verify OESIS_V4_4_3_4248_0r_465VTD.zip.sig OESIS_V4_4_3_4248_0r_EVOLRP.zip
gpg: Signature made Thu Sep 5 19:55:06 2024 SEAST
gpg: using RSA key XXXXXXXXXXXXXXXX
gpg: Can't check signature: No public key
gpg: Signature made Thu Sep 5 19:55:07 2024 SEAST
gpg: using RSA key XXXXXXXXXXXXXXXX
gpg: Good signature from "OPSWAT Inc. (OES Portal) <customer_support@opswat.com>"

This occurs because gpg validates using both the old and new keys during the transition period. After the expiration date, only the new key will be valid for SDK packages, and the issue will no longer persist.

#### [This key is not certified with a trusted signature](/docs/mdsdk/knowledge-base/verify-sdk-packages-with-public-key-signatures#this-key-is-not-certified-with-a-trusted-signature)

When executing Digital Signature Verification, you may encounter the following warning:

BashCopy$ gpg --verify OESIS_V4_4_3_4248_0r_465VTD.zip.sig OESIS_V4_4_3_4248_0r_EVOLRP.zip
...
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.

This warning is expected from the key management system, as we have not yet signed or certified our keys with a third party. To ensure security, always pull the key from the VCR Gateway or OEM Portal.
