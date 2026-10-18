<!-- source: https://www.opswat.com/docs/supply-chain/configuration/workflow-creation -->

# Workflows

MetaDefender Software Supply Chain includes a built-in **Default Workflow**, so creating your own workflow is not mandatory for basic scanning — scans can run against the Default Workflow. Creating a custom workflow is only necessary when you want to configure **remediations** (or other custom scan behavior such as specific rules, scan pools, or blocked-file handling). A custom workflow is also required for **real-time (webhook) scans**, which cannot use the Default Workflow.

Multiple workflows can be created. To create any workflow, a **scan pool** must first be registered.

Workflows are no longer created "by type." A single workflow applies to all of your connections, and its configuration is organized into three connection categories, each with its own remediation settings:

- **Source Code** — currently available services: GitHub, GitLab, Bitbucket, SVN, Azure DevOps, and Gitea.
- **Container** — currently available services: DockerHub, Amazon ECR, Azure ACR, JFrog Container, Quay, Harbor, and Nexus Container.
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

## Step 2: Configure the workflow (the workflow diagram)

After creation (or when editing an existing workflow), the workflow opens in the **Workflow Details** view as a left-to-right pipeline diagram:

**Start → Hash Scanning → Scan Configuration → Technologies → Blocked File Definition → (decision) → Source Code / Container / Binary branches (each split into Allowed / Blocked) → Promote to Secure Zone → Other Remediations → End**

Each node is clickable and opens a configuration panel on the right. Nodes display their status (e.g. **Active** / **Inactive**), and the remediation nodes show chips (**Keep**, **Copy**, **Delete**) reflecting the configured action. Every panel has **Save Changes** and **Cancel**; saving shows "Workflow updated successfully."

![](https://uploads.developerhub.io/prod/jdK6/43wl2n79tw1gas0dl5pxfocjr10rwfvrxkf8cqe6jvdtf42awaclzrlrqcrm6dgv.png)

### Scan Configuration

Choose the **Scan Pool** and the **Rule(s)** used to trigger scans (same behavior as the Create panel — multi-select rules and custom-rule creation for Cloud pools, single rule otherwise).

![](https://uploads.developerhub.io/prod/jdK6/rr3etrj8j9ijo0kdh8d1d1p2g9t1kp7gkaqs25qze98l6zjhq70bw12486bedajw.png)

### **Hash Scanning**

Detects whether files changed since the last scan so unchanged files can be skipped for faster scans. Toggle on/off; when enabled, set **Days Before Rescan** (whole number ≥ 1).

![](https://uploads.developerhub.io/prod/jdK6/xv8uc8jh2fdmxde4kxcapnozfklqnzx49car50wptfxqarsgmkyl68t70mdd5fhz.png)

### **Technologies**

A **read-only** status view showing which MetaDefender Core modules are active for the selected rule: **SBOM**, **MetaScan™** (multiscanning), and **Secrets Prevention (DLP)** — each shown as Active / Disabled / Unknown.

![](https://uploads.developerhub.io/prod/jdK6/nqupuw9d4ed6n9eqthtlu7pj8v9n33va2w8tb03cekgv27l2tvrd80sqig6bf1d4.png)

### **Blocked File Definition**

Controls which files are treated as blocked:

- **Strict mode** — any file blocked by MetaDefender Core (malware, encryption, blocklist) stays blocked.
- **Configurable mode** — override Core verdicts by category via checkboxes (sensitive data, vulnerabilities). When vulnerabilities are enabled, select the **severities** to block: Critical / High / Medium / Low. Files with malicious content are always blocked. This checkbox is always selected and you cannot clear it.

![](https://uploads.developerhub.io/prod/jdK6/fnrsm65k85xv7rr8enj4azzkv766h6w2hy8x6oithma7wfkpd98tvaaohj9sceci.png)

### **Remediation branches: Source Code / Container / Binary**

After the decision point, the pipeline forks into **Source Code**, **Container**, and **Binary**, and each branch splits into an **Allowed Files** and a **Blocked Files** node. "Allowed" vs "Blocked" reflects MetaDefender Core's verdict, so you can set different actions for each.

#### **Source Code (Allowed / Blocked)** — choose:

- **Keep** — leaves the file unchanged and lets it continue through the workflow.
- **Soft-Delete** — marks artifacts as deleted without permanently removing them (recovery possible). For GitHub, GitLab, Azure DevOps and Gitea connections, soft deletion commits a change that removes the file. For Bitbucket connections, a commit replaces the file content with empty content.
- **Copy** — copies the scanned repository to the selected destination repositories, either directly or through a pull request. Select Create Pull Request (default) or Push Directly. Copy remediation only applies to GitHub connections.

![](https://uploads.developerhub.io/prod/jdK6/oeoelda1xjfmfjf6qcc1t2ouxi2h31qv4m2xbovjpgaqm6nx5fs5ejyfzx41skzo.png)

#### **Container (Allowed / Blocked)** — choose:

- **Keep**, or
- **Copy** — copies the images from the selected source service connection to the selected destination service connection, which can also be the same one. Copy remediation only applies to JFrog Container and Harbor connections and is ignored for other container connection types.

![](https://uploads.developerhub.io/prod/jdK6/c40ymy53gbqel50dzrstcdfu77frjiig9qubp8wej8rskgv4ba6yz4oioofwovt5.png)

#### **Binary (Allowed / Blocked)** — choose:

- **Keep**, or
- **Copy** — copies the packages from the selected source service connection to the selected destination service connection, which can also be the same one.
- The **Blocked** binary node additionally has a **Malicious Package Deletion** switch: when enabled, packages containing threats, secrets, and/or vulnerabilities are deleted after the scan.

![**Copy Task**: configure one or more copy tasks, each with **From Service Connection, To Service Connection, From Local or Remote,** and **To Local**. Use **Add Copy Task** for more; the repository dropdowns are enabled only after their service connection is selected. The source and destination can be different connections, for example JFrog Container to Harbor.](https://uploads.developerhub.io/prod/jdK6/8gi4y7kab788m8891bw1oc3gbn1314vit355sav2tre3owhsfewb212s0q3rox6o.png)

### **Promote to Secure Zone**

A single switch enabling controlled cross-domain transfer of approved artifacts from a lower trust boundary to a designated secure (high-side) environment. When the switch is on, the panel shows the workflow's Blocked File Definition, which also blocks transfers. Click Edit Blocked File Definition to change it.

![](https://uploads.developerhub.io/prod/jdK6/6m6ibgcx9tgeybrjpe2xzc40vtz4sua20bt3rrleyhuw2xtgdxxhxv6erufpugoa.png)

### **Other Remediations**

Post-scan notification/ticketing actions, each an independently toggleable section:

- **Email Notification** — enter recipient email addresses (added as chips). *Disabled until SMTP is configured: "Configure and enable SMTP in Settings before enabling this remediation."*
- **Jira Ticket** — select a **Jira Connection**, then a **Jira Project**. *Disabled when no Jira connection exists: "Add a Jira connection in Settings before enabling this remediation."*
- **Microsoft Teams Notification** — select a **Microsoft Teams Connection**. *Disabled when no Teams connection exists: "Add a Microsoft Teams connection in Settings before enabling this remediation."*

![](https://uploads.developerhub.io/prod/jdK6/41k2npc2iki0y5jhouuf4jq3f62493cs0cxw6y5w8gpv0dw3y4philbs6wr2tcne.png)

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
