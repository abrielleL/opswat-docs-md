<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab -->

# How to disable the Local PostgreSQL when using an external Database?

This article applies to MetaDefender Storage Security v4.x

### [**Overview**](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#overview)

If you prefer to connect the MetaDefender Storage Security (MDSS) application to your own [remote PostgreSql](/docs/mdss/4.4.2/metadefender-storage-security/4.0.0/installation/windows-deployments#how-to-setup-an-external-postgresql-in-metadefender-storage-security) database server, you can disable the built-in PostgreSql container and its related references by editing the Docker Compose files. While the bundled PostgreSql service consumes minimal resources when idle, you can still reclaim those resources by following the steps below.

---

### [**Instructions**](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#instructions)

#### [1. Stop the MDSS Application](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#1-stop-the-mdss-application)

Before making any configuration changes, stop the MDSS services:

PowershellCopysudo mdss -c stop

---

#### [2. Disable the Built-in PostgreSql Container](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#2-disable-the-built-in-postgresql-container)

Open the following file in a text editor: `/etc/mdss/docker-compose.main.yml`

Locate the `postgresql` service section and **add the following**:

PowershellCopyprofiles:
- disabled
#### [3. Start the MDSS Application](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#3-start-the-mdss-application)

Once all modifications are complete, start the MDSS services again:

PowershellCopysudo mdss -c start

---

### [**Verification**](/docs/mdss/4.4.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab#verification)

After restarting, verify that:

- MDSS is running without the internal PostgreSql container.
- The application is successfully connected to your external PostgreSql server.

You can check logs or test basic application functionality to ensure a proper connection.

---

Support:

If you have followed all of the steps above but are still experiencing issues, please follow these instructions on [how to generate a Support Package](https://www.opswat.com/docs/mdss/where-to-get-help/how-to-generate-a-support-package) before [creating a support case or chatting with one of our support engineers.](https://my.opswat.com/support)
