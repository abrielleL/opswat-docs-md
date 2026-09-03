<!-- source: https://www.opswat.com/docs/supply-chain/installation/advanced-installation-for-unix-based-deployments -->

# Advanced installation for Unix-based deployments

This page describes in detail how you can achieve the following tasks:

- Use an external PostgreSQL server instead of the built-in database
- Configure HTTPS communication for the web server
- Install MetaDefender Software Supply Chain on a different disk

### Use an external database

Production deployments of MetaDefender Software Supply Chain should ensure high availability and/or load-balancing at the database level by using an external PostgreSQL for any compatible service) instead of the built-in database that is included with the basic installation.

### How to setup an external PostgreSQL in MetaDefender Software Supply Chain

The following steps should be performed before initializing MetaDefender Software Supply Chain for the first time (i.e before the **mdssc -u init** command from the [installation guide](https://www.opswat.com/docs/supply-chain/installation/installing-using-the-command-line)).

1. Ensure that your external PostgreSQL is properly configured and ready to accept remote connections

**Note:** it is recommended to setup [access control](https://docs.mongodb.com/manual/tutorial/enable-authentication/)   for your external database as well as taking the necessary network security measures to ensure that only the server running MetaDefender Software Supply Chain can access the database.

> **Info**
>
> These steps can be performed after the installation or at any other time but the existing data (if any) will be lost. In this case, the last step should be replaced with a restart instead of a start command.

> **Info**
>
> We recommend using a version of PostgreSQL that is the same as the built-in database version from the [System Requirements | Installation components](https://www.opswat.com/docs/supply-chain/installation/system-requirements-for-unix-based-deployments#installation-components) page.

2. Locate the configuration file created by the installer in **/etc/mdssc/customer.env**
3. Add the following configuration line:

```bash
POSTGRESQL_URL=Host={your_pg_host};Port=5432;Username={your_pg_user};Password={your_pg_password};Database=MDSS
```

4. Please check the [connection string documentation](https://docs.mongodb.com/manual/reference/connection-string/)  for more information. Make sure you add MDCS as the target database as shown in the example above.
5. Save the file.
6. Initialize MetaDefender Software Supply Chain by running the following command:

```bash
sudo mdssc -u init
```

7. Return to the [installation process](https://www.opswat.com/docs/supply-chain/installation/installing-using-the-command-line) and continue the installation.

### PostgreSQL advanced setup

For special use cases you may need to backup your database or restore it. MetaDefender Software Supply Chain allows you to do this by using the following commands

```bash
sudo mdssc -u export_db
```

Running this command will create a dump file in `/etc/mdssc/db_[...].tar` this file can be use afterwards as a restore file using the import command:

```bash
sudo mdssc -u import_db
```

> **Warning: Stop the Product Before Importing the Database**
>
> To ensure **data integrity**, always stop the MDSSC product **before** importing the database.
>
> Use `mdssc -c stop` to stop the product, and once the import is complete, `mdssc -c start` to start it.

### Configure HTTPS communication for the web server

Production deployments should ensure that any HTTP traffic between clients (browsers or other API client) and MetaDefender Software Supply Chain is encrypted using HTTPS.

In order to setup HTTPS communication please follow these steps:

1. Obtain the **certificate** and the **private key** as two separate files (for example, crt.pem & key.pem )
2. Rename the **private key file** in the form of <name>.key such that the extension of the file is .key
3. Place your certificates in */etc/mdssc/webclient/*
4. Run the *enable_https* utility by executing the below command
5. Verify that HTTPS is configured correctly by navigating with your browser.

```bash
sudo mdssc -u enable_https
```

### D[isabling HTTPS communication for the web server](https://www.opswat.com/docs/mdss/configuration/enabling-https#disable-https-on-unix-based-deployments?utm_term=opswat%20solutions)

For disabling HTTPS communication, run the following command:

```bash
sudo mdssc -u disable_https
```

### Add Self Signed SSL certification of service providers and MD Core

For various on-prem instances of services like GitHub, GitLab, Bitbucket, SVN, Jfrog, or an on-prem instance of MD Core with self signed SSL certifications, it is necessary that the correct certification chains should be copied in the MDSSC installation directory, under the subfolder ca-certificates:

> **Info**
>
> Default location of ca-certificates is: `/etc/mdssc/ca-certificates`

### Install MetaDefender Software Supply Chain on a different disk

The following steps should be performed before initializing MetaDefender Software Supply Chain for the first time (i.e. before the **mdssc -u init** command from the [installation guide](https://www.opswat.com/docs/supply-chain/installation/installing-using-the-command-line)).

> **Info**
>
> These steps should be performed right after the installation of Docker so that no data is lost.

1. First make sure Docker is not running and the default directory is clean
2. Remove existing images and volumes

```bash
sudo docker rm -f $(docker ps -aq); docker rmi -f $(docker images -q)
```

3. Stop Docker

```bash
sudo systemctl stop docker
```

4. Remove the default Docker location

```bash
sudo rm -rf /var/lib/docker
```

5. Create a new empty directory in the default location

```bash
sudo mkdir /var/lib/docker
```

6. Create a new empty directory on the new partition

```bash
sudo mkdir /<PATH_TO_NEW_LOCATION>
```

7. Mount the new location in the default directory

```bash
sudo mount --rbind //<PATH_TO_NEW_LOCATION> /var/lib/docker
```

8. Start back the docker service

```bash
sudo systemctl start docker
```

9. Initialize MetaDefender Software Supply Chain by running the following command:

```bash
sudo mdssc -u init
```
