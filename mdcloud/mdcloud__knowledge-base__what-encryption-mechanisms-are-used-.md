<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/what-encryption-mechanisms-are-used- -->

# What encryption mechanisms are used by MetaDefender Cloud?

This article applies to all active MetaDefender Cloud license holders - whether your product is paid for or issued for evaluation purposes.

Please Note:

MetaDefender Cloud maintains a highly secure infrastructure to ensure that user data is processed and stored safely. This includes multiple layers of encryption and advanced safety features that are subject to stringent Encryption and Export Administration (EAR) and other U.S. laws. These encryption and data safety measures have been approved for export from the United States, subject to specified requirements and limitations under law.

**Integrated measures include:**

- Uploaded files are stored on AWS S3 buckets set to encrypt the data using the AES-256 (256-bit Advanced Encryption Standard) algorithm.
- The servers processing the files all use encrypted storage volumes.
- All user files are automatically encrypted when stored.
- All communication done via REST API uses HTTPS encryption.

**Optional measures include:**

- As an extra layer of security for files *in flight* to and from MetaDefender Cloud, users can encrypt those files using an RSA key.
- For more information on RSA keys and how to use them, please [Read This](https://docs.opswat.com/mdcloud/account-management/rsa-key-encryption).
- Our enterprise customers have the ability to leverage mTLS instead of just TLS 1.2 which also comes with a custom URL dedicated just to them.

Support:

For any queries or concerns regarding **Encryption Or User Privacy and Data Protection**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
