<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-is-eset-detecting-legitimate-software-as-a-potentially-unsaf -->

# Why is ESET detecting legitimate software as a Potentially Unsafe Application (PUA/PUP)?

This article applies to all MetaDefender Core releases on Windows and Linux with **ESET antivirus licensed**.

**Issue:**

ESET may classify certain legitimate software tools as **Potentially Unsafe Applications (PUA/PUP)**.

These tools—such as remote access utilities, keyloggers, and password crackers—are commonly used for system administration but can be misused for malicious purposes.

To mitigate risk, ESET flags them under the **Win32/PrcView** category and similar classifications.

Note:

This classification does not indicate the software is malicious, only that it has the potential to be misused.

If you're experiencing excessive false positives, you can disable PUA/PUP detection in ESET by following the steps below.

1. Go to **Inventory > Modules > Metascan > ESET**.
2. Disable **"Detect PUP/PUA"**.

**Workarounds:**

Disabling PUA/PUP detection may reduce protection against potentially risky tools. As an alternative, you can **keep detection enabled** and **add detected files to the local whitelist**.

Refer to [How to locally whitelist a file using allowlist](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-local-whitelist-a-file-using-allowlist-) for instructions.

**Related Articles:**

- [How to locally whitelist a file using allowlist](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-local-whitelist-a-file-using-allowlist-)
- [ESET Glossary | ESET Online Help](https://help.eset.com/glossary/en-US/unsafe_application.html) (External link)

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
