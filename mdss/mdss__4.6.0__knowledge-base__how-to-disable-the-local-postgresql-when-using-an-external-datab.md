<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-to-disable-the-local-postgresql-when-using-an-external-datab -->

# How to disable the Local PostgreSQL when using an external Database?

> **Check Your Version:**
>
> This article applies to MetaDefender Storage Security v4.x

### **Overview**

If you prefer to connect the MetaDefender Storage Security (MDSS) application to your own [remote PostgreSql](https://www.opswat.com/docs/mdss/installation/windows-deployments#how-to-setup-an-external-postgresql-in-metadefender-storage-security) database server, you can disable the built-in PostgreSql container so that it is not deployed. The bundled PostgreSQL container is tuned to use a share of the host memory (on Linux, shared buffers are set to 25% of RAM at installation), so disabling it frees those resources. Follow the steps below.

---

### **Instructions**

#### 1. Stop the MDSS Application

Before making any configuration changes, stop the MDSS services:

```powershell
sudo mdss -c stop
```

---

#### 2. Disable the Built-in PostgreSql Container

Open the file `/etc/mdss/customer.env` in a text editor and add `postgres` to the `DISABLED_SERVICES` variable (create the line if it does not exist):

```bash
DISABLED_SERVICES=postgres
```

`DISABLED_SERVICES` accepts a comma-separated list, so other externally managed services can be listed alongside it, for example `DISABLED_SERVICES=postgres,rabbitmq,redis`. See [How to Enable Specific Modules in the Configuration?](https://www.opswat.com/docs/mdss/knowledge-base/how-to-enable-specific-modules-in-the-configuration) for details.

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
