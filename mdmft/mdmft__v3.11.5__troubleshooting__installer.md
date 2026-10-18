<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/troubleshooting/installer -->

# Installer

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### [Installation Halts at DB Selection Step](/docs/mdmft/v3.11.5/troubleshooting/installer#installation-halts-at-db-selection-step)

Installation may be hindered at the *DB Selection* step when selecting the "Windows Authentication DB" option, with an error related to an existing helper service.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/installer#resolution)

To overcome this issue, follow these steps:

1. Open "Command Prompt" as an administrator
2. Manually delete the service using the command:

BatchCopysc DELETE "mftHelper"

3. If the deletion fails, restart the machine

These steps will resolve the installation issue and allow you to proceed past the DB selection step.

---

### [RunDLL Failure Due to Potential Unwanted Virus During Installation](/docs/mdmft/v3.11.5/troubleshooting/installer#rundll-failure-due-to-potential-unwanted-virus-during-installation)

A *RunDLL failure* may occur during installation, indicating a potential unwanted virus. This may be due to using an outdated operating system.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/installer#resolution)

To resolve this issue, follow these steps:

1. Upgrade Windows to the latest version
2. Restart your computer

Upgrading Windows and restarting the PC should ensure a smoother installation process.

---

### ["Network Resource is Unavailable" Error During Upgrade or Installation](/docs/mdmft/v3.11.5/troubleshooting/installer#network-resource-is-unavailable-error-during-upgrade-or-installation)

Users may encounter a "Network Resource is Unavailable" error during upgrades or installations.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/installer#resolution)

1. Explore the solutions outlined in ["Fix: The Feature You Are Trying to Use is on a Network Resource That is Unavailable"](https://appuals.com/fix-the-feature-you-are-trying-to-use-in-on-a-network-resource-that-is-unavailable/) .
2. If the issue persists, perform a clean installation of MetaDefender Managed File Transfer™ after cleaning the database using PSTool.
