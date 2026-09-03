<!-- source: https://www.opswat.com/docs/cm/deployment/migration-plan--upgrading-from-it-access-to-cm10 -->

# Migration Plan: Upgrading from IT Access to CM10

The document provides an overview plan for all customers who are using **MetaDefender IT Access On-premise version 3.49.x** to upgrade to **My OPSWAT Central Management (Central**** ****Management v10)**.

### **1. Key Principles**

- No **in‑place upgrade** from IT Access OVA to CM10 OVA.
- Recommended path: **Deploy CM10 in parallel → migrate/recreate config → re‑enroll endpoints in waves**.
- CM10 uses **active mode** (agents connect to CM10).

### **2. Phase 1 – Preparation**

- **Deploy CM10 on‑prem** OVA [Virtual Appliance Deployment](https://www.opswat.com/docs/cm/deployment/virtual-appliance-deployment) and verify the following:
  - FQDN/DNS, TLS cert, access to UI
- **Network/ports (minimum)**:
  - Endpoint → CM10: HTTPS 443 (or 9000).
- **Licensing:**
  - Activate Endpoint licenses on CM10.

### **3. Phase 2 – Configuration & UAT**

- **Determine the necessary data for migration and review the required features.** **Capture screenshots of existing configurations in IT Access for reference.**
  - Using HTTPS
  - Using SMTP
  - Take screenshots of groups, policy, and settings
  - Auto-reconnect MetaDefender Endpoints
  - Able to re-deploy all MetaDefender Endpoints
  - Keep all groups & Configuration
  - Keep all Policy & Configuration
- **Recreate configuration in CM10**:
  - Re-configure necessary data: account settings, service configurations, policies, groups.
  - Re‑enroll a small set of agents to CM10.
  - Reference for server configuration changes: [https://www.opswat.com/docs/mdendpoint/user-guide/migrating-metadefender-endpoint-to-another-account#configure-the-server-settings](https://www.opswat.com/docs/mdendpoint/user-guide/migrating-metadefender-endpoint-to-another-account#configure-the-server-settings)
  - Verify that
    - Devices appear in CM10
    - Policies are applied correctly
    - Events/logs are accurate
- **Define Go/No‑Go**:
  - Agree on simple criteria to move from UAT to production.

### **4. Phase 3 – Cutover (Waves)**

- **Agent re‑enrollment strategy**:
  - Change server settings on endpoints to point to CM10 (URL + Registration Code), or Use custom scripts to silently re‑enroll at scale.
  - Reference for server config change: [https://www.opswat.com/docs/mdendpoint/user-guide/migrating-metadefender-endpoint-to-another-account#configure-the-server-settings](https://www.opswat.com/docs/mdendpoint/user-guide/migrating-metadefender-endpoint-to-another-account#configure-the-server-settings)
- **Parallel run & decommission**:
  - Keep legacy IT Access as a backup during migration.
  - Decommission IT Access after most endpoints are stable on CM10
