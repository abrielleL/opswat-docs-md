<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-manage-false-positives-in-metadefender-core- -->

# How to manage false positives in MetaDefender Core?

This article applies to all MetaDefender Core version 5.0 and newer releases deployed on Windows and Linux systems.

#### [How to Manage False Positives in MetaDefender Core](/docs/mdcore/v5.22.0/knowledge-base/how-to-manage-false-positives-in-metadefender-core-#how-to-manage-false-positives-in-metadefender-core)

False positives—clean files incorrectly flagged as threats—can disrupt operational workflows and cause unnecessary concern. MetaDefender Core offers several methods to handle false positives, depending on the scenario and your internal security policies. Use the options below in the recommended order:

**1. Verify That the File Is a False Positive, Not an Actual Threat**

Before taking any further action, it is essential to confirm that the file is indeed a false positive.

- Review the detection details provided by each engine.
- Test the file in a controlled environment to validate its behavior.
- If you suspect a false positive, you can submit the file to OPSWAT for further analysis:

  - Log into My OPSWAT.
  - In the left-hand side menu, select “Support,” and then choose “Report False Detection” from the submenu.
  - Provide the file you would like OSPWAT's malware analyst team to investigate. Note that the maximum size for file uploads is restricted to 2GB.
  - In the Submission Type section, specify if you suspect the file is a false positive (i.e., a clean file incorrectly flagged) or a false negative (i.e., a malicious file not detected).  Note: You should not be overly concerned about categorizing your submission as a false positive or false negative. OPSWAT utilizes a thorough validation process for analyzing submitted files.

See official guidance: [How do I get a False Detection (False Positive or False Negative) corrected?](/docs/mdcore/v5.22.0/knowledge-base/how-do-i-get-a-false-detection--false-positive-or-false-negative)

- Once the file has been confirmed as a false positive, the Reputation engine will be updated and will override the AV engines detection with a Known good verdict.

- Also, the AV vendors will be notified of the false positives and in time these will no longer be flagged.

**2. Use the Sandbox Engine for Behavioral Analysis**

To gain deeper insight into the file’s behavior, enable scanning with the **Sandbox** engine.

- The sandbox analyzes files in a controlled virtual environment to detect malicious behavior beyond traditional AV signatures.
- This additional layer helps validate whether a detection is accurate or a false positive.

Using sandbox analysis is especially helpful for suspicious scripts, executables, or documents where static detection yields inconclusive results.

**3. Use the Allow List for Known Trusted Files (With Caution)**

If you are certain the file is safe (e.g., it is a known internal script or tool), you can add its hash to the **Allow List** to prevent future detections:

- Go to **Workflow Management -> Workflows -> your workflow -> Allowlist -> Allowlist by HASH**
- Add the file’s SHA256 hash
- Save the configuration

⚠️ **Warning**: Adding a file to the Allow List means it will bypass all scanning. This creates a potential security risk. Always ensure that internal security policies are followed, and use this option **only when absolutely necessary**.

**4. Adjust Engine Scoring Thresholds in Metascan Workflow (Advanced Use)**

MetaDefender Core allows you to configure thresholds for how many engines must flag a file before it is classified as **infected** or **suspicious**.

- Go to **Workflow Management -> Workflows -> your workflow -> Metascan**
- Adjust the values for AV engines thresholds:

  - **Number of engines to classify as Infected**
  - **Number of engines to classify as Suspicious**
- **Save the configuration**

⚠️ **Warning**: Lowering these thresholds increases the risk of allowing actual threats into the environment. Use this option only when:

- You are using a **large number of engines** (e.g., 16, 20, or MAX packages)
- You have **sufficient compensating controls** in place
- You are following **internal security guidelines**

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
