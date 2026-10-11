<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me -->

# How to Reduce the High Memory Usage on the SQL Server Used by MetaDefender MFT?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Check Your Version:**

This article applies to all MetaDefender Managed File Transfer releases.

## [**Summary**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#summary)

When MetaDefender Managed File Transfer (MFT) is configured to use an external Microsoft SQL Server, administrators may observe high memory usage on the SQL Server machine. This behavior is **expected** and is related to SQL Server’s built-in memory management and caching mechanisms.
However, if SQL Server consumes too much memory, it may reduce system responsiveness, so setting a **maximum memory limit** for SQL Server would resolve the issue.

---

## [**Issue**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#issue)

The SQL Server connected to MetaDefender MFT shows **high RAM utilization,** and the server may become slow or unresponsive. Symptoms can include:

- Slow MFT application responses when performing SQL queries
- Delayed backups, monitoring operations, or scheduled tasks
- High page file usage (disk swapping)
- General OS sluggishness on the SQL Server host

---

## [**Cause**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#cause)

This is not a defect in MetaDefender MFT.
The behavior is caused by **SQL Server’s intentional memory caching strategy**.

SQL Server is designed to use as much memory as possible to cache:

- Data pages
- Execution plans
- Indexes

This design leads to SQL Server:

- **Allocating RAM up to the available system limit**
- **Holding onto memory even when the workload decreases**
- **Not automatically releasing memory** unless OS memory pressure occurs or a hard memory cap is set

Because SQL Server aggressively caches, it may starve the operating system or other applications, causing performance issues.

---

## [**Resolution**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#resolution)

Configure SQL Server’s **Maximum Server Memory** setting to ensure the operating system and other services retain sufficient RAM.

### [**Recommended Rule**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#recommended-rule)

Leave **at least 4 GB** (or more, depending on the server role) for the OS and background services.

#### [**Example**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#example)

For a SQL Server host with **20 GB RAM**:

- Required for OS + background services: **~4 GB**
- Recommended SQL Server max memory: **16 GB**

This prevents SQL Server from consuming all available RAM and ensures stable system performance.

---

## [**How to Set the Maximum Memory Limit in SQL Server**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#how-to-set-the-maximum-memory-limit-in-sql-server)

1. Open **SQL Server Management Studio (SSMS)**
2. Connect to your SQL Server instance
3. Right-click the server name → **Properties**
4. Navigate to the **Memory** page
5. Under *Server Memory Options*, set:

   - **Maximum server memory (in MB)** → enter the desired limit (e.g., 16000 MB for 16 GB)
6. Click **OK** to apply the new memory configuration

The change takes effect immediately and does not require a SQL Server restart.

---

## [**Additional Notes**](/docs/mdmft/v3.11.5/knowledge-base/how-to-reduce-the-high-memory-usage-on-the-sql-server-used-by-me#additional-notes)

- This configuration is safe and recommended in most production environments.
- You may need to adjust values based on:

  - Total server RAM
  - Number of instances
  - Other applications on the server
- Monitoring tools such as Task Manager may still show SQL Server holding allocated memory, but it will no longer grow beyond the configured limit.

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
