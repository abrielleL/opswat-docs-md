<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-are-files-encrypted-in-vault- -->

# Are files encrypted in MetaDefender Managed File Transfer and, if so, how?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer releases deployed on Windows systems.

Yes, MetaDefender Managed File Transfer encrypts files after they have been successfully processed:

- The algorithm used for encryption is the **Advanced Encryption Standard (AES)** with **Cipher Block Chaining** mode enabled, and **PKCS #7** padding:

  - The cipher block size is 128 bits.
  - The cryptographic key is 256 bits.
  - The algorithm also uses an initialization vector (IV) of 128 bits.
  - The cryptographic key is derived from a randomly generated 256 bit passphrase and 64 bit salt, conforming to the RFC 2898 standard.
- Users have the option to generate new cryptographic keys to facilitate **key rotation** as an extra security measure:

  - Bear in mind that only new files will be encrypted with your newly generated cryptographic keys.
  - Files that were uploaded prior to key generation will remain encrypted with the original cryptographic key.
  - For instructions on how to generate a new cryptographic key, please [Read This](/docs/mdmft/v3.11.4/configuration/encryption).
- The MetaDefender Managed File Transfer system stores all encryption keys in the database as **UTF-8 encoded hexadecimal characters**:

  - Following successful key generation, the system will return the newly created cryptographic key as a UTF-8 encoded hexadecimal sequence of characters.
  - It is possible to use a trusted platform module (TPM) or hardware security module (HSM) to store the key, but these cannot be directly queried by the MetaDefender Managed File Transfer application.

Support:

If you have queries, concerns or issues regarding **MetaDefender** **Managed File Transfer** **Encryption Methods**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
