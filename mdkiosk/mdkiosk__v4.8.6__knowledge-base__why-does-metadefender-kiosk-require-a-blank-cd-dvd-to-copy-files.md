<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files -->

# Why does Metadefender Kiosk require a Blank CD/DVD to copy files to?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk v4 releases deployed on Windows systems.

## [**Summary**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files#summary)

When using Metadefender Kiosk to export files to a CD/DVD, whether through **File Handling → Copy to Secondary Location** or by **retrieving files from an MFT server,** the Kiosk may prompt the user to *“insert an empty media”* and will not accept a partially written one.
This behavior is expected. Metadefender Kiosk **always closes (finalizes) the disc session** after writing files, preventing further data from being added later.

---

## [**Root Cause**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files#root-cause)

Metadefender Kiosk is designed as a **security-focused, controlled file transfer appliance**.
To maintain the integrity and auditability of exported media, the Kiosk Finalizes (closes) the CD/DVD session immediately after writing.

Once a disc is finalized:

- No additional files can be written
- The disc is effectively **read-only**
- A new write attempt will require a **new blank CD/DVD**

This ensures that exported media cannot be modified after scanning or transferred outside the validated workflow.

---

## [**Why Windows Allows Multisession but the Kiosk Does Not**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files#why-windows-allows-multisession-but-the-kiosk-does-not)

Windows 10/11 supports multisession writing using “**Live File System**” mode, which leaves the disc unfinalized so users can add files later.

Metadefender Kiosk **intentionally does not support multisession discs**, due to security risks such as:

- Adding unscanned files after export
- Bypassing workflow controls
- Compromising audit logs
- Creating unverifiable media used for cross-domain transfer

Multisession support would undermine the trust and traceability required in secure environments.

---

## [**Resolution / Workaround**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files#resolution--workaround)

There is **no workaround** that enables writing multiple times to the same CD/DVD using Metadefender Kiosk.

To export additional data:

- Use a **new blank CD/DVD**, or
- Export to a different secondary location (e.g., USB drive, network share) that allows multiple write sessions.

---

## [**Additional Notes**](/docs/mdkiosk/v4.8.6/knowledge-base/why-does-metadefender-kiosk-require-a-blank-cd-dvd-to-copy-files#additional-notes)

- Finalizing the disc protects the integrity of exported media according to security and compliance requirements.
- Previously written discs can still be read by Windows, but are not writable by the Kiosk.
- Attempting to use a partially used “open session” disc created by Windows will also be rejected.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
