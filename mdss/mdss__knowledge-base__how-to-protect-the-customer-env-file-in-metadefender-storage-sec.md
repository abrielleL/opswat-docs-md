<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/how-to-protect-the-customer-env-file-in-metadefender-storage-sec -->

# How to protect the customer.env file in MetaDefender Storage Security?

This article applies to all MetaDefender Storage Security releases deployed on Windows and Linux systems.

The customer.env file stores the Postgres username and Postgres password in plaintext, these credentials are randomly generated at startup and are required for MetaDefender Storage Security to connect to the internal database that is not exposed outside of the machine.

### [Options for security:](/docs/mdss/knowledge-base/how-to-protect-the-customer-env-file-in-metadefender-storage-sec#options-for-security)

- If you are connecting MDSS to an external database, it is recommended to setup [**access control**](https://www.postgresql.org/docs/8.1/client-authentication.html) for the external database at [Client Authentication](https://www.postgresql.org/docs/8.1/client-authentication.html) to ensure that only the server running MetaDefender Storage Security can access the database.
- The password must remain in plaintext, it cannot be hashed as it is sent in plaintext over the network, therefore ensure you have a **secure network**.
- Remove the `customer.env` file after MetaDefender Storage Security service starts, and place it back only when starting/stopping MetaDefender Storage Security service, or you may configure permissions for the file so that only authorized users have access to it, by default only **root user** has access to it.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
