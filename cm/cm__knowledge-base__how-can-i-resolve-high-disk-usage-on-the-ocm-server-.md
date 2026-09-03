<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-resolve-high-disk-usage-on-the-ocm-server- -->

# How Can I Resolve High Disk Usage on the OCM Server?

Please note this article addresses high disk usage specifically in scenarios where OCM manages Cores. It may not apply to all use cases.

#### **Issue**:

High disk usage observed on the OCM server, particularly under the path:

**C:\ProgramData\OPSWAT\Central\Data**

This folder contains **WT files** associated with the **MongoDB database. Do not delete these files manually** as it may corrupt database integrity.

#### **Recommended Actions:**

To address and reduce disk usage safely, follow the steps below:

1. **Clean Up Data from the OCM Side**

Use the **Processing History → Clean Up** feature within the OCM UI.

- This action allows you to remove old processing history safely.
- Follow the official guide here: [OCM Processing History Cleanup Documentation](https://www.opswat.com/docs/ocm/integrations/processing-history)

2. **Adjust Data Retention on MD Core**

Reduce the data retention period or manually clean up old data stored by MD Core.

- This helps limit the buildup of historical data that may not be needed long-term.
- Follow the official configuration instructions here: [MD Core Data Retention Configuration](https://www.opswat.com/docs/mdcore/configuration/data-retention)

> **Support:**
>
> If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
