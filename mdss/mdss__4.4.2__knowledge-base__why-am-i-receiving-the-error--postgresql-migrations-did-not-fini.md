<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini -->

# Why am I receiving the error "PostgreSQL migrations did not finish" when installing MetaDefender Storage Security?

This article applies to MetaDefender Storage Security v4.0.x releases deployed on Windows systems.

### [Issue:](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#issue)

- When installing MetaDefender Storage Security on Windows server, the error "PostgreSQL migrations did not finish after 10000 retries. Please check logs for any issues.“ is received, even on a fresh installation.

### [Main Cause:](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#main-cause)

- This occurs because MetaDefender Storage Security was previously installed on the machine but not completely removed after an uninstall or problem. This leftover data causes the installer to recognize an existing installation and attempt an upgrade instead of a fresh install.

### [Resolution:](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#resolution)

Please follow the steps below to safely remove and reinstall MetaDefender Storage Security (MDSS):

### [**1. Stop MDSS Services**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#1-stop-mdss-services)

Stop all related MDSS services from **Services (services.msc)** or by using the following commands:

net stop mdss
net stop mdss_postgresql
net stop mdss_rabbitmq

---

### [**2. Remove MDSS Windows Services**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#2-remove-mdss-windows-services)

Run the following commands as Administrator to remove existing services:

sc.exe delete "mdss_postgresql"
sc.exe delete "mdss_rabbitmq"
sc.exe delete "mdss"

---

### [**3. Remove Installation Directory**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#3-remove-installation-directory)

Delete the default installation folder:

C:\Program Files\OPSWAT\MetaDefender Storage Security

Ensure all files are removed.

---

### [**4. Handle Locked Files (if any)**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#4-handle-locked-files-if-any)

If some files cannot be deleted:

- Ensure all MDSS services are stopped
- Close any open log files
- Restart the system if needed

**Advanced:**

- Use [**Process Explorer**](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer) to identify which process is locking the files

---

### [**5. Remove Registry Entry**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#5-remove-registry-entry)

Clean up the registry by running:

reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MetaDefender Storage Security" /f

---

### [**6. Reboot the System**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#6-reboot-the-system)

Restart the machine to ensure all remaining components are fully cleared.

### [**7. Reinstall MDSS**](/docs/mdss/4.4.2/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini#7-reinstall-mdss)

Run the installer again after completing all steps above.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer.](https://my.opswat.com/portal/support-services)
