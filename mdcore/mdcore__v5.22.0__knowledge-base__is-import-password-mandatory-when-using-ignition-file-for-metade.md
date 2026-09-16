<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/is-import-password-mandatory-when-using-ignition-file-for-metade -->

# Is Import Password Mandatory When Using Ignition File for MetaDefender Core installation?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

### [Summary](/docs/mdcore/v5.22.0/knowledge-base/is-import-password-mandatory-when-using-ignition-file-for-metade#summary)

When installing MetaDefender Core, the system uses an ignition file to apply the initial configuration. This article explains whether including an import password is mandatory when the configuration package is referenced within the ignition file.

Here we have an example of a configuration file with OPSWAT.zip as in password file, and OPSWAT_Nopass will be the one with the password.

**Example:**

Here we have an example of two configuration files:

- `**OPSWAT.zip**`: This configuration file **requires an import password**.
- `**OPSWAT_Nopass.zip**`: This configuration file **does not have a password**.

### [Scenario 1: No password configuration file. (OPSWAT_Nopass.zip)](/docs/mdcore/v5.22.0/knowledge-base/is-import-password-mandatory-when-using-ignition-file-for-metade#scenario-1-no-password-configuration-file-opswat_nopasszip)

Example 1

Example 2

When importing the configuration file above, MetaDefender Core reports it as an invalid format.

HtmlCopyFailed to initialize the product with config file, reason='import file format invalid, C:/opswat/OPSWAT_Nopass.zip'Error:

One of the other ways to confirm if the ignition file fails is to access MetaDefender Core, is to see if the login screen appears or starts with the wizards to set up the account.

### [Scenario 2: Password-protected configuration file. (OPSWAT.zip)](/docs/mdcore/v5.22.0/knowledge-base/is-import-password-mandatory-when-using-ignition-file-for-metade#scenario-2-password-protected-configuration-file-opswatzip)

Once the ignition file is confirmed when installing MetaDefender Core, the configuration file is in the right format.

HtmlCopyIgnition: Config package has been imported!, schemaImportPath='C:/opswat/OPSWAT.zip'

Since the import was a success, we can access the login page to proceed.

Support:

If you have followed all of the steps above but are still unable to resolve the issue. Please follow these instructions on [How to Create Support Package With Bundle Tools?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-#), before [creating a support case or chatting with our support engineer.](https://my.opswat.com/portal/support)
