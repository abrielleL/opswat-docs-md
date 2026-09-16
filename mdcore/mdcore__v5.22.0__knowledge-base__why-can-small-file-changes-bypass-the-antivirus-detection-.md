<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-can-small-file-changes-bypass-the-antivirus-detection- -->

# Why can small file changes bypass the Antivirus detection?

When you open a file in a text editor and **add even a single character**, you **modify the file's binary content**. This changes the **file's checksum (hash)** — a fingerprint used by antivirus software to recognize known malware. Many traditional antivirus engines rely heavily on **static signatures**, which are based on specific patterns or hashes.

**So, when you add, for example, a space:**

- The file's checksum (e.g., its MD5 or SHA256 hash) changes.
- Signature-based AV engines no longer recognize it as matching a known malicious file.
- Unless the antivirus is doing **behavioral analysis**, **deep scanning**, or **structure-aware parsing** (looking inside the file in a smarter way), it won't flag it anymore.

**In short:**

The AV was looking for an *exact match* of the malicious file, and your tiny edit broke that match.

---

**Important**:

- Modern, better AVs and EDR (Endpoint Detection and Response) systems often go beyond simple signature matching — they can **analyze the file's structure, detect exploits**, or **simulate its behavior**.
- But many basic AV engines are still very "hash-dependent."

**Heuristic detection** is *specifically* designed to catch exactly these kinds of tricks, where a simple file change (like adding a space) would fool basic signature-based detection.

Here’s how it helps:

- **Heuristics** don't rely only on exact file hashes or fixed byte patterns.
- Instead, they **analyze the structure, behavior, and content patterns** of the file to see if it "acts suspiciously," even if it’s slightly modified.
- For example, in a PDF, heuristics might look for:

  - Hidden JavaScript code
  - Unusual embedded objects (like an executable inside the PDF)
  - Exploit patterns targeting vulnerabilities (like old Adobe Reader flaws)
  - Abnormal structures (e.g., heavily obfuscated streams)

So **even if you change the file slightly** (adding a space, changing a few bytes), **a good heuristic engine** would still flag it if the **malicious core behavior or structure** is present.

---

**Example:**

- Signature detection: "This exact MD5 hash = known bad."
- Heuristic detection: "This PDF has JavaScript that automatically runs shellcode — suspicious, even if it’s new or slightly altered."

---

**However**, heuristics aren't perfect:

- They can sometimes **miss** very well-obfuscated threats.
- They also sometimes generate **false positives** (marking legit files as suspicious).

---

For a comprehensive list of engines that support heuristic capabilities, please refer to: [Anti-malware capabilities](/docs/mdcore/v5.22.0/metascan-engines/anti-malware-vendors)

Info:

Note that AI/heuristic capabilities may be disabled by default and must be manually enabled via the engine's advanced settings, as outlined at: [Configuring engine advanced settings](/docs/mdcore/v5.22.0/operating/library-management#configuring-engine-advanced-settings)

To enhance detection capabilities, we recommend complementing MetaDefender’s Multiscanning technology, which leverages 30+ leading anti-malware engines, with additional layers of protection such as our [Deep Content Disarm and Reconstruction (Deep CDR)](/docs/mdcore/v5.22.0/deep-cdr/supported-file-types) engine and [Sandbox](/docs/mdcore/v5.22.0/sandbox/overview) engine for adaptive threat analysis.

---

Support:

If **Further Assistance** is required regarding this topic, please proceed to log a [**support case or chat with a support engineer**](https://my.opswat.com/portal/support).
