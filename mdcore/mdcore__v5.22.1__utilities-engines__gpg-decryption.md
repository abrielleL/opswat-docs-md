<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/utilities-engines/gpg-decryption -->

# Decrypt GPG files

View as Markdown Ask ChatGPT about this page Ask Claude about this page

GPG files are created by applying GPG encryption to a file or message, ensuring that only authorized individuals with the corresponding private key can decrypt and access the original content. This is commonly used for securing sensitive information, such as emails, files, or communications.

Prerequisite: Install the [GPG tool](https://www.gnupg.org/documentation/manpage.html) on the MetaDefender Core server.

Configure the GPG command line path: Inventory > Modules > Utilities > Archive extraction module. set GPG Path to the installed GPG bin folder

### [Symmetric encryption (encrypted with password)](/docs/mdcore/v5.22.1/utilities-engines/gpg-decryption#symmetric-encryption-encrypted-with-password)

With this setting, users can scan a GPG file with a provided password as a regular password-protected archive file.

### [Asymmetric encryption (encrypted with private/public key)](/docs/mdcore/v5.22.1/utilities-engines/gpg-decryption#asymmetric-encryption-encrypted-with-privatepublic-key)

- Users need to import the private key to the local GPG tool first.
- Enable the "Enable GPG decryption with asymmetric key" option.
- Run **gpg --help** command to get the GPG Home directory, e.g.:

*In Linux, users have to give "metascan" user permission to this home directory, including subfolders and files.*

- Set the GPG Home directory in the UI.

With this setting, users can scan a GPG file with a provided passphrase as a regular password-protected archive file.
