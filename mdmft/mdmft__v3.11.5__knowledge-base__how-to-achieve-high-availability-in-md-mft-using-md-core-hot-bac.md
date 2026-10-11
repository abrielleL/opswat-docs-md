<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-achieve-high-availability-in-md-mft-using-md-core-hot-bac -->

# How to Achieve High Availability in MD MFT Using MD Core Hot Backup?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [**Overview**](/docs/mdmft/v3.11.5/knowledge-base/how-to-achieve-high-availability-in-md-mft-using-md-core-hot-bac#overview)

**MetaDefender MFT** does **not natively support high availability (HA)**. However, it can be integrated with a **Core Hot Backup** architecture to improve redundancy and fault tolerance. This article outlines recommended approaches and considerations for setting up HA using **MetaDefender Core Hot Backup**, particularly in deployments involving MFT.

## [**Deployment Scenario**](/docs/mdmft/v3.11.5/knowledge-base/how-to-achieve-high-availability-in-md-mft-using-md-core-hot-bac#deployment-scenario)

In a typical HA/DR architecture, the setup includes:

- **Two Active Core instances**
- **Two Hot Backup Core instances**
- **Separate or shared databases depending on setup**
- **One MFT instance per security zone (e.g., Low and High)**
- **Possibly a Load Balancer (LB) between MFT and Core**

This configuration supports high availability across multiple locations or zones and can be extended to disaster recovery (DR) scenarios.

## [**Key Considerations**](/docs/mdmft/v3.11.5/knowledge-base/how-to-achieve-high-availability-in-md-mft-using-md-core-hot-bac#key-considerations)

🔹 **1. Database Synchronization**

- If each Core instance uses a **standalone local database**, there is **no built-in synchronization** between the active and hot-backup instances.

**Impact:** Data processed by the active Core cannot be retrieved by the hot-backup instance.

- To enable data continuity:

Use a [**shared remote database**](https://www.opswat.com/docs/mdcore/installation/shared-database-mode) with:

db_type = remote

db_mode = 4

This configuration allows the hot-backup Core instance to access the same database as the active instance, preserving file history and scan records during failover.

🔹 **2. Load Balancer and Failover Automation**

- **Load Balancer Use:**

A Load Balancer can help route MFT traffic to an active Core instance.

However, since **failover is not automatic**, the Load Balancer **alone cannot manage the switch** between active and hot-backup instances.

- **Manual Promotion Required:**

If the active Core instance fails, the hot-backup instance must be **manually promoted** via:

MetaDefender Core **UI**, or

**REST API**

- **Automated Promotion (Recommended Workaround):**

Implement a **custom monitoring mechanism** that:

Detects failure of the active Core instance

Executes a **script** to:

Promote the hot-backup Core

Update the Core URL in the MFT configuration

🔹 **3. High-Security Environments**

- In use case, where Core instances are deployed on both **Low** and **High security sides**, each side can maintain its **own shared database** with **replication** for disaster recovery.
- This setup ensures isolation and compliance while supporting failover at each zone.

Support:

If **Further Assistance** is required, please proceed to log a [****support case or chatting with our support engineer****](https://my.opswat.com/support).
