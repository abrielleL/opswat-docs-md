<!-- source: https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer -->

# Cross Domain Transfer

**Cross Domain Transfer** is a feature that allows users to securely transfer data from a **Low Side** environment to a **High Side** environment using **MetaDefender Software Supply-Chain and optionally,** **Data Diodes**.

![](https://uploads.developerhub.io/prod/jdK6/w27e51g8iha1oqlscqml9eo9ovys0mpz0l7djftzouric44nn7gm3kj1dyu9w85i.png)

This feature is designed for environments where strict separation between networks is required while still allowing controlled data flow into a secure zone.

### **Low Side Configuration**

The **Low Side** environment is where the source code or data resides before being scanned and transferred to the **High Side** (secure zone).

This is typically the development or less restricted environment.

#### **Low Side Setup**

- In your **Low Side MDSSC Instance** -> Open **Settings**.
- Navigate to the **Cross Domain Transfer** tab.
- Select "**Low Side**" to configure this as a Low Side environment.
- Enable transfers using the **toggle switch**.
- Enter the **Data Diode address**.
- [Configuring an API Key](https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key) from the **High Side** UI
- Enter the **API key** from the High Side as the **authorization token**.
- Click on the "**Save**" button.

![](https://uploads.developerhub.io/prod/jdK6/oxw6beolzzrw6uktgwzq7qq0yj4ej5bdvja4iotb4hte4en82hj4686t6q7ofhtm.png)

Once the **Cross Domain Transfer** settings are configured on both sides, cross-domain transfers must also be enabled at the workflow level on the Low Side instance.

This is done through the lowside interface, in the workflow creation or update screen.

**Setup:**

- Navigate to **Workflow** in the left sidebar and open or create a workflow.
- Enable the **Cross-domain transfer after scan** toggle.
- Set the **Max Allowed Severity** — files exceeding this threshold will be blocked from transfer.
- If needed, enable **Block transfer if secrets are found** to prevent transfers when sensitive data is detected.
- Click **Continue** to finalize the workflow.

![](https://uploads.developerhub.io/prod/jdK6/fmuqikrbzcvotuz9z5rxzciiwu92fy7g3epsxzu5cc1uh7y850x93rbqlbnp52an.png)

---

### **High Side Configuration**

The **High Side** environment is the secure destination where **scanned** source code or data is transferred after passing inspection.

This is typically the production or more restricted environment.

#### **High Side Setup**

- In your **High Side MDSSC Instance** -> Open **Settings**.
- Navigate to the **Cross Domain Transfer** tab.
- Select "**High Side**" to configure this as a High Side environment.
- Accept incoming transfers using the **toggle switch**.
- Configure your **Push Behavior** — either via **pull request** or **direct push**.
- Click on the "**Save**" button.

![](https://uploads.developerhub.io/prod/jdK6/59z5djfl2s76ypys3lvl5ldz2kjhbiu1pg0lmeoikg7xs0mjnfedrimrn9lmotle.png)

To push code to the High Side, ensure your API tokens have write permissions. You may need to regenerate them if they were created with read-only access.

1. [Add A GitHub Service](https://www.opswat.com/docs/supply-chain/integrations/add-a-github-service)
2. [Add A GitLab Service](https://www.opswat.com/docs/supply-chain/integrations/add-a-gitlab-service)

![](https://uploads.developerhub.io/prod/jdK6/eovjdxsv97k1fktglbeii9uq7dfwvb5rmbws506fg1k1grxn3gtlatc2mjr37aib.png)

High-side scanning is enabled through the "**Scan Before Import**" feature, which executes scans on the high side with enforcement gates that control and audit cross-domain transfers.
This capability supports organizations with strict data compartmentalization and security requirements:

- Administrators can configure scan policies by setting a maximum allowed severity threshold—vulnerability findings above this level will block the import.
- Additionally, a dedicated option allows organizations to block transfers whenever secrets are detected, adding an extra layer of protection against credential exposure in software supply chain assets.

---

### **Supported Services**

The following cross-domain transfer routes are supported:

#### Source code

| Source | Destination |
| ---- | ---- |
| ![](https://cdn.simpleicons.org/gitlab) GitLab | ![](https://cdn.simpleicons.org/gitlab) GitLab |
| ![](https://cdn.simpleicons.org/gitlab) GitLab | ![](https://cdn.simpleicons.org/github) GitHub |
| ![](https://cdn.simpleicons.org/github) GitHub | ![](https://cdn.simpleicons.org/gitlab) GitLab |
| ![](https://cdn.simpleicons.org/github) GitHub | ![](https://cdn.simpleicons.org/github) GitHub |

#### Containers

| Source | Destination |
| ---- | ---- |
|  Amazon ECR | ![](https://cdn.simpleicons.org/harbor) Harbor |
| ![](https://cdn.simpleicons.org/harbor) Harbor |  Amazon ECR |
| ![](https://cdn.simpleicons.org/sonatype) Nexus Containers | ![](https://cdn.simpleicons.org/sonatype) Nexus Containers |

#### Binaries

| Source | Destination |
| ---- | ---- |
| ![](https://cdn.simpleicons.org/jfrog) JFrog Binary | ![](https://cdn.simpleicons.org/jfrog) JFrog Binary |
| ![](https://cdn.simpleicons.org/jfrog) JFrog Binary | ![](https://cdn.simpleicons.org/sonatype) Nexus Binary |
| ![](https://cdn.simpleicons.org/sonatype) Nexus Binary | ![](https://cdn.simpleicons.org/jfrog) JFrog Binary |
| ![](https://cdn.simpleicons.org/sonatype) Nexus Binary | ![](https://cdn.simpleicons.org/sonatype) Nexus Binary |

### Operating

Once both MDSSC instances are individually set up, you will need to link the connections for which you want cross-domain transfers.

#### **Mapping the Transfer**

1. On the **Low Side**, navigate to **Cross Domain Transfer** and add a new connection.
2. After adding the connection, head to the **High Side** and map it to a local connection via the **Add Mapping** panel. Transfers from the Low Side will be routed to that connection.

![](https://uploads.developerhub.io/prod/jdK6/cwnls891j9p2zd7krfuvroyhy7lfcq72s6f3bdorr5oet1edgqvlsqdl7aturlb3.png)

![](https://uploads.developerhub.io/prod/jdK6/3x9sjoc6ci0lw3dv3n74xeskcl8yjuvaujodmaijnomakotqkioq6ggwoeojfjcu.png)

#### **Triggering & Monitoring**

Once the feature is configured:

1. **Initiate a scan in lowside** with the previously configured workflow.
2. Use the **live logs** on both the Low Side and High Side to monitor the transfer in real time.
3. If the transfer completes successfully, your code will now be available on the High Side.

![](https://uploads.developerhub.io/prod/jdK6/gfoykthc17waglxr04t2zbhb0ql4tjdvtbxwoknhyr5eumylovlf7tbczbz2kwwy.png)

### Recommended Optical Diode Setup

1. Enter on the **NetWall Blue Server**, go to Streams and create a new HTTP one:

![](https://uploads.developerhub.io/prod/jdK6/u9mzd9iiftzzs6fd74kfbdugrblnbnm98by004e3i5ok28yds1uncakljs657gz0.png)

2. Complete with the following settings:

![](https://uploads.developerhub.io/prod/jdK6/rgnvrd56r4uprqn2volx9501cpa8595kavz3fizlk5ihys18ptnk6khirwlc46jk.png)

3. Click on **Submit**

![](https://uploads.developerhub.io/prod/jdK6/n8ft6jwrk1qcqpk8xa26g0dy97k3syxvdabtinc8vx4csn0gnto8gb52jvjacdcf.png)

Afterwards, go to **Redwall Server** and repeat the procedure as following:

1. Add a new HTTP Stream:

![](https://uploads.developerhub.io/prod/jdK6/n699mnthzefj8kxbvbb8ut3y7zk4noj5bd5vzdg9cpgtmwrbfb43b3epqzai7y5p.png)

2. Complete with the following settings:

![](https://uploads.developerhub.io/prod/jdK6/gf392pll805a3znhop0ub7hxx7ed99t89ocfwbqclo1h0cd6zwdm9gco2b8vrkfx.png)

3. Click on submit:

![](https://uploads.developerhub.io/prod/jdK6/smfo88ozgz7ks2yo7buatzpvv0124kwc4e6rm1epz80jyvyx3wvdbyyp6funm08f.png)
