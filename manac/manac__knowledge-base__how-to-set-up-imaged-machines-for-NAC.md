<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC -->

# How to set up imaged machines for NAC?

This article applies to the current NAC Enforcer and Web UI, as well as all Windows and MacOS systems running the latest NAC Policy Key.

## [Setting up non Deep Freeze imaged machines for NAC](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#setting-up-non-deep-freeze-imaged-machines-for-nac)

When using NAC with machine images, the **sc.dat** file will need to be deleted from **Program Files (x86)\SafeConnect** (on Windows machines) or **SafeConnect.app/Contents/MacOS** (on macOS machines) to ensure that it is absent when the machine image is created or frozen.

Pro Tip:

The **sc.dat** file is the Policy Key’s unique identifier. If it is the same on more than one active machine, NAC will ignore Policy Key traffic from the duplicate machine/s, forcing a reinstall.

Removing this file, as outlined in the instructions below, will ensure that the NAC Policy Key functions on the original and duplicate machines as expected.

For the full process, follow the OS-relevant steps below.

### [Windows](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#windows)

1. Install the **Policy Key** via the normal process.
2. Once the client has successfully started, stop the SCmanager service as follows:

- Open a **Command Prompt** and run **net stop scmanager**
- Open the **Task manager** and stop the **SafeConnect Manage**r Service.

3. With the service stopped, navigate to the **Program Files (x86)\SafeConnect** directory and remove the **sc.dat** file.
4. Finally, **Shutdown** the machine before pulling the image via your normal process.

### [macOS](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#macos)

1. Install the **Policy Key** via the normal process.
2. Once the Client has successfully started, stop the **scManagerD** and **NAC** processes as follows:

- Open the **Activity Monitor**, select (Cmd-click) and Ctrl-click both **scManagerD** and **NAC**, then click the **Quit Process** option.

3. Open **Finder** and click on **Applications** in the left-hand navigation panel, then Ctrl-click **SafeConnect** and click the **Show Package Contents** option:

- Open the **Contents/MacOS** folder.
- Remove the **sc.dat** file.

4. Finally, **Shutdown** the machine before pulling the image via your normal process.

Pro Tip:

If there is a server on your network that is used to host machine images, it may be necessary to add an exception allowing access to the server IP from your managed NAC machines.

To add an exception for the image server, you must add the IP address to the appropriate ACL of the network device that is used for NAC enforcement. If assistance is required, feel free to contact **OPSWAT Support** as outlined in the support box at the end of this article.

## [Setting up Deep Freeze imaged machines for NAC](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#setting-up-deep-freeze-imaged-machines-for-nac)

For the full process, follow the OS-relevant steps below.

### [Windows](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#windows)

Pro Tip:

On Deep Freeze machines, the NAC Policy Key should be installed in **Thaw Space**.

This allows the Policy Key to function as intended, without reverting to previous versions or prompting reinstallation, after the machine reverts to its image.

Please Note:

If required, it may be possible to automate the following step-by-step operations via, for example, a batch file.

1. Install the Policy Key by opening a **Command Prompt** and running **ServiceInstaller.exe /s**
2. Stop the SafeConnect Client and service by running **net stop scmanager** and then **taskkill /IM SafeConnectClient.exe**
3. Delete the Policy Key’s unique fingerprint file by running **DEL “C:Program Files (X86)\SafeConnect\SC.dat**
4. Create a SafeConnect directory on the non-frozen drive, which is D in this example, by running **MKDIR D:\SafeConnect**
5. Copy the Policy Key files to the directory by running **COPY “C:Program Files (X86)\SafeConnect\ “D:\SafeConnect**
6. Delete the original Policy Key files and then the original directory by running **Del /Q “CProgram Files (X86)\SafeConnect:** and then **RD “C:Program Files (X86)\SafeConnect\”**
7. Create a symbolic link to the new directory by running **MKLINK /D “C:Program Files (X86)\SafeConnect” D:\SafeConnect** but, if this method of linking does not work, you may need to run **Junction** as detailed [Here](https://learn.microsoft.com/en-us/sysinternals/downloads/junction).

### [macOS](/docs/manac/knowledge-base/how-to-set-up-imaged-machines-for-NAC#macos)

1. Install the latest **Policy Key** on the thawed OS.
2. Open a **Terminal**, then run the following commands:

- **sudo killall scClient && sudo launchctl unload /Library/LaunchDaemons/Safe.Connect.plist**
- **sudo mv /Applications/SafeConnect.app /Volumes/THAWSPACE/**
- **sudo In -s /Volumes/THAWSPACE/SafeConnect.app /Applications/SafeConnect.app**

3. Finally, freeze the operating system, then **Reboot**.

Support:

If you have followed the instructions above but have been unable to **Set Up One Or More Imaged Machines For NAC**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
