<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/windows-deployments -->

# Windows Deployments

This page describes in detail how you can achieve the following tasks:

- Use an external PostgreSQL server instead of the built-in database
- Configure HTTPS communication for the web server

## Use an external database

Production deployments of MetaDefender Storage Security should ensure high availability and/or load-balancing at the database level by using an external PostgreSQL (or any compatible service) instead of the built-in database that is included with the basic installation.

> **Info**
>
> We recommend using a version of PostgreSQL that is the same as the built-in database version from the [requirements](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements) page.

## How to setup an external PostgreSQL in MetaDefender Storage Security

> **Info**
>
> These steps should be performed immediately after the installation (before completing the onboarding or any other UI configuration) because any existing data will be lost.

1. Ensure that your external PostgreSQL is properly configured and ready to accept remote connections

**Note:** it is recommended to setup [access control](https://www.postgresql.org/docs/8.1/client-authentication.html)  for your external database as well as taking the necessary network security measures to ensure that only the server running MetaDefender Storage Security can access the database.

1. Locate the configuration file `customer.env` created by the installer (by default it is located at *C:\Program Files\OPSWAT\MetaDefender Storage Security\config*)
2. Add the following configuration line:

```plaintext
POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=dbName
POSTGRESQL_URL=Host=postgres;Port=5432;Username=user;Password=password;Database=dbName
```

4. Please check the [connection string documentation](https://www.npgsql.org/doc/connection-string-parameters.html)  for more information. Make sure you add "mdss" as the target database as shown in the example above.
5. Save the file.
6. Reinstall the internal components by running the following PowerShell command

```plaintext
PS> .\mdss.ps1 -c refresh
```

7. Continue to the [onboarding](https://www.opswat.com/docs/mdss/operations/onboarding) process.

## PostgreSQL SSL Configuration

To enable SSL/TLS certificate validation for the PostgreSQL connection, update the `POSTGRESQL_URL` variable in the `customer.env` file.

#### File Location

By default, the `customer.env` file is located at:

C:\Program Files\OPSWAT\MetaDefender Storage Security\config

The installer creates this file automatically.

### Configuring POSTGRESQL_URL

The `POSTGRESQL_URL` variable can include additional parameters for SSL/TLS. By default SSL Mode is set to "prefer".

```json
POSTGRESQL_URL=Host=postgres;Port=5432;Username=user;Password=password;Database=dbName;SSL Mode=VerifyFull;Root Certificate=<path to root CA certificate>
```

### SSL Mode Options

• **prefer** (default): Attempts to connect using SSL. If SSL fails, falls back to unencrypted. **No certificate validation.**

• **require**: Requires SSL encryption. **Certificate validation is skipped** — allows self-signed, expired, or otherwise invalid certifications.

• **verify-full**: Requires SSL and performs **full certificate validation**, including hostname match and trusted CA.

### Important Notes

•  If **certificate validation is required**, use `verify-full` and provide a valid CA-signed certificate via the `Root Certificate` parameter.

• If using a **self-signed or otherwise invalid certificate**, use `require`, which skips validation but still encrypts the connection.

•  The `Root Certificate` must point to the CA file if using `verify-ca` or `verify-full`.

### How to modify it

Set the parameter in your **customer.env** file. Please find [here](https://www.opswat.com/docs/mdss/configuration/custom-configuration) more details on how to update the configuration file.

## PostgreSQL advanced setup

For special use cases you may need to backup your database or restore it. MetaDefender Storage Security allows you to do this by using the following commands

```plaintext
PS> .\mdss.ps1 -u export_db
```

Running this command will create a dump file in the install directory. This file can be use afterwards as a restore file using the import command:

```plaintext
PS> .\mdss.ps1 -u import_db
```

> **Info**
>
> The import_db utility will use the latest file as restore point

> **CRITICAL: Stop MDSS Service Before Database Import**
>
> Data corruption may occur if the MDSS service is running during database import.
>
> Follow these steps:
>
> **1.** Stop the service: mdss -c stop **2.** Verify it's stopped: mdss -c status **3.** Import your database **4.** Restart the service: mdss -c start
>
> **Allow 30 seconds between stop and start commands.**
>
> Failure to follow this procedure may result in data loss.

## Configure HTTPS communication for the web server

Production deployments should ensure that any HTTP traffic between clients (browsers or other API client) and MetaDefender Storage Security is encrypted using HTTPS.

[Click here](https://www.opswat.com/docs/mdss/configuration/enabling-https) for detailed instructions on how to setup a certificate for NGINX web server.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
