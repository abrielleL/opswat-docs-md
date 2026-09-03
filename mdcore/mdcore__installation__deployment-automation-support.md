<!-- source: https://www.opswat.com/docs/mdcore/installation/deployment-automation-support -->

# Deployment automation support

An Ignition file could be utilized for either / both of following use-cases:

1. Pre-define PostgreSQL server information for MetaDefender Core to connect and setup database: only required on Linux installation, or Windows with command line installation. Learn more details at:

   1. [Standalone Mode > Command Line Installation](/docs/mdcore/installation/standalone-mode#command-line-installation) ( applicable on version 4.19.0 or newer).
   2. [Shared Database Mode > Command Line Installation](/docs/mdcore/installation/shared-database-mode#command-line-installation) (only applicable on version 4.20.0 or newer).
2. Automating to accept EULA, create a default local admin user and import MetaDefender Core configurations upon installed: Those steps could be automated using ignition file described in this page.

Ignition file location to create:

- **Windows***:*`C:\OPSWAT\ometascan.conf`
- **Linux**: `/etc/opswat/ometascan.conf`

The product supports fully automated deployment. It means that it can be installed and configured with no human interaction.

The automated deployment can be split to three steps on a high level:

1. Installation
2. Initialization
3. Configuration

## [Installation](/docs/mdcore/installation/deployment-automation-support#installation)

To automate the installation, install the product from the command line and provide the installation-time options as parameters to the installer. For further details see [Command Line Installation](/docs/mdcore/installation/standalone-mode#command-line-installation)

After the installation is complete, the product starts up and waits in a pre-initialized status. The product may be initialized in two ways:

1. Manually using the [Wizard Setup](/docs/mdcore/installation/initial-setup-using-configuration-wizard) or
2. Automatically using an *ignition file* (see below).

Warning

If the automated initialization fails for some reason (e.g. the ignition file is not in place) then the automated initialization may be retried after fixing the problem (e.g. placing the ignition file in its lookup location) and restarting the OPSWAT MetaDefender Core service.

Until the product is in pre-initialized status, it will try the automated initialization every time after a service (re)start.

## [Initialization](/docs/mdcore/installation/deployment-automation-support#initialization)

Initialization is the process of bringing the product to an operable status.

Basically the initialization consists of the following steps:

1. Accept the End User License Agreement (EULA),
2. Import product configuration and
3. Create the first administrator user account.

## [Ignition file](/docs/mdcore/installation/deployment-automation-support#ignition-file)

The initialization process can be configured in a file called the *ignition file*.

Please check more details if you have special characters in Ignition file: [Ignition file - special characters](/docs/mdcore/installation/ignition-file-----special-characters)

Warning

In Linux, the ignition file and the folder /etc/opswat should have the permission 755 and must be in **conf** format.

### [Ignition file location](/docs/mdcore/installation/deployment-automation-support#ignition-file-location)

- **Windows:** `C:\OPSWAT\ometascan.conf`
- **Linux:**`/etc/opswat/ometascan.conf`

Example:

ometascan.confCopyeula=true
[user]
name=admin
password=admin
email=admin@local
apikey=44c96cbb4e4e6c0a1d16bcb3c3da24def317
[config]
import=config_package.zip
import_password=123
[security]
session_cookie_samesite=Lax
[internal]
skip_startup_pages=true
skip_upgrade_scan_data=false
[dbserver]
type=local
host=localhost
port=5432
user=postgres
password=non_Unicode_password
private_username=my_internal_db_user
private_password=mypassword
[ocm]
ocm_url=https://my.opswat.com
reg_code=XXXXXXXX
[max_body_size]
body_size=body_size_in_byte
[https]
cert_name=my_cert_name
cert_path=C:/OPSWAT//certs/server.crt
key_path=C:/OPSWAT/certs/server.key
passphrase=my_pass_if_any
tls_version=1.2,1.3
### [Ignition file fields](/docs/mdcore/installation/deployment-automation-support#ignition-file-fields)

The ignition file accepts the following fields:

### [Detailed initialization process](/docs/mdcore/installation/deployment-automation-support#detailed-initialization-process)

1. After the product has been started, it looks for the ignition file in the designated location.

- **Windows**: `C:\OPSWAT\ometascan.conf`
- **Linux**: `/etc/opswat/ometascan.conf`

2. If an ignition file is found, then

2.1) It gets validated, and if it is valid, then based on the information found in the ignition file:

- The EULA is accepted,
- The configuration is imported,
- The administrator account is created.
- If any of the above steps fails, then the error is logged, and the initialization gets terminated.

Info

In this case the product starts normally: if for example the basic configuration wizard has not been completed yet, then it must be completed first.

2.2) If it is not valid, then the error is logged, and the initialization gets terminated.

Info

In this case the product starts normally: if for example the basic configuration wizard has not been completed yet, then it must be completed first.

3. If there is no ignition file, then no initialization is performed.

Info

In this case the product starts normally: if for example the basic configuration wizard has not been completed yet, then it must be completed first.

Warning

If the automated initialization fails for some reason (e.g. the ignition file is not in place) then the automated initialization may be retried fixing the problem (e.g. placing the ignition file to its lookup location) and restarting the OPSWAT MetaDefender Core service.

Until the product is in pre-initialized status, it will try the automated initialization every time after a service (re)start.

## [Configuration](/docs/mdcore/installation/deployment-automation-support#configuration)

After initialization is complete, the product is ready with both the default and imported configurations.

This configuration can be later changed by calling the configuration API functions. For further details about the API, see [Configuration related APIs](/docs/mdcore/metadefender-core#tag-config)
