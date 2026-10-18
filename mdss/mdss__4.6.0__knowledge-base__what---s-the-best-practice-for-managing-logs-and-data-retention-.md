<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/what---s-the-best-practice-for-managing-logs-and-data-retention- -->

# What’s the Best Practice for Managing Logs and Data Retention in MDSS?

> **Check Your Version:**
>
> This article applies to MetaDefender Storage Security versions up to 3.5.1

If you're experiencing storage issues on your MetaDefender Storage Security (MDSS) deployment, there are several strategies you can use to manage and free up disk space. This article outlines recommended practices for monitoring storage, adjusting configurations, and leveraging built-in features to maintain system performance and availability.

### Recommended Actions

#### 1.Configure Database Retention

To help manage storage usage, you can configure the system to automatically delete older records from the MDSS database. This helps prevent data buildup and keeps your storage usage under control. Refer to this support article: [Database Retention](https://www.opswat.com/docs/mdss/configuration/database-retention)

- **Enable automatic cleanup for the following record types:**
  - Audit records
  - Report records
  - Real-time processing history
- **Set retention periods** to define how many days these records are kept before being automatically deleted.
- **Lower retention thresholds** as needed to reduce overall database size and free up space.

#### 2. **Increase Disk Size for Key Directories**

Especially on Linux-based installations, directories like `/var` often store temporary files related to file scans and remediation. If storage is running low:

- Extend the disk size allocated to MDSS.
- **Recommended formula:**
- *Temporary space ≥ 2 × (Size of the largest file in GB)**

#### 3. **Regularly Monitor Disk Space**

- Regularly monitor disk space and identify large directories or files that may be consuming excessive storage.

#### 4. **Extend** `/var` **if Remediation Files Are Large**

If remediation actions produce temporary files that fill up your `/var` directory:

- Consider resizing or extending the `/var` partition.
- Monitor this location closely, especially if you process large files.

#### 5. **Cloud Deployments: Use Native Monitoring Tools**

If you’ve deployed MDSS in a cloud environment (e.g., AWS, Azure, GCP):

- Use built-in monitoring tools to track disk space.
- Set up automated alerts when usage reaches critical thresholds.

#### 6. **Upgrade to the Latest Version**:

If you are using an older version of MDSS, upgrade to the latest version as it may include improvements for storage management. You can check and download the latest version by logging in to [**My OPSWAT**](https://my.opswat.com/) and navigating to "Product Downloads".

**Performance Limitations on Windows**:

- Be aware that on Windows, each Docker container can only be assigned 2GB of RAM, which may impact performance. Consider moving to MDSS Linux for better resource management if possible

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
