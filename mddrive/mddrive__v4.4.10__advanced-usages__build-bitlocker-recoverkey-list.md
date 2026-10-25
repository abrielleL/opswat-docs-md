<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list -->

# Building a Persistent BitLocker Key List on MetaDefender Drive

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#overview)

MetaDefender Drive can automatically unlock BitLocker-encrypted disks if the corresponding recovery keys are pre-loaded into the `tools/bitlocker/` folder on the Drive partition. This article explains how to collect keys and deploy them across one or multiple Drives for scanning multiple machines.

Security Warning:

Anyone with physical access to a Drive containing BitLocker keys can unlock the associated encrypted disks. Store the Drive securely, track which keys are on which Drive, and rotate keys immediately if a Drive is lost or stolen.

## [How It Works](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#how-it-works)

At boot time, MetaDefender Drive reads all key files from `tools/bitlocker/` and attempts to match them against any BitLocker-encrypted disks it finds. If a match is found, the disk is unlocked automatically — no manual input required.

### [Step 1: Collect BitLocker Keys](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#step-1-collect-bitlocker-keys)

Use any of these methods to obtain recovery keys from each target machine. You only need to do this once per machine:

[Unlock BitLocker Manually](/docs/mddrive/v4.4.10/advanced-usages/unlock-bitlocker-manually)

[Unlock BitLocker Automatically Using OPSWAT's Tool](/docs/mddrive/v4.4.10/advanced-usages/unlocking-bitlocker-automatically-using-opswat-tool)

[Unlock BitLocker Automatically Using Windows Recovery Key](/docs/mddrive/v4.4.10/advanced-usages/unlocking-bitlocker-automatically-using-windows-recovery-key)

#### [Step 2: Consolidate Keys on the Drive](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#step-2-consolidate-keys-on-the-drive)

Once you have keys from all target machines, place them all in one folder on the Drive:

PowershellCopyMetaDefender Drive (E:\)
└── tools/
└── bitlocker/
├── BitLocker Recovery Key ABC123.txt (from Machine A)
├── BitLocker Recovery Key DEF456.txt (from Machine B)
├── BitLocker Recovery Key GHI789.txt (from Machine C)
└── ...

That’s it. Boot any of those machines from this Drive and the encrypted disks unlock automatically.

## [Multiple Drives](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#multiple-drives)

If your organization uses multiple MetaDefender Drives, simply copy the same set of key files to each Drive’s `tools/bitlocker/` folder. Each Drive becomes capable of unlocking all the machines whose keys it carries.

## [Removing Keys](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#removing-keys)

To revoke: delete the corresponding `.txt` or `.key` file from `tools/bitlocker/`. Rotate the BitLocker recovery key on the target machine for full security.

## [Security Reminder](/docs/mddrive/v4.4.10/advanced-usages/build-bitlocker-recoverkey-list#security-reminder)

- Treat any Drive carrying keys as a sensitive asset — lock it up when not in use.
- If a Drive is lost: rotate all BitLocker keys that were stored on it immediately.
- Keep an inventory of which keys live on which Drives.
