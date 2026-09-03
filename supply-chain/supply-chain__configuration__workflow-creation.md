<!-- source: https://www.opswat.com/docs/supply-chain/configuration/workflow-creation -->

# Workflows

MetaDefender Software Supply Chain includes a built-in **Default Workflow**, so creating your own workflow is not mandatory for basic scanning — scans can run against the Default Workflow. Creating a custom workflow is only necessary when you want to configure **remediations** (or other custom scan behavior such as specific rules, scan pools, or blocked-file handling). A custom workflow is also required for **real-time (webhook) scans**, which cannot use the Default Workflow.

Multiple workflows can be created. To create any workflow, a **scan pool** must first be registered.

Workflows are no longer created "by type." A single workflow applies to all of your connections, and its configuration is organized into three connection categories, each with its own remediation settings:

- **Source Code** — currently available services: GitHub, GitLab, Bitbucket, SVN, Azure DevOps, and Gitea.
- **Container** — currently available services: DockerHub, Amazon ECR, Azure ACR, JFrog Container, Quay, and Harbor.
- **Binary** — currently available services: JFrog Binary and Nexus Binary.

A workflow can be created by navigating to the "**Workflow**" menu where the following screen will be shown:

![](https://uploads.developerhub.io/prod/jdK6/wkjtrf42qzafejt22qm3jnxa3ad9ntco9wb4lwwzgj0ss5bfdedfyndk1t85e6qn.png)

On this screen, the user can inspect a list of the already existing workflows. The list also always includes the built-in **Default Workflow** at the top, which cannot be edited or deleted. The following properties are shown for each workflow:

- **Name** — the workflow's name.
- **Hash Scanning** — whether hash-based file discovery filtering is enabled for the workflow.
- **Scan Pool** — the scan pool (scan configuration) associated with the workflow.
- **Security** — the security options enabled for the workflow.
- **Source Code Allowed / Source Code Blocked** — the source code policy rules configured to allow or block.
- **Containers Allowed / Containers Blocked** — the container policy rules configured to allow or block.
- **Binary Allowed / Binary Blocked** — the binary policy rules configured to allow or block.
- **Other Remediations** — additional remediation actions configured for the workflow; these are specific actions that can be executed after a scan is completed.

The list can be filtered using the search box, and it supports pagination for large numbers of workflows.

A workflow can be created by clicking on the **"Create Workflow"** button. This opens the **Create Workflow** panel, where the workflow name, scan pool, and rules are configured.

An existing workflow can be edited by **clicking on the workflow row** in the list. This opens the workflow in edit mode, with the existing fields prepopulated with the current workflow configuration. Changes can be discarded at any time to revert undesired edits.

To rename a workflow directly from the list, click the **edit (pencil) icon** at the end of the listed workflow, which opens the Rename panel.

Workflows can be deleted by clicking the **delete icon** at the end of the listed workflow. The Default Workflow and any workflow that is currently being created or updated do not show edit, rename, or delete controls.

When choosing to delete a workflow, the user is presented with the following confirmation dialog:

> **Warning**
>
> Deleting workflows that are currently running scans will result in incorrect system behavior !

When choosing to delete a workflow the user is presented with following confirmation dialog:

![](https://uploads.developerhub.io/prod/jdK6/tvahckq30tzrl3nw0n4mw52g3yz8o9u49nz7og41u8lgdrq52ps9nim7ojvy7z43.png)

Clicking the "**Delete**" button here will result in the deletion of the workflow, causing the system to not be able to access its scan configuration details that need to be displayed in certain scan reports, resulting in incomplete information displayed in those reports!

## Step 1: Creating a workflow

A workflow is created by clicking the **"Create Workflow"** button on the Workflows screen. This opens the **Create Workflow** panel, which contains three fields:

- **Workflow Name** — a short, descriptive name (3–50 characters). Mandatory.
- **Scan Pool** — select the scan pool (a group of MetaDefender Core or Cloud instances) that will run the scans for this workflow.
- **Rule** — select the scanning rule to apply. If the selected scan pool is a **Cloud** pool, this field lets you select multiple rules and create custom rules on the fly; for other pools you select a single rule.

> If no scan pool has been registered yet, you must first configure a valid, accessible Scan Pool before a workflow can be created, since the Scan Pool field is required.

Click **Create** to save. The new workflow is created and you are taken directly to its **workflow configuration diagram**, where the rest of the setup is done.

>

![](https://uploads.developerhub.io/prod/jdK6/qnov8foihsb68zzdy13flwh7uuz99q76p1jwn2qvgagfxkp75pzliok9a7wrjise.png)

After choosing the type of the workflow the "Continue" button will be enabled, clicking it, will display the Step 2 screen.

## Step 2: Configure the workflow (the workflow diagram)

After creation (or when editing an existing workflow), the workflow opens in the **Workflow Details** view as a left-to-right pipeline diagram:

**Start → Hash Scanning → Scan Configuration → Technologies → Blocked File Definition → (decision) → Source Code / Container / Binary branches (each split into Allowed / Blocked) → Promote to Secure Zone → Other Remediations → End**

Each node is clickable and opens a configuration panel on the right. Nodes display their status (e.g. **Active** / **Inactive**), and the remediation nodes show chips (**Keep**, **Copy**, **Delete**) reflecting the configured action. Every panel has **Save Changes** and **Cancel**; saving shows "Workflow updated successfully.

![](https://uploads.developerhub.io/prod/jdK6/hj1ydtqta9teo6f7x195nl206w2tzekdz55lrh4hm0d9jg235j6drpi1ux7gzbuo.png)

### Scan Configuration

Choose the **Scan Pool** and the **Rule(s)** used to trigger scans (same behavior as the Create panel — multi-select rules and custom-rule creation for Cloud pools, single rule otherwise).

![](https://uploads.developerhub.io/prod/jdK6/u7438h630df46cxienqaqeoru0o3ypxmxicsrw8he2rt5a0i4hi4libnt65btprd.png)

### **Hash Scanning**

Detects whether files changed since the last scan so unchanged files can be skipped for faster scans. Toggle on/off; when enabled, set **Days Before Rescan** (whole number ≥ 1).
*Applies to Source Code and Container scans only; for other connection types all files are scanned.*

![](https://uploads.developerhub.io/prod/jdK6/23sxdacz6oc9nywwwp4vhobyvmm8g6ezwjfbiamahkf35josiz1mt7mua0l09qtu.png)

### **Technologies**

A **read-only** status view showing which MetaDefender Core modules are active for the selected rule: **SBOM**, **MetaScan™** (multiscanning), and **Secrets Prevention (DLP)** — each shown as Active / Disabled / Unknown.

![](https://uploads.developerhub.io/prod/jdK6/7vxkspofadqdqt9akpr27cvfxlv3b6ujuhmsmx005znw54w3tlbupld5ci3ld140.png)

### **Blocked File Definition**

Controls which files are treated as blocked:

- **Strict mode** — any file blocked by MetaDefender Core (malware, encryption, blocklist) stays blocked.
- **Configurable mode** — override Core verdicts by category via checkboxes (malicious content, sensitive data, vulnerabilities). When vulnerabilities are enabled, select the **severities** to block: Critical / High / Medium / Low.

![](https://uploads.developerhub.io/prod/jdK6/dyoq5xtxno9iexeysyrtk3nbgf1eke2nbmnf0dnffvc5nvmtue2fz0b45imxikt3.png)

### **Remediation branches: Source Code / Container / Binary**

After the decision point, the pipeline forks into **Source Code**, **Container**, and **Binary**, and each branch splits into an **Allowed Files** and a **Blocked Files** node. "Allowed" vs "Blocked" reflects MetaDefender Core's verdict, so you can set different actions for each.

#### **Source Code (Allowed / Blocked)** — choose:

- **Keep** — leaves the file unchanged and lets it continue through the workflow.
- **Soft-Delete** — marks artifacts as deleted without permanently removing them (recovery possible). *For GitHub connections, soft deletion commits a change that removes the file.*

![](https://uploads.developerhub.io/prod/jdK6/bwnmuym5m1y6hafam2aby99blcpqhh31vfoq9z67nvrxg4wgeww7cemer5bjcj66.png)

#### **Container (Allowed / Blocked)** — choose:

- **Keep**, or
- **Copy** — images are transferred within the same service connection; by default only risk-free images are transferred (enable *Allow Risky Images* to include others). *Copy remediation only applies to JFrog Container connections and is ignored for other container connection types.***Container (Allowed / Blocked)** — choose:
  - **Keep**, or
  - **Copy** — images are transferred within the same service connection; by default only risk-free images are transferred (enable *Allow Risky Images* to include others). *Copy remediation only applies to JFrog Container connections and is ignored for other container connection types.*

![](https://uploads.developerhub.io/prod/jdK6/pw2qvuojp6oekx57hs5dpl7v7qtfqa79o3uanpzqj4glbccmw22q0jlusfbgx1jf.png)

#### **Binary (Allowed / Blocked)** — choose:

- **Keep**, or
- **Copy** — packages are transferred within the same service connection; by default only risk-free packages (enable *Allow Risky Packages* to include others).
- The **Blocked** binary node additionally has a **Malicious Package Deletion** switch: when enabled, packages containing threats, secrets, and/or vulnerabilities are deleted after the scan.

![**Copy Tasks** (Container/Binary, when Copy is selected): configure one or more copy tasks, each with **From Service Connection**, **To Service Connection**, **From Local or Remote**, and **To Local**. Use **Add Copy Task** for more; the repository dropdowns are enabled only after their service connection is selected.](https://uploads.developerhub.io/prod/jdK6/h14gcpnqj7697v823glq9z4c16rb96ntnrjwpbjme163fv04icae7f8zg0pj3dqh.png)

### **Promote to Secure Zone**

A single switch enabling controlled cross-domain transfer of approved artifacts from a lower trust boundary to a designated secure (high-side) environment.

![](https://uploads.developerhub.io/prod/jdK6/q3ljbapnds4ko0eisxzlc8xc7r2dvzkyxjdpt5zmlhl9t6qmeszx0f13e4r9hcoa.png)

### **Other Remediations**

Post-scan notification/ticketing actions, each an independently toggleable section:

- **Email Notification** — enter recipient email addresses (added as chips). *Disabled until SMTP is configured: "Configure and enable SMTP in Settings before enabling this remediation."*
- **Jira Ticket** — select a **Jira Connection**, then a **Jira Project**. *Disabled when no Jira connection exists: "Add a Jira connection in Settings before enabling this remediation."*
- **Microsoft Teams Notification** — select a **Microsoft Teams Connection**. *Disabled when no Teams connection exists: "Add a Microsoft Teams connection in Settings before enabling this remediation."*

![](https://uploads.developerhub.io/prod/jdK6/aai6rhjtuj10pv08k5pwrfxgxejbnay94ltvzvqc43whwboqvh3ny8e30st56zq6.png)

####
