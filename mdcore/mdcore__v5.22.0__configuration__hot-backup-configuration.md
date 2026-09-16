<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/hot-backup-configuration -->

# Hot Swap Backup Configuration

MetaDefender Core version 5.0.0 or newer

Hot backup mode supports you to register (activate) as many MetaDefender Core instances as you might need for backup purpose, and those backup instance(s) should be ready to take over with your active / production MetaDefender Core instance whenever applicable.

With engines and configurations ready to use, that helps mitigate any down time in scanning system in case of your recovery disaster plan needs to be triggered.

MetaDefender Core backup instance(s), once registered properly, does not accumulate into your actual license activation slots, that means, you will not be required to purchase additional product license just for this backup purpose alone.

What is allowed

MetaDefender Core backup instance, upon activated in the backup mode, allowing you to:

- Download and deploy licensed engines (modules), proceed them all to active mode.
- Modify MetaDefender Core and its engines (modules) settings.
- Import MetaDefender Core settings.
- Access and administrate all other operations on MetaDefender Core management console.
What is not allowed

The only thing that MetaDefender Core backup instance(s) does not allow is accepting any scan requests coming, and processing them.

## [Register a backup instance](/docs/mdcore/v5.22.0/configuration/hot-backup-configuration#register-a-backup-instance)

1. Online environment: Using following REST API: [POST - Setup hot-backup instance](/docs/mdcore/v5.22.0/metadefender-core#postlicensebackup)
2. Offline environment:

- Obtain `license.yml` file that supposed to use to active your MetaDefender Core active / production instance before.
- Using following REST API: [POST - Setup hot-backup instance](/docs/mdcore/v5.22.0/metadefender-core#postlicensebackup) with that yaml file content.

Note

If you try to activate a MetaDefender Core instance which is currently registered as a backup one (using [POST - Activate license online](/docs/mdcore/v5.22.0/metadefender-core#licenseactivation)) then expecting to hit error. Instead you should **either** do following:

1. Nominate that backup instance (see below)
2. Unregister that backup instance (see below), and then activate it using [POST - Activate license online](/docs/mdcore/v5.22.0/metadefender-core#licenseactivation)
Register backup on an active / production instance

You cannot register a MetaDefender Core as a backup instance when it is still running as an active / production one.

Instead, you are required to deactivate that instance first.

## [Unregister a backup instance](/docs/mdcore/v5.22.0/configuration/hot-backup-configuration#unregister-a-backup-instance)

This step will be required when following circumstances happen:

1. You want to activate that backup instance directly without using nomination method (see below) via [POST - Activate license online](/docs/mdcore/v5.22.0/metadefender-core#licenseactivation)
2. You want to shutdown that backup instance for some reasons, but avoid removing the container or system where that MetaDefender Core instance is installed on for possible usage later.

Using following REST API: [DELETE - Remove a backup instance](/docs/mdcore/v5.22.0/metadefender-core#removebackupinstance)

Upon unregistered successfully, that MetaDefender Core instance will no longer allow you to:

- Download engines and their databases from OPSWAT update server source (online mode)
- Upload engines and their databases manually
- Deploy engines and their databases on MetaDefender Core

Basically that MetaDefender Core will become an unlicensed one as a fresh installation.

## [Nominate a backup instance](/docs/mdcore/v5.22.0/configuration/hot-backup-configuration#nominate-a-backup-instance)

Nominating a backup instance is to make that instance become an active / production one. That means, your nominated instance will be able to process files as in production.

**Online environment:** Using following REST API: [POST - Nominate a backup instance to a production instance](/docs/mdcore/v5.22.0/metadefender-core#licensebackupnomination)

Expected behaviors:

When the backup instance is successfully nominated to be a new active / production one, then expecting following behaviors:

- The backup instance's actual deployment ID will be registered with relevant license key on our OPSWAT Licensing system, and it is then able to process processing requests right away.
- The former active / production instance (before the nomination took place), will be auto unregistered from OPSWAT Licensing system.

**Offline environment:** You are not allowed to directly nominate a MetaDefender Core backup instance which was previously registered in offline mode.

Nominating MetaDefender Core backup instance in offline mode

Instead, following actions needs to be made as alternative procedure:

- Manually deactivate your MetaDefender Core active / production instance first, and unregister it from OPSWAT Licensing system.
- Unregister your MetaDefender Core backup instance.
- Then, activate your MetaDefender Core backup instance as a production one.
