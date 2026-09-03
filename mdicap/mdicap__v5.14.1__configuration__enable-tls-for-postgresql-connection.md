<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection -->

# Enable TLS for PostgreSQL Connection

## [Remote PostgreSQL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#remote-postgresql)

### [Linux](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#linux)

#### [Step 1: Install PostgreSQL and OpenSSL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-1-install-postgresql-and-openssl)

For Ubuntu/Debian:

BashCopysudo apt update
sudo apt install postgresql postgresql-contrib openssl

For CentOS/RHEL:

BashCopysudo yum install postgresql postgresql-server postgresql-contrib openssl
#### [Step 2: Create SSL Certificates](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-2-create-ssl-certificates)

To enable TLS, you need a certificate and key for the server, and you can also create a certificate authority (CA) to sign the server certificate.

2.1 Create the CA Key and Certificate

BashCopyopenssl genrsa -des3 -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt

- `ca.key`: Private key for the Certificate Authority.
- `ca.crt`: Public certificate for the Certificate Authority.

2.2 Create the Server Key and Certificate Signing Request (CSR)

BashCopyopenssl genrsa -out server.key 4096
openssl req -new -key server.key -out server.csr

- `server.key`: Private key for the PostgreSQL server.
- `server.csr`: Certificate Signing Request (CSR) for the PostgreSQL server.

2.3 Sign the Server Certificate with the CA

BashCopyopenssl x509 -req -in server.csr \
-CA ca.crt -CAkey ca.key \
-CAcreateserial -out server.crt -days 365

- server.crt: Signed server certificate.

2.4 Remove the Passphrase from the Server Key

BashCopyopenssl rsa -in server.key -out server.key

Now you should have the following files:

- `ca.crt`
- `server.crt`
- `server.key`

#### [Step 3: Configure PostgreSQL to Use SSL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-3-configure-postgresql-to-use-ssl)

You need to place the certificates and keys in the appropriate directory and update the PostgreSQL configuration to enable SSL.

3.1 Copy Certificates to PostgreSQL Data Directory

Copy the `server.crt`, `server.key`, and `ca.crt` files to PostgreSQL's data directory, usually located at the output of the below CLI

BashCopysudo -u postgres psql -c 'SHOW data_directory;'

The output is: `/var/lib/postgresql/16/main`

BashCopysudo cp server.crt server.key /var/lib/postgresql/16/main
sudo cp ca.crt /var/lib/postgresql/16/main

Ensure the correct permissions and ownership:

BashCopysudo chown postgres:postgres \
/var/lib/postgresql/16/main/server.crt \
/var/lib/postgresql/16/main/server.key \
/var/lib/postgresql/16/main/ca.crtBashCopysudo chmod 600 /var/lib/postgresql/16/main/server.key

3.2 Update postgresql.conf

Edit the `postgresql.conf` file to enable SSL. The configuration file is usually located in the PostgreSQL data directory.

BashCopy/etc/postgresql/16/main/conf.d/postgresql.conf

Set the following parameters:

BashCopyssl=on
ssl_ciphers='HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers=on
ssl_cert_file='server.crt'
ssl_key_file='server.key'
ssl_ca_file='ca.crt'

Replace `<version>` with your PostgreSQL version number.

3.3 Update pg_hba.conf

Edit the pg_hba.conf file to enforce SSL connections. The configuration file is usually located in the PostgreSQL data directory.

BashCopysudo nano /etc/postgresql/16/main/pg_hba.conf

Add or modify the following lines to require SSL connections:

BashCopy# Require SSL for all connections
hostssl all all 0.0.0.0/0 md5
hostssl all all ::/0 md5
#### [Step 4: Restart PostgreSQL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-4-restart-postgresql)

Restart the PostgreSQL service to apply the changes.

BashCopysudo systemctl restart postgresql
#### [Step 5: Verify the SSL Setup](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-5-verify-the-ssl-setup)

To verify that SSL is enabled and working, you can connect to your PostgreSQL server using `psql` or any other client with SSL support.

BashCopypsql "host=localhost dbname=postgres user=postgres password=a sslmode=require"

Additionally, you can check if SSL is active by querying the server:

BashCopySHOW ssl;

It should return `on` if SSL is enabled.

### [Windows](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#windows)

#### [Step 1: Download and install the Postgresql Server for Windows OS](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-1-download-and-install-the-postgresql-server-for-windows-os)

#### [Step 2: Create SSL Certificates:](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-2-create-ssl-certificates)

Download OpenSSL for the Windows: <https://slproweb.com/download/Win64OpenSSL-3_3_2.msi>

Download dependency for OpenSSL: <https://aka.ms/vs/17/release/vc_redist.x64.exe> and install it now

After installed the OpenSSL on your system, please help add the OpenSSL to SYSTEM PATH via cli:

BashCopy[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Program Files\OpenSSL-Win64\bin", [EnvironmentVariableTarget]::Machine)

Open a new Powershell windows

BashCopyopenssl --version

To enable TLS, you need a certificate and key for the server, and you can also create a certificate authority (CA) to sign the server certificate.

2.1 Create the CA Key and Certificate

Create a directory to store the certificate:

BashCopymkdir -p certsBashCopyopenssl genrsa -des3 -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt

- `ca.key`: Private key for the Certificate Authority.
- `ca.crt`: Public certificate for the Certificate Authority.

2.2 Create the Server Key and Certificate Signing Request (CSR)

BashCopyopenssl genrsa -out server.key 4096
openssl req -new -key server.key -out server.csr

- `server.key`: Private key for the PostgreSQL server.
- `server.csr`: Certificate Signing Request (CSR) for the PostgreSQL server.

2.3 Sign the Server Certificate with the CA

BashCopyopenssl x509 -req -in server.csr \
-CA ca.crt -CAkey ca.key \
-CAcreateserial -out server.crt -days 365

- server.crt: Signed server certificate.

2.4 Remove the Passphrase from the Server Key

BashCopyopenssl rsa -in server.key -out server.key

Now you should have the following files:

- `ca.crt`
- `server.crt`
- `server.key`

#### [Step 3: Configure PostgreSQL to Use SSL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-3-configure-postgresql-to-use-ssl)

3.1 Copy Certificates to PostgreSQL Data Directory

Copy these files above to the `C:\Program Files\PostgreSQL\15\data`

3.2: Update postgresql.conf

Edit C:\Program Files\PostgreSQL\15\datapostgresql.conf file to enable SSL. The configuration file is usually located in the PostgreSQL data directory.

BashCopyssl=on
ssl_ciphers='HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers=on
ssl_cert_file='server.crt'
ssl_key_file='server.key'
ssl_ca_file='ca.crt'

3.3: Update pg_hba.conf

Edit the `C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data\pg_hba.conf` file to enforce SSL connections. The configuration file is usually located in the PostgreSQL data directory.

BashCopy## Add these lines at the end of the file
hostssl all all 0.0.0.0/0 md5
hostssl all all ::/0 md5
#### [Step 4: Restart the Postgresql service](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-4-restart-the-postgresql-service)

Open the tab Service on the Task Manager to find the Postgresql service

Step 5: Verify the SSL Setup

BashCopypsql "host=localhost dbname=postgres user=postgres password=a sslmode=require port=5432"

## [Local PostgreSQL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#local-postgresql)

### [Linux](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#linux)

#### [Step 1: Installed MD ICAP Server with local mode](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-1-installed-md-icap-server-with-local-mode)

Refer: <https://docs.opswat.com/mdicap/installation/installation-icap-v520#21without-ignition-file>

#### [Step 2: Create SSL Certificates:](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-2-create-ssl-certificates)

Same as step 2: Create SSL Certificate at [Linux](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#linux)

#### [Step 3: Configure PostgreSQL to Use SSL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-3-configure-postgresql-to-use-ssl)

3.1 Copy Certificates to PostgreSQL Data Directory

BashCopysudo cp server.crt server.key /var/lib/mdicapsrv/pg_data/
sudo cp ca.crt /var/lib/mdicapsrv/pg_data/

3.2: Update postgresql.conf

Edit the `/usr/lib/mdicapsrv/postgres/postgresql.conf` file to enable SSL. The configuration file is usually located in the PostgreSQL data directory.

BashCopysudo nano /usr/lib/mdicapsrv/postgres/postgresql.conf

Set the following parameters:

BashCopyssl=on
ssl_ciphers='HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers=on
ssl_cert_file='server.crt'
ssl_key_file='server.key'
ssl_ca_file='ca.crt'

3.3: Update pg_hba.conf

Edit the `/var/lib/mdicapsrv/pg_data/pg_hba.conf` file to enforce SSL connections. The configuration file is usually located in the PostgreSQL data directory.

BashCopysudo nano /var/lib/mdicapsrv/pg_data/pg_hba.conf

Add or modify the following lines to require SSL connections:

BashCopy## Add these lines at the end of the file
hostssl all all 0.0.0.0/0 md5
hostssl all all ::/0 md5
#### [Step 4: Restart the mdicapsrv service](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-4-restart-the-mdicapsrv-service)

BashCopysudo systemctl restart mdicapsrv

Step 5: Verify the SSL Setup

BashCopypsql "host=localhost dbname=postgres user=postgres password=a sslmode=require port=5433"

### [Windows](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#windows)

#### [Step 1: Installed MD ICAP Server with local mode](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-1-installed-md-icap-server-with-local-mode)

#### [Step 2: Create SSL Certificates](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-2-create-ssl-certificates)

Download OpenSSL for the Windows: <https://slproweb.com/download/Win64OpenSSL-3_3_2.msi>

Download dependency for OpenSSL: <https://aka.ms/vs/17/release/vc_redist.x64.exe> and install it now

After installed the OpenSSL on your system, please help add the OpenSSL to SYSTEM PATH via cli:

BashCopy[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Program Files\OpenSSL-Win64\bin", [EnvironmentVariableTarget]::Machine)

Open a new Powershell windows

BashCopyopenssl --version

To enable TLS, you need a certificate and key for the server, and you can also create a certificate authority (CA) to sign the server certificate.

2.1 Create the CA Key and Certificate

Create a directory to store the certificate:

BashCopymkdir -p certsBashCopyopenssl genrsa -des3 -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt

- `ca.key`: Private key for the Certificate Authority.
- `ca.crt`: Public certificate for the Certificate Authority.

2.2 Create the Server Key and Certificate Signing Request (CSR)

BashCopyopenssl genrsa -out server.key 4096
openssl req -new -key server.key -out server.csr

- `server.key`: Private key for the PostgreSQL server.
- `server.csr`: Certificate Signing Request (CSR) for the PostgreSQL server.

2.3 Sign the Server Certificate with the CA

BashCopyopenssl x509 -req -in server.csr \
-CA ca.crt -CAkey ca.key \
-CAcreateserial -out server.crt -days 365

- `server.crt`: Signed server certificate.

2.4 Remove the Passphrase from the Server Key

BashCopyopenssl rsa -in server.key -out server.key

Now you should have the following files:

- `ca.crt`
- `server.crt`
- `server.key`

#### [Step 3: Configure PostgreSQL to Use SSL](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-3-configure-postgresql-to-use-ssl)

3.1 Copy Certificates to PostgreSQL Data Directory

Copy these files above to the C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data

3.2: Update postgresql.conf

Create C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres\postgresql.conf file to enable SSL. The configuration file is usually located in the PostgreSQL data directory.

BashCopyssl=on
ssl_ciphers='HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers=on
ssl_cert_file='server.crt'
ssl_key_file='server.key'
ssl_ca_file='ca.crt'

3.3: Update pg_hba.conf

Edit the `C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data\pg_hba.conf` file to enforce SSL connections. The configuration file is usually located in the PostgreSQL data directory.

BashCopy## Add these lines at the end of the file
hostssl all all 0.0.0.0/0 md5
hostssl all all ::/0 md5
#### [Step 4: Restart the mdicapsrv service](/docs/mdicap/v5.14.1/configuration/enable-tls-for-postgresql-connection#step-4-restart-the-mdicapsrv-service)

Open the tab Service on the Task Manager to find the mdicapsrv service

Step 5: Verify the SSL Setup

BashCopypsql "host=localhost dbname=postgres user=postgres password=a sslmode=require port=5433"
