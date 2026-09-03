<!-- source: https://www.opswat.com/docs/mdss/configuration/security---encryption-keys -->

# Security & Encryption Keys

To enhance your system's security, you can generate a new master encryption key. This action will re-encrypt all sensitive data—such as storage credentials, API keys, and others—and securely retire the previous key.

You can start this process by navigating to **Settings** and selecting the **Security** tab. Here, click the **Generate New** button from the **Encryption Key** section.

A confirmation dialog will appear to ensure you understand the consequences. Please note that this action is irreversible and will immediately log out all active users from the application. To proceed, click **Generate**.

While the key rotation is in progress, the system prioritizes data integrity. To prevent data corruption, any operations that access or modify encrypted information will be temporarily unavailable. For example, you will not be able to add or edit storage configurations or user accounts during this time. The process is designed to be as fast as possible, but the total duration will depend on the amount of data stored in your system. We recommend performing this critical security operation during a planned maintenance window or a period of low system activity to minimize disruption for your users.
