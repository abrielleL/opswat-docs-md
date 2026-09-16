<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/ssl-connection-for-postgresql-communication -->

# SSL Connection for bundled PostgreSQL

The SSL connection configuration is possible thanks to the support made by PostgreSQL. For reference: [**https://www.postgresql.org/docs/14/ssl-tcp.html**](https://www.postgresql.org/docs/14/ssl-tcp.html)

MetaDefender Core is tested against this mode on particular version 4.21.1

### [Step 1: Generate SSL certificate for PostgreSQL server](/docs/mdcore/v5.22.0/configuration/ssl-connection-for-postgresql-communication#step-1-generate-ssl-certificate-for-postgresql-server)

Note

Following instructions are for self-sign certificate. For production environment, making sure to use the certificate signed by your trusted CA.

**1) Generate a private key**

BashCopyopenssl genrsa -aes256 -out server.key 2048

Sample output:

BashCopyGenerating RSA private key, 1024 bit long modulus ........++++++
................++++++
e is 65537 (0x10001)
Enter pass phrase for server.key:
Verifying - Enter pass phrase for server.key:

Type your desired password / pass phrase to encrypt the private key

**2) Remove the pass phrase to automatically start up the PostgreSQL server**

BashCopyopenssl rsa -in server.key -out server.keyNote

On Linux, make sure to set permission on the server.key file

BashCopychmod og-rwx server.key

**3) Create a self-signed certificate**

BashCopyopenssl req -new -key server.key -days 3650 -out server.crt -x509

You will be prompted to enter detailed information which is incorporated into your self-signed certificate request.

Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:CA
Locality Name (eg, city) [Default City]:San Francisco
Organization Name (eg, company) [Default Company Ltd]:OPSWAT
Unit Name (eg, section) []:OPSWAT
Common Name (eg, your name or your server's hostname) []:localhost
Email Address []:dummy_email@opswat.com

For self-signed certificate, use the server ceriticate as the trusted root certificate:

BashCopycp server.crt root.crt

Copy **server.key**, **server.crt**, **root.crt** to PostgreSQL data folder. For bundled local MetaDefender Core's PostgreSQL:

- Windows: **<Installation folder>\data\pg_data\**
- Linux: **/var/lib/ometascan/pg_data/**

### [Step 2: Configure PostgreSQL server for SSL authentication connection](/docs/mdcore/v5.22.0/configuration/ssl-connection-for-postgresql-communication#step-2-configure-postgresql-server-for-ssl-authentication-connection)

**1) Create a custom config file (e.g. ssl.conf) for PostgreSQL.**

For bundled local MetaDefender Core's PostgreSQL:

- Windows: **<Installation folder>\postgres\ssl.conf**
- Linux: **/usr/lib/ometascan/postgres/ssl.conf**

**2) Content of ssl.conf:**

ssl = on
ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers = on
ssl_cert_file = '<abs_path_to_server.crt>'
ssl_key_file = '<abs_path_to_server.key>'
ssl_ca_file = '<<abs_path_to_root.crt>'

**3) Modify pg_hba.conf**

For bundled local MetaDefender Core's PostgreSQL:

- Windows: **<Installation folder>\data\pg_data\pg_hba.conf**
- Linux: **/var/lib/ometascan/pg_data/pg_hba.conf**

Add following (modify **::1/128** if needed to match with your environment requirement)

hostssl all all ::1/128 scram-sha-256

After the modify, the content of pg_hba.conf should be like this (example):

Note

In a Linux environment, a local and host connection is required to upgrade from version 5.5.1 or earlier to version 5.6.0 or later.

# PostgreSQL Client Authentication Configuration File
# ===================================================
#
# Refer to the "Client Authentication" section in the PostgreSQL
# documentation for a complete description of this file. A short
# synopsis follows.
#
# This file controls: which hosts are allowed to connect, how clients
# are authenticated, which PostgreSQL user names they can use, which
# databases they can access. Records take one of these forms:
#
# local DATABASE USER METHOD [OPTIONS]
# host DATABASE USER ADDRESS METHOD [OPTIONS]
# hostssl DATABASE USER ADDRESS METHOD [OPTIONS]
# hostnossl DATABASE USER ADDRESS METHOD [OPTIONS]
# hostgssenc DATABASE USER ADDRESS METHOD [OPTIONS]
# hostnogssenc DATABASE USER ADDRESS METHOD [OPTIONS]
local all all password/scram-sha-256
host all all ::1/128 password/scram-sha-256
hostssl all all ::1/128 password/scram-sha-256
#More content.......

**4) Reload the services**

- Standalone DB mode: Restart **ometascan** service (MetaDefender Core service)
- Shared DB mode: Restart **ometascan-pg**`/`**ometascan-postgresql** service (MetaDefender Core PostgreSQL service) and then **ometascan** service (MetaDefender Core service)

Test your SSL database connection:

BashCopypsql.exe "sslmode=require dbname=postgres user=postgres host=localhost port=5432"
Password for user postgres:
psql (12.7)
WARNING: Console code page (437) differs from Windows code page (1252)
8-bit characters might not work correctly. See psql reference
page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.

This message indicate that you are now using SSL connection:

BashCopySSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
