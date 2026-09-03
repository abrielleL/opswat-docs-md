<!-- source: https://www.opswat.com/docs/cm/deployment/uninstall-my-opswat-central-management -->

# Uninstall My OPSWAT Central Management

## Windows:

On Windows, My OPSWAT Central Management can be removed through the Add or Remove Programs tool or through the command prompt.

### Option 1: Use the Add or Remove Programs tool

1. Go to Control Panel > Programs and Features or Add/Remove Programs depending on your version of Windows.
2. Select My OPSWAT Central Management and click Uninstall to start the uninstallation process.

### Option 2: Use the Command prompt

> **Warning**
>
> While it is possible to uninstall the program from the same .msi package used for installation, please note that the procedure requires an elevated context (i.e. with administrative privilege), such as via an elevated command prompt.

1. Start the command prompt as Administrator.
2. From the command-line interface, execute the command:

```bash
msiexec /x <msi file name>
```

Or for silent uninstallation:

```bash
msiexec /x <msi file name> /quiet
```

Where <msi file name> should be the location of your msi package. For example:

```bash
msiexec /x C:\MyOPSWATCentralManagement.msi/quiet
```

## [Red Hat Enterprise Linux:](https://www.opswat.com/docs/ocm/installation/uninstall-opswat-central-management#red-hat-enterprise-linux)

On Red Hat Enterprise Linux, My OPSWAT Central Management can be removed through the terminal.

1/ Enter the command (requires sudo privilege):

```bash
dnf remove mocm-10.x.x.x-1.x86_64
```

[Replace `10.x.x.x` with your specific version number.)

## Clean Uninstallation

In case of a problem during the installation of a new version of My OPSWAT Central Management, you can perform a clean uninstallation to completely remove all data related to My OPSWAT Central Management and resolve any possible conflicts.

> **Warning**
>
> Please note that clean uninstallation should only be performed at a last resort. The following instructions will result in the loss of all changes to your My OPSWAT Central Management installation (persistent data from the current instance, stored files and custom configuration).

1. Uninstall My OPSWAT Central Management via one of the methods described above.
2. Delete all My OPSWAT Central Management directories. Please refer to [Directory](https://www.opswat.com/docs/cm/deployment/system-requirements#directory).
