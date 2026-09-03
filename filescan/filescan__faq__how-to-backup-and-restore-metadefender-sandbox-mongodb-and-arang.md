<!-- source: https://www.opswat.com/docs/filescan/faq/how-to-backup-and-restore-metadefender-sandbox-mongodb-and-arang -->

# How to Backup and Restore MetaDefender Aether MongoDB and ArangoDB?

This article applies to all MetaDefender Aether releases.

## [Overview](/docs/filescan/faq/how-to-backup-and-restore-metadefender-sandbox-mongodb-and-arang#overview)

This article explains how to back up and restore the MetaDefender Aether MongoDB and ArangoDB databases.

## [**Backup procedure**](/docs/filescan/faq/how-to-backup-and-restore-metadefender-sandbox-mongodb-and-arang#backup-procedure)

**Preferred method:** Create a full system snapshot.

**Alternative method:** Manually back up the `/data` folder, which contains both **MongoDB** and **ArangoDB** databases.

#### [Steps:](/docs/filescan/faq/how-to-backup-and-restore-metadefender-sandbox-mongodb-and-arang#steps)

1. **Stop the sandbox service:**

sudo service sandbox stop

2. **Back up the** `/data` **folder:**

sudo cp -R /data/* /YOUR/BACKUP/FOLDER

3. **Restart the sandbox service:**

sudo service sandbox startNote:

It is strongly recommended to store the backup on a separate disk or network share to safeguard against potential disk failures.

## [**Restore procedure**](/docs/filescan/faq/how-to-backup-and-restore-metadefender-sandbox-mongodb-and-arang#restore-procedure)

1. **Stop the sandbox service:**

sudo service sandbox stop

2. **Remove existing database files:**

sudo rm -rf /data/db/fsio/*
sudo rm -rf /data/graphdb/fsio/*

3. **Restore the backup to** `/data`**:**

sudo cp -R /YOUR/BACKUP/FOLDER/* /data/

4. **Start the sandbox service:**

sudo service sandbox startSupport:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
