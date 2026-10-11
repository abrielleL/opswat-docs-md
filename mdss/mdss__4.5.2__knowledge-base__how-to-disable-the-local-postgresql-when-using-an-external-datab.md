<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab -->

# How to disable the Local PostgreSQL when using an external Database?

> **Check Your Version:**
>
> This article applies to MetaDefender Storage Security v4.x

### **Overview**

If you prefer to connect the MetaDefender Storage Security (MDSS) application to your own [remote PostgreSql](https://www.opswat.com/docs/mdss/installation/windows-deployments#how-to-setup-an-external-postgresql-in-metadefender-storage-security) database server, you can disable the built-in PostgreSql container and its related references by editing the Docker Compose files. While the bundled PostgreSql service consumes minimal resources when idle, you can still reclaim those resources by following the steps below.

---

### **Instructions**

#### 1. Stop the MDSS Application

Before making any configuration changes, stop the MDSS services:

```powershell
sudo mdss -c stop
```

---

#### 2. Disable the Built-in PostgreSql Container

Open the following file in a text editor: `/etc/mdss/docker-compose.main.yml`

Locate the `postgresql` service section and **add the following**:

```powershell
profiles:
     - disabled
```

#### 3. Start the MDSS Application

Once all modifications are complete, start the MDSS services again:

```powershell
sudo mdss -c start
```

---

### **Verification**

After restarting, verify that:

- MDSS is running without the internal PostgreSql container.
- The application is successfully connected to your external PostgreSql server.

You can check logs or test basic application functionality to ensure a proper connection.

---

> **Support:**
>
> If you have followed all of the steps above but are still experiencing issues, please follow these instructions on [how to generate a Support Package](https://www.opswat.com/docs/mdss/where-to-get-help/how-to-generate-a-support-package) before [creating a support case or chatting with one of our support engineers.](https://my.opswat.com/support)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
