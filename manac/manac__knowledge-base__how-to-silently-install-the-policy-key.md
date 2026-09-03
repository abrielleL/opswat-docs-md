<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-silently-install-the-policy-key -->

# How do I silently install the Policy Key?

This article applies to the current NAC Enforcer and Web UI, as well as all Windows systems running the latest NAC Policy Key.

1. Follow the steps in [This Article](https://docs.opswat.com/manac/knowledge-base/download-policy-key-installer) to download a copy of the **Policy Key ServiceInstaller.exe** for Windows devices.
2. Open an elevated **Command Prompt**, then navigate to the folder where the downloaded *.exe* is located.
3. Run **ServiceInstaller.exe /s** to silently install the Policy Key. In the example screenshot below, **ServiceInstaller.exe** was downloaded to **C:\Users\John Doe\Downloads**.

4. The Policy Key should now be installed, but you can verify this by opening **Windows Service Manager** and checking whether the **SafeConnect Manager** service is running.

Support:

If you have followed the instructions above but have been unable to **Silently Install The NAC Policy Key**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
