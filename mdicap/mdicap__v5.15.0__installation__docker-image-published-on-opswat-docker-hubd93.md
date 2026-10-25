<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/docker-image-published-on-opswat-docker-hubd93 -->

# Docker image published on OPSWAT Docker Hub

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

OPSWAT publish all official **public** docker images on Docker Hub:

`opswat/metadefendericapsrv-<os-type>:<version>`

The docker images are all bundled with the official release MetaDefender ICAP Server.

More information:

<https://hub.docker.com/r/opswat/metadefendericapsrv-centos>

<https://hub.docker.com/r/opswat/metadefendericapsrv-debian>

## [Pull from the OPSWAT Docker Hub repository](/docs/mdicap/v5.15.0/installation/docker-image-published-on-opswat-docker-hubd93#pull-from-the-opswat-docker-hub-repository)

pull imageCopydocker pull <repository>/metadefendericapsrv-<platform>[:<version>]

- `<repository>` - OPSWAT repository address
- `<platform>` - can be `centos`, `debian`
- `<version>` - desired Core version (optional, default is `latest`)

Example:

## [Run MetaDefender ICAP Server docker image](/docs/mdicap/v5.15.0/installation/docker-image-published-on-opswat-docker-hubd93#run-metadefender-icap-server-docker-image)

docker run cmdCopydocker run -d [--name <container_name>] \
[-e "<env_var>=<value>"] \
[-v <ignition_folder>:<container_ignition_folder>] \
[-v <host_folder>:<container_folder>] \
[-u <user ID>] \
-p <rest_port>:8048 <image_name>
### [[Parameter] Container Name](https://docs.opswat.com/mdcore/advanced-deployment/docker-image-published-on-opswat-docker-hub#parameter-container-name)

**Argument**: `--name <container_name>`

**Description**: Your container’s name

**Example**: `--name mdicapsrv01`

### [[Parameter] Init Details (Environmental Variables & Ignition File)](https://docs.opswat.com/mdcore/advanced-deployment/docker-image-published-on-opswat-docker-hub#parameter-init-details-environmental-variables--ignition-file)

**Argument**: `-v <ignition_folder>:<container_ignition_folder> -e "<env_var>=<value>"`

**Description**:

You must configure MetaDefender ICAP Server(default local admin account, database connection etc.) before running MetaDefender Core docker image. It could be done via either one of following options **( do not use both options**, otherwise the environmental variables will be ignored ):

1. Using environmental variables (`-e`)
2. Using ignition file (`-v`)

**Option 1:**`-e "<env_var>=<value>"` - set an environmental variable to configure, each environmental variable need one -e argument

Available environmental variables:

| name | description | note |
| --- | --- | --- |
| ACCEPT_EULA | Set the ACCEPT_EULA variable to any value to confirm your acceptance of the End-User Licensing Agreement | Default value is **false.** Must set true this ENV to start container. |
| MD_USER | Username to create the first admin user |  |
| MD_PWD | Password to create the first admin user |  |
| MD_EMAIL | Email to create the first admin user |  |
| APIKEY | The API key will be assigned to the admin user for license auto deactivation and activation |  |
| LICENSE_KEY | An license key for license auto activation |  |
| REST_ADDRESS | REST binding address for MetaDefender ICAP Server's Nginx to be allowed |  |
| REST_PORT | REST binding port for MetaDefender ICAP Server's Nginx to be allowed |  |
| ICAP_ADDRESS | ICAP binding address for MetaDefender ICAP Server's Nginx to be allowed |  |
| ICAP_PORT | ICAP binding port for MetaDefender ICAP Server's Nginx to be allowed |  |
| ICAPS_PORT | ICAPS binding port for MetaDefender ICAP Server's Nginx to be allowed |  |
| ICAP_CONF_JSON | MetaDefender ICAP Server configuration file settings, only JSON format is accepted | **For example:** ICAP_CONF_ JSON='{"global/restport": "8009", "logger/loglevel": "info"}' |
| ICAP_DATA_ PATH | a full path to folder (in the container) storing all writable data (engine data, logs, runtime data, etc.). | - Default is */opt/mdicapsrv/icap_data* - Make sure to mount a volume to this folder to run with the policy |
| DATA_DIR | a full path of MetaDefender ICAP Server working data directory | Where ICAP store:   - LDAP Cert - Custom Block Page File Path |
| IMPORT_CONF_FILE | A full path to the file containing the configuration | You need to mount the configuration file to container to use it |
| ICAP_TRUST_CERTS_PATH | A full path to the folder containing the certificate files used to verify MD-Core HTTPS server. | You need to mount the folder containing all certificate files you need to container to use it |
| HTTPS_CERT_PATH | A full path to the folder containing the certificate and private key files used to enable HTTPS. | These files must have the same filename meanwhile their extensions must be .crt and .key  After being added, the filename without extension will be the name of the certificate in MetaDefender ICAP Server |
| ICAPS_CERT_PATH | A full path to the folder containing the certificate and private key files used to enable ICAPS. | These files must have the same filename meanwhile their extensions must be .crt and .key  After being added, the filename without extension will be the name of the certificate in MetaDefender ICAP Server |
| NGINX_CERT_PATH | A full path to the folder containing the certificate and private key files used to enable NGINX Secured Communication. | Supported since MD ICAP Server v5.1.0 |
| TEST_MD_CORE_CONNECTION | Support options test MD Core connection when startup container   - Retry 3 times after the first test failed, 10s delay each time - Exit container when all tests failed | - `true` to enable - `false` to disable - default is `false` |
| AUDIT_DATA_RETENTION | Set time of audit data retention | Default is 168 hours (7 days) |
| HISTORY_DATA_RETENTION | Set time of history data retention | Default is 168 hours (7 days) |
| IGNITION_JSON | The ignition file settings, only JSON format is accepted | **For example:** IGNITION_JSON='{"user/name": "admin", "user/password": "admin", "user/email": "admin@local"}'   - or for enable NGINX integration (supported since MD ICAP Server v5.1.0)   JSON='{"user/name": "admin", "user/password": "admin", "user/email": "admin@local", "nginxsupport/enabled": "true", "nginxsupport/port": "8043", "nginxsupport/ports": "8443"}'   - Or setup PostgreSQL database - (supported since MD ICAP Server v5.2.0)   IGNITION_JSON={"dbserver/private_username": "internal_user", "dbserver/private_password": "internal_user_password"} |
| IMPORT_CONFIG_FILE_PASS | Password for unzip file import config file. **If you use the JSON file, you can let it empty** | supported since MD ICAP Server v5.1.0 |
| NGINX_PORT | NGINX Communication port | 8043 |
| NGINXS_PORT | NGINX Communication SSL/TLS | 8443 |
| IMPORT_CONF_FILE_TARGET | - List of import target for `IMPORT_CONF_FILE`.    - `all` : Import all target   - `schema` : Configuration for Security rules   - `servers` : Configuration for Server profiles   - `global` : Configuration for Global setting   - `history` : Configuration for ICAP history   - `auditlog` : Configuration for Config history   - `session` : Configuration for Security -> Session   - `password-policy` : Configuration for Password policy   - `certs` : Configuration for Certificates. **Notes:** Make sure the path in the config file is valid in the container **(unsupported this from MD ICAP Server v5.2.0)**   - `ssl` : Configuration for Security. It is used to enable/disable HTTPS/ICAPS/NGINXS **(unsupported this from MD ICAP Server v5.2.0)**   - `user-management` : Configuration for User management   - `email`: Configuration for Email Server   - `nginx`: Configuration for NGINX Communication | The `all, user-management` **target will override** `HTTPS_CERT_PATH`, `ICAPS_CERT_PATH`, `NGINX_CERT_PATH`, `MD_USER`, `MD_PWD`, `MD_EMAIL` **only use it if you know what are you doing**. e.g:  `IMPORT_CONF_FILE_TARGET='["servers", "schema"]'` |
| HTTPS_SSL_PROTOCOLS | The version of the TLS for HTTPS | Default value is "TLSv1.3" from MD ICAP Server v5.2.0 (previous default is TLS v1.2) |
| ICAPS_SSL_PROTOCOLS | The version of the TLS for ICAPS | Default value is "TLSv1.3" from MD ICAP Server v5.2.0 (previous default is TLS v1.2) |
| NGINXS_SSL_PROTOCOLS | The version of the TLS for NGINX Communication | Default value is "TLSv1.3" from MD ICAP Server v5.2.0 (previous default is TLS v1.2) |
| ENABLE_HEALTHCHECK | The feature support for service MD ICAP Server run on Kubernetes | Default value is “true”   - Supported since MD ICAP Server 5.2.0 |
| ALLOW_CROSS_IP_SESSIONS | Allow requests coming from sources different from the authenticated origin. | Default value is “true”   - Supported since MD ICAP Server 5.2.0 |
| OLMS_HOST_URL | Define the host url of the `OPSWAT On Prem Licensing Management Server` | Default value is ““   - Supported since MD ICAP Server 5.2.0 |
| OLMS_REST_PORT | Default REST port for the OLMS service | Default value is “443”   - Supported since MD ICAP Server 5.2.0 |
| OLMS_RULE | Default rule for active license on the On-Prem License Manager Server | Default value is ““   - Used for On-prime license manager - Supported since MD ICAP Server 5.2.0 |
| OLMS_SOCKET_PORT | Default Socket port for the OLMS service | Default values:   - Non-secure connection: 3316 - Secure connection: 13316 |
| OLMS_COMMENT | Set the comment for the On-Prem License Manager Server | Default value is ““   - Supported since MD ICAP Server 5.2.0 |
| OLMS_USE_PROXY | optional | **Default**: false  If the user want to use proxy for the OLMS activation  Supported since ICAP v5.6.0 |
| OLMS_PROXY_SERVER | optional | **Default**: empty string  Proxy server address  This field is required if OLMS_USER_PROXY is set to **true**  Supported since ICAP v5.6.0 |
| OLMS_PROXY_PORT | optional | **Default**: empty string  Proxy port  This field is required if OLMS_USER_PROXY is set to **true**  Supported since ICAP v5.6.0 |
| OLMS_PROXY_PROXY_TYPE | optional | **Default**: empty string  Proxy type. Accepted values:   - socks4 - socks5 - http   This field is required if OLMS_USER_PROXY is set to **true**  Supported since ICAP v5.6.0 |
| OLMS_PROXY_USERNAME | optional | **Default**: empty string  Proxy username  Supported since ICAP v5.6.0 |
| OLMS_PROXY_PASSWORD | optional | **Default**: empty string  Proxy password  Supported since ICAP v5.6.0 |
| ENABLE_NGINX | Enable nginx communication with the variable environment | Default value is “false”   - Supported since MD ICAP Server 5.2.0 |
| DB_MODE | Database mode | Required |
| DB_TYPE | Database type | Required |
| DB_HOST | Database host | Required |
| DB_PORT | Database port | Required |
| DB_USER | Database user | Required |
| DB_PWD | Database password | Required |
| MDICAPSRV_INSTANCE_NAME | Instance name | Optional |

Configurations overriding

The priority for overriding configs is: **single environmental variable < JSON environmental variable (IGNITION_JSON, ICAP_CONF_JSON)**

For example, the following command will start a container with `restport=8009`

`docker run -it --name mdicapsrv -p 8048:8009 \`

`-e REST_PORT=8010 \`

`-e IGNITION_JSON='{"user/name": "admin", "user/password": "admin", "user/email": "admin@local"}' \`

`-e ICAP_CONF_JSON='{"global/restport": "8009", "logger/loglevel": "info"}' \`

`-e ICAP_DATA_PATH=/home/icap_data_dir \`

`-e DB_MODE=4 \`

`-e DB_TYPE=remote \`

`-e DB_HOST=10.40.50.99 \`

`-e DB_PORT=5432 \`

`-e DB_USER=postgres \`

`-e DB_PWD=admin \`

`opswat/metadefendericapsrv-centos:5.1.1`

**Option 2:**`-v <ignition_folder>:<container_ignition_folder>` - (optional) mounting the folder containing the ignition file to the container’s folder

- `<ignition_folder>` - ignition folder path containing the ignition file `<ignition_folder>/ometascan.conf`

  - [Deployment automation support](/docs/mdicap/v5.15.0/installation/deployment-automation-supporthhj)
- `<container_ignition_folder>` container’s folder to be mounted to `/opt/ometascan/core_data/opswat` (by default)

**Example**:

Setup the first admin

- user = **admin**
- password = **admin**
- email = **admin@local**
- apikey = **e276cc32f85b6bf312e7a47d6fc5d530f42e**

**Option 1 - using environmental variables**

runCopydocker run -d --name icapsrv \
-e IGNITION_JSON='{"user/name": "admin", "user/password": "admin", "user/email": "admin@local", "user/apikey": "e276cc32f85b6bf312e7a47d6fc5d530f42e"}' \
-e DB_MODE=4 \
-e DB_TYPE=remote \
-e DB_HOST=10.40.50.99 \
-e DB_PORT=5432 \
-e DB_USER=postgres \
-e DB_PWD=admin \
-p 8048:8048 opswat/metadefendericapsrv-centos:5.2.0

**Option 2 - using the ignition file**

runCopymkdir /ignition_folder
touch /ignition_folder/mdicapsrv.conf
# Create /ignition_folder/mdicapsrv.conf based on
# https://docs.opswat.com/mdicap/installation/deployment-automation-support
echo "[user]" >> /ignition_folder/mdicapsrv.conf
echo "name = admin" >> /ignition_folder/mdicapsrv.conf
echo "password = admin" >> /ignition_folder/mdicapsrv.conf
echo "email = admin@local" >> /ignition_folder/mdicapsrv.conf
echo "apikey = e276cc32f85b6bf312e7a47d6fc5d530f42e" >> /ignition_folder/mdicapsrv.conf
echo "[dbserver]" >> /ignition_folder/mdicapsrv.conf
echo "type = remote" >> /ignition_folder/mdicapsrv.conf
echo "host = 10.40.50.99" >> /ignition_folder/mdicapsrv.conf
echo "port = 5432" >> /ignition_folder/mdicapsrv.conf
echo "user = postgres" >> /ignition_folder/mdicapsrv.conf
echo "password = 123" >> /ignition_folder/mdicapsrv.conf
docker run -d --name icap \
-v /ignition_folder:/opt/mdicapsrv/icap_data/opswat \
-p 8048:8048 \
opswat/metadefendericapsrv-centos:5.2.0
### [Volumes](/docs/mdicap/v5.15.0/installation/docker-image-published-on-opswat-docker-hubd93#volumes)

| **Name** | **Detail** | Default |
| --- | --- | --- |
| OS_CERTS_STORE_PATH | Where OS use for store the certificates  Needed when read-only file system or non-root privileges | **CentOS**  `/etc/pki/ca-trust`  **Debian**  `/etc/ssl/certs` |
| OS_CERTS_INSTALL_PATH | Where OS read the certificates to install  Needed when read-only file system or non-root privileges | **CentOS**  `/etc/pki/ca-trust/source/anchors/`  **Debian**  `/usr/local/share/ca-certificates/` |
| SYSTEM_DIR | Temp system path for ICAP Server running | `/opt/mdicapsrv/system` |
| ICAP_DATA_PATH | A full path to the folder (in the container) storing all writable data (engine data, logs, runtime data, etc.). | `/opt/mdicapsrv/icap_data` |
| PW_PATH | Store users and groups to which users belong under Linux and UNIX operating system (/etc/group, /etc/passwd) | `/mdicapsrv/pw` |
