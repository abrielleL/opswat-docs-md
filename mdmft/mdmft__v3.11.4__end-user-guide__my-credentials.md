<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/end-user-guide/my-credentials -->

# My Credentials

Summarize Page    Connect to Cursor Connect to VS Code

MetaDefender MFT allows [certain users](/docs/mdmft/v3.11.4/operating/RBAC-role-base-access-control-permissions) to store personal credentials for use in other parts of the application.

To view your credentials, click the "user" icon in the top right corner of the application and select "My Credentials" from the dropdown menu.

Info

Currently, SSH private keys and P12/PFX-type certificates can be stored. The SSH keys may be used for authentication on SFTP servers, while the certificates can be used for authentication with SharePoint Online™.

---

### [SSH Keys](/docs/mdmft/v3.11.4/end-user-guide/my-credentials#ssh-keys)

To save a private SSH key, click the "Add SSH Key" button. In the pop-up window, enter a suitable name and paste your private key.

After saving the SSH key, you can edit or delete it from the "action" (three-dot) menu.

Info

For security reasons, the application does not return the saved private key. If you need to update the stored key's name, you must re-enter the key.

---

### [Certificates](/docs/mdmft/v3.11.4/end-user-guide/my-credentials#certificates)

To save a certificate , click the "Add Certificate" button. In the pop-up window, enter a suitable name, upload your certificate, and add the required password.

After saving the certificate, you can edit or delete it in the same way as SSH Keys.

Info

For security reasons, the application does not return the saved certificate or its password. If you need to update the stored certificate's name, you must re-upload the file and re-enter the password.

### [MFT Keys](/docs/mdmft/v3.11.4/end-user-guide/my-credentials#mft-keys)

To save a MFT key, click the "Add MFT Key" button. In the pop-up window, enter a suitable name and paste your private key.

Info

The MFT API key is used for authentication in MFT Push/Pull jobs when multi-factor authentication (MFA) is required by the remote server.

For security reasons, the application does not return the saved private key. If you need to update the stored key's name, you must re-enter the key.

### [Local MFT API keys](/docs/mdmft/v3.11.4/end-user-guide/my-credentials#local-mft-api-keys)

Regular users or Automation Coordinators can create and store API keys of the MetaDefender® MFT.

To create and save an API key for your MetaDefender® MFT instance, click “Add API Key.” In the modal, select an expiration date, optionally enter a description, then click “Add API Key” to generate the key.

In the list, click the actions menu (three dots) next to an API key to copy it, change the expiration date, or remove the key.

Info

The Local MFT API key can be used for authentication when multi-factor authentication (MFA) is required.
