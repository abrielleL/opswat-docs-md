<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/knowledge-base/metadefender-downloader-uninstallation-guide-for-windows-and-lin -->

# MetaDefender Downloader Uninstallation Guide for Windows and Linux

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to All version of Metadefender Downloader Windows and Linux version

**Issue:**

This article provides the commands and directory locations required to fully uninstall MetaDefender Downloader from Windows and Linux environments, including the removal of application files, configuration files, services, and residual data.

**Solution:**

To completely uninstall MetaDefender Downloader and ensure a clean removal of all application components by follow the instructions below:

**Uninstall on a Window’s Deployment:**

1. Go to **Add or Remove Program** under the search menu

Find the **MetaDefender Update Downloader** and Press the Uninstall button to uninstall application.

2. Click the Uninstall button to uninstall the MetaDefender Downloader application.
3. To completely remove all MetaDefender Downloader related data, logs and configuration files, please deleted all the directories reference in this article: [What are the installation directories for MetaDefender Update Downloader?](https://opswat.atlassian.net/wiki/spaces/~71202072e168519b204f5db27c73bcb68cc135/pages/5016814171)

**Uninstall Linux Environment:**

The command line to uninstall the downloader is as follows:

1. Stop and Disabled MetaDefender Downloader Core services.

sudo systemctl stop ometadownloader
sudo systemctl disable ometadownloader

2. For Debian-based Systems (Ubuntu, Debian):

sudo apt-get remove --purge ometadownloader

For RPM-Based Systems (Rocky Linux, CentOS, RHEL):

sudo dnf remove ometadownloader

3. To completely remove all MetaDefender Downloader related data, logs and configuration files, please deleted all the directories reference in this article: [What are the installation directories for MetaDefender Update Downloader?](https://opswat.atlassian.net/wiki/spaces/~71202072e168519b204f5db27c73bcb68cc135/pages/5016814171)

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
