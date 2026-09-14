<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-am-i-getting-a--stat--etc-mdss-docker-compose-onedrive-yml-- -->

# Why am I getting a "stat /etc/mdss/docker-compose.onedrive.yml: no such file or directory" error when upgrading MetaDefender Storage Security from 3.6.1 to 4.1.0?

This article applies to MetaDefender Storage Security versions v4.1.0 deployed on Linux systems.

### [**Issue**](/docs/mdss/knowledge-base/why-am-i-getting-a--stat--etc-mdss-docker-compose-onedrive-yml--#issue)

During an upgrade from **MetaDefender Storage Security** version **3.6.1** to **4.1.0**, you may encounter the following error:

`[error] stat /etc/mdss/docker-compose.onedrive.yml: no such file or directory [emergency] Cannot pull containers`

This error occurs when the `ENABLED_MODULES` variable in the configuration file `/etc/mdss/customer.env` includes the value `onedrive`, which is no longer valid in version 4.1.0.

### [**Cause**](/docs/mdss/knowledge-base/why-am-i-getting-a--stat--etc-mdss-docker-compose-onedrive-yml--#cause)

In version 4.1.0, the `/etc/mdss/docker-compose.onedrive.yml` has been replaced by the `/etc/mdss/docker-compose.graph.yml`.

The upgrade process expects the updated module name, and referencing `onedrive` in customer.env causes it to look for a non-existent configuration file (`docker-compose.onedrive.yml`), resulting in the error.

### [**Resolution**](/docs/mdss/knowledge-base/why-am-i-getting-a--stat--etc-mdss-docker-compose-onedrive-yml--#resolution)

To fix the issue:

1. Open the file `/etc/mdss/customer.env`.
2. Locate the line that starts with `ENABLED_MODULES=`.

3. If `onedrive` is listed, replace it with `graph`.

**Example:**

- **Before:** ENABLED_MODULES=smb,box,**onedrive**,sftp,nfs,mft,ftp
- **After:** ENABLED_MODULES=smb,box,**graph**,sftp,nfs,mft,ftp

4. Save the file and re-run the upgrade command: `sudo mdss -u update`

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
