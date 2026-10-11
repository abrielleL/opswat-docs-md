<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-am-i-getting-a--stat--etc-mdss-docker-compose-onedrive-yml-- -->

# Why am I getting a "stat /etc/mdss/docker-compose.onedrive.yml: no such file or directory" error when upgrading MetaDefender Storage Security from 3.6.1 to 4.1.0?

> **Check Your Version:**
>
> This article applies to the upgrade from MetaDefender Storage Security **3.6.1** to **4.1.0** on Linux systems. Starting with 4.6.0, the upgrade no longer fails on an unknown module name: a value in `ENABLED_MODULES` that has no matching compose file is skipped silently. Replacing `onedrive` with `graph` is still recommended, because `onedrive` no longer enables anything.

### **Issue**

During an upgrade from **MetaDefender Storage Security** version **3.6.1** to **4.1.0**, you may encounter the following error:

![](https://uploads.developerhub.io/prod/k8zL/hy9pf7sfrg7a9ppell9jr0a0jy8xeht7qh87p52gqfuv4y8wauftz6ha8tr8ljw2.png)

`[error] stat /etc/mdss/docker-compose.onedrive.yml: no such file or directory [emergency] Cannot pull containers`

This error occurs when the `ENABLED_MODULES` variable in the configuration file `/etc/mdss/customer.env` includes the value `onedrive`, which is no longer valid in version 4.1.0.

### **Cause**

In version 4.1.0, the `onedrive` module was renamed to `graph`, and the `/etc/mdss/docker-compose.onedrive.yml` file was replaced by `/etc/mdss/docker-compose.graph.yml`.

The upgrade process expects the updated module name, and referencing `onedrive` in customer.env causes it to look for a non-existent configuration file (`docker-compose.onedrive.yml`), resulting in the error.

### **Resolution**

To fix the issue:

1. Open the file `/etc/mdss/customer.env`.
2. Locate the line that starts with `ENABLED_MODULES=`.

![](https://uploads.developerhub.io/prod/k8zL/vqqn600c2y122jidplnsp4q4m55tyvdxly7fnb1yn8us1xqvw1z58lpi7w2bfn3a.png)

3. If `onedrive` is listed, replace it with `graph`.

![](https://uploads.developerhub.io/prod/k8zL/5ai2azty9ydfykhy3dgd5wwd45e39q7w16y4qsm49vkzctso5iu00il53ahbczwd.png)

**Example:**

- **Before:** ENABLED_MODULES=smb,box,**onedrive**,sftp,nfs,mft,ftp
- **After:** ENABLED_MODULES=smb,box,**graph**,sftp,nfs,mft,ftp

4. Save the file and re-run the upgrade command: `sudo mdss -u update`

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
