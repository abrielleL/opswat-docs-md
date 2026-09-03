<!-- source: https://www.opswat.com/docs/mdss/4.4.2/installation/uninstall -->

# Uninstall

> If the current MetaDefender Storage Security (MDSS) deployment (4.0.0 or later) was upgraded from 3.6.1 or earlier, any existing MongoDB backups will be deleted during uninstallation. Manually back up the data beforehand if it’s still needed.

## [Uninstall via Command Line](/docs/mdss/4.4.2/installation/uninstall#uninstall-via-command-line)

## [**Debian / Ubuntu (.deb package)**](/docs/mdss/4.4.2/installation/uninstall#debian--ubuntu-deb-package)

To remove all files installed by MetaDefender Storage Security:

BashCopysudo mdss -u clean

To remove the `mdss` package from the system:

BashCopysudo apt-get remove mdss
## [**Red Hat Enterprise Linux / CentOS (.rpm package)**](/docs/mdss/4.4.2/installation/uninstall#red-hat-enterprise-linux--centos-rpm-package)

To remove all files installed by MetaDefender Storage Security

BashCopysudo mdss -u clean

To remove the `mdss` package from the system:

BashCopysudo yum remove mdss
## [Uninstall via Uninstall Wizard (Windows only)](/docs/mdss/4.4.2/installation/uninstall#uninstall-via-uninstall-wizard-windows-only)

NOTE
> The Uninstall Wizard is available only for the Windows installer (`.msi`).

## [Step-by-Step Instructions](/docs/mdss/4.4.2/installation/uninstall#step-by-step-instructions)

1. Open **Start** → **Control Panel** → **Uninstall a program**
2. Locate **MetaDefender Storage Security** in the list
3. Double-click the entry
4. Click **Uninstall and Yes** to begin the process

5. Wait for the uninstallation to complete
6. Click **Finish** to finish.
