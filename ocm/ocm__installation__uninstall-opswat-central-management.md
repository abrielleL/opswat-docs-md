<!-- source: https://www.opswat.com/docs/ocm/installation/uninstall-opswat-central-management -->

# Uninstall OPSWAT Central Management

## [Windows:](/docs/ocm/installation/uninstall-opswat-central-management#windows)

On Windows, OPSWAT Central Management can be removed through the Add or Remove Programs tool or through the command prompt.

## [Option 1: Use Add or Remove Programs tool](/docs/ocm/installation/uninstall-opswat-central-management#option-1-use-add-or-remove-programs-tool)

1. Go to **Control Panel** > **Programs and Features** or **Add/Remove Programs** depending on your version of Windows.
2. Select **OPSWAT Central Management** and click Uninstall to start the uninstallation process.

## [Option 2: Use Command prompt](/docs/ocm/installation/uninstall-opswat-central-management#option-2-use-command-prompt)

Warning

While it is possible to uninstall the program from the same .msi package used for installation, please note that the procedure requires an elevated context (i.e. with administrative privilege), such as via an elevated command prompt.

1. Start command prompt **as Administrator.**
2. From the command-line interface, execute the command:

msiexec /x <msi file name>

Or for silent uninstallation:

msiexec /x <msi file name> /quiet

Where <msi file name> should be the location of your msi package. For example:

msiexec /x C:\OPSWATCentralManagement.msi/quiet
## [Red Hat Enterprise Linux:](/docs/ocm/installation/uninstall-opswat-central-management#red-hat-enterprise-linux)

On Red Hat Enterprise Linux, OPSWAT Central Management can be removed through the terminal.

Enter the command (requires sudo privilege):

sudo yum remove ocm

Ubuntu:

On Ubuntu, OPSWAT Central Management can be removed through the terminal.

Enter the command (requires sudo privilege):

sudo dpkg -e ocm

The Ubuntu package also supports the built-in "purge" command for .deb package. This command will perform a clean uninstallation of OPSWAT Central Management.

sudo dpkg -P ocm
## [Clean Uninstallation:](/docs/ocm/installation/uninstall-opswat-central-management#clean-uninstallation)

In case of a problem during the installation of a new version of OPSWAT Central Management, you can perform a clean uninstallation to completely remove all data related to OPSWAT Central Management and resolve any possible conflicts.

Warning

Please note that clean uninstallation should only be performed at a last resort. The following instructions will result in the loss of all changes to your OPSWAT Central Management installation (persistent data from the current instance, stored files and custom configuration).

1. Uninstall OPSWAT Central Management via one of the methods described above.
2. Delete all OPSWAT Central Management directories. Please refer to [Directory](/docs/ocm/installation/recommended-system-requirements#directory).
