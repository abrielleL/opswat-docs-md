<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/why-am-i-receiving-the-error--postgresql-migrations-did-not-fini -->

# Why am I receiving the error "PostgreSQL migrations did not finish" when installing MetaDefender Storage Security?

> **Check Your Version:**
>
> This article applies to MetaDefender Storage Security v4.0.x releases deployed on Windows  systems.

### Issue:

- When installing MetaDefender Storage Security on Windows server, the error "PostgreSQL migrations did not finish after 10000 retries. Please check logs for any issues.“ is received, even on a fresh installation.

![](https://uploads.developerhub.io/prod/k8zL/142suyl9u73aaa4r14cami1fg3wtxwd9kh19u5mlrkrfeu9kf6nbctlsvtft939v.png)

### Main Cause:

- This occurs because MetaDefender Storage Security was previously installed on the machine but not completely removed after an uninstall or problem. This leftover data causes the installer to recognize an existing installation and attempt an upgrade instead of a fresh install.

![](https://uploads.developerhub.io/prod/k8zL/rzutix3jb4ym4duhag89ul27geld03dukpgl6b6xmdhelzh4vsb9m5grlaexlueo.png)

### Resolution:

Please follow the steps below to safely remove and reinstall MetaDefender Storage Security (MDSS):

### **1. Stop MDSS Services**

Stop all related MDSS services from **Services (services.msc)** or by using the following commands:

```plaintext
net stop mdss
net stop mdss_postgresql
net stop mdss_rabbitmq
```

---

### **2. Remove MDSS Windows Services**

Run the following commands as Administrator to remove existing services:

```plaintext
sc.exe delete "mdss_postgresql"
sc.exe delete "mdss_rabbitmq"
sc.exe delete "mdss"
```

---

### **3. Remove Installation Directory**

Delete the default installation folder:

```plaintext
C:\Program Files\OPSWAT\MetaDefender Storage Security
```

Ensure all files are removed.

---

### **4. Handle Locked Files (if any)**

If some files cannot be deleted:

- Ensure all MDSS services are stopped
- Close any open log files
- Restart the system if needed

**Advanced:**

- Use [**Process Explorer**](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer) to identify which process is locking the files

---

### **5. Remove Registry Entry**

Clean up the registry by running:

```plaintext
reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MetaDefender Storage Security" /f
```

---

### **6. Reboot the System**

Restart the machine to ensure all remaining components are fully cleared.

### **7. Reinstall MDSS**

Run the installer again after completing all steps above.

> **Support:**
>
> If Further Assistance is required, please proceed to [create a support case or chat with our support engineer.](https://my.opswat.com/portal/support-services)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
