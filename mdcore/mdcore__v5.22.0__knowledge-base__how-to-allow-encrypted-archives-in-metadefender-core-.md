<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core- -->

# How to Allow Encrypted Archives in MetaDefender Core?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

### [**Summary**](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core-#summary)

By default, MetaDefender Core (MD Core) blocks encrypted archive files since their contents cannot be scanned. If it is necessary to allow encrypted archives to pass through (for example, when integrating with MetaDefender Email Gateway Security (EGS)), the workflow can be configured to classify these files as **“Allowed.”**

This article explains how to configure the workflow so that encrypted archives are not blocked and can be forwarded even when their contents cannot be scanned.

### [**Symptoms**](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core-#symptoms)

Encrypted archive files sent via email are automatically blocked by MetaDefender Core or MetaDefender Email Gateway Security (EGS).

### [**Cause**](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core-#cause)

Encrypted archives cannot be scanned because their contents are protected by a password. By default, such files are blocked to prevent potential threats from bypassing security checks.

### [**How to Allow Encrypted Archives**](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core-#how-to-allow-encrypted-archives)

Follow the steps below to configure MetaDefender Core to allow encrypted archives:

1. **Access the Configuration Interface** Log in to the MetaDefender Core management console.
2. **Select the Workflow** Choose the workflow used by MetaDefender Email Gateway Security (EGS) or the relevant integration.
3. **Open the Process Settings** Navigate to **General → Process**.
4. **Enable Allowed Processing Results** Enable the option **“Processing results to be classified as Allowed.”**
5. **Select Encrypted Archive** Under this section, select **“Encrypted archive.”**
6. **Save the Configuration** Click **Save** to apply the changes.
7. **Verify the Configuration** Confirm that the new setting is saved successfully.

### [**Expected Result**](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-encrypted-archives-in-metadefender-core-#expected-result)

Encrypted archives that cannot be scanned are classified as **Allowed** and forwarded according to the configured workflow.

Warning

Please note that allowing **Encrypted Archive** files may introduce potential security risks. Attackers often use encrypted archives to bypass content inspection and deliver malicious files.

We strongly recommend that you **carefully evaluate this option** before enabling it, ideally through a **cross-review process** involving multiple teams (e.g., security, compliance, and IT operations).

For example, if a system problem arises, an administrator might quickly allow encrypted archives to restore functionality — which is exactly the scenario attackers aim to exploit to gain access and compromise user machines.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
