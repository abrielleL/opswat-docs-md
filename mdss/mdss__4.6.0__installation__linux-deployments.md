<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/linux-deployments -->

# Linux Deployments

This page describes in detail how you can achieve the following tasks:

- Use an external PostgreSQL server instead of the built-in database
- Configure HTTPS communication for the web server
- Install MetaDefender Storage Security on a different disk

## Use an external database

Production deployments of MetaDefender Storage Security should ensure high availability and/or load-balancing at the database level by using an external PostgreSQL (or any compatible service) instead of the built-in database that is included with the basic installation.

> **Info**
>
> We recommend using a version of PostgreSQL that is the same as the built-in database version from [this](https://www.opswat.com/docs/mdss/getting-started/unix-deployment) page.

## How to setup an external PostgreSQL in MetaDefender Storage Security

The following steps should be performed before initializing MetaDefender Storage Security for the first time (i.e before the **mdss -u init** command from the [Installation Methods](https://www.opswat.com/docs/mdss/installation/installation-methods)).

> **Info**
>
> These steps can be performed after the installation or at any other time but the existing data (if any) will be lost. In this case, the last step should be replaced with a restart instead of a start command.

1. Ensure that your external PostgreSQL is properly configured and ready to accept remote connections

**Note:** it is recommended to setup [access control](https://www.postgresql.org/docs/8.1/client-authentication.html) for your external database as well as taking the necessary network                                security measures to ensure that only the server running MetaDefender Storage Security can access the                                      database.

2. Locate the configuration file created by the installer in **/etc/mdss/customer.env**
3. Add the following configuration line:

```plaintext
POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=dbName
POSTGRESQL_URL=Host=postgres;Port=5432;Username=user;Password=password;Database=dbName
```

4. Please check the [connection string documentation](https://www.npgsql.org/doc/connection-string-parameters.html) for more information. Make sure you add "mdss" as the target database as shown in the example above.
5. Save the file.
6. Initialize MetaDefender Storage Security by running the following command:

```plaintext
sudo mdss -u init
```

7. Return to the steps in [Installation Methods](https://www.opswat.com/docs/mdss/installation/installation-methods) and continue the installation.

## PostgreSQL SSL Configuration

To enable SSL/TLS certificate validation for the PostgreSQL connection, update the `POSTGRESQL_URL` variable in the `customer.env` file.

### File Location

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
sudo mdss -u export_db
```

Running this command will create a dump file in `/etc/mdss/db_[...].tar` this file can be use afterwards as a restore file using the import command:

```plaintext
sudo mdss -u import_db
```

> **Info**
>
> Product versions 3.4.2 and above do not support importing databases from earlier versions (less than 3.4.2). When using the `import_db` utility on these versions, it will automatically restore the database from the most recent backup file named `db_[...].tar`.

> **CRITICAL: Stop MDSS Service Before Database Import**
>
> > Data corruption may occur if the MDSS service is running during database import.
> >
> > Follow these steps:
> >
> > **1.** Stop the service: mdss -c stop **2.** Verify it's stopped: mdss -c status **3.** Import your database **4.** Restart the service: mdss -c start
> >
> > **Allow 30 seconds between stop and start commands.**
> >
> > Failure to follow this procedure may result in data loss.

## Configure HTTPS communication for the web server

Production deployments should ensure that any HTTP traffic between clients (browsers or other API client) and MetaDefender Storage Security is encrypted using HTTPS.

[Click here](https://www.opswat.com/docs/mdss/configuration/enabling-https) for detailed instructions on how to setup a certificate for NGINX web server.

## Install MetaDefender Storage Security on a different disk

The following steps should be performed before initializing MetaDefender Storage Security for the first time (i.e before the **mdss -u init** command from the [Linux Installation](https://www.opswat.com/docs/mdss/installation/linux-installation)).

> **Info**
>
> These steps should be performed right after the installation of Docker so that no data is lost.

1. First make sure Docker is not running and the default directory is clean
2. Remove existing images and volumes

```plaintext
sudo docker rm -f $(docker ps -aq); docker rmi -f $(docker images -q)
```

3. Stop Docker

```plaintext
sudo systemctl stop docker
```

4. Remove the default Docker location

```plaintext
sudo rm -rf /var/lib/docker
```

5. Create a new empty directory in the default location

```plaintext
sudo mkdir /var/lib/docker
```

6. Create a new empty directory on the new partition

```plaintext
sudo mkdir /<PATH_TO_NEW_LOCATION>
```

7. Mount the new location in the default directory

```plaintext
sudo mount --rbind //<PATH_TO_NEW_LOCATION> /var/lib/docker
```

8. Start back the docker service

```plaintext
sudo systemctl start docker
```

9. Initialize MetaDefender Storage Security by running the following command:

```plaintext
sudo mdss -u init
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
