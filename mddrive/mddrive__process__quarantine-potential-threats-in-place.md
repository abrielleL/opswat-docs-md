<!-- source: https://www.opswat.com/docs/mddrive/process/quarantine-potential-threats-in-place -->

# Quarantine Potential Threats In-Place

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**MetaDefender Drive now can quarantine detected files in place during scans**, keeping them on the source volume and reversible when needed.

Each quarantined file is:

- Moved to `\OPSWAT_Quarantine\` on the same source volume as the original file.
- Stored as a **ZipCrypto-encrypted** ZIP.
- Accompanied by a plain-text Quarantine Record that identifies the original file.
- Ready to be restored from the host Windows or from Bare Metal and In-Session [Restore Quarantined Threats](/docs/mddrive/process/restore-quarantined-threats)
- Synced and viewable from Central Management if MetaDefender Drive is enrolled.
- And quarantined files will also be **collected in Forensic Collection**

Please follow these instructions to proceed and make use of **Quarantine and Restore Quarantined Files** features.

- [Quarantine Potential Threats after a Bare Metal Scan](/docs/mddrive/process/quarantine-threats-bare-metal-scan)
- [Quarantine Potential Threats after an In-Session Scan](/docs/mddrive/process/quarantine-threats-in-session-scan)
- [Restore Quarantined Threats](/docs/mddrive/process/restore-quarantined-threats)
