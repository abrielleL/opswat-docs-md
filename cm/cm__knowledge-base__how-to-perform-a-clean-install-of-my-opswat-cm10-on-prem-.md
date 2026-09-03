<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-perform-a-clean-install-of-my-opswat-cm10-on-prem- -->

# How to Perform a Clean Install of My OPSWAT CM10 On-Prem?

#### **Purpose**

This article outlines the steps required to perform a clean installation of My OPSWAT Central Management (CM10) On-Premises on Windows OS.

#### **Procedure**

**Step 1 – Uninstall CM10**

1. Open the Windows Control Panel.
2. Navigate to Programs and Features.
3. Locate OPSWAT CM10 On-Premise in the list.
4. Select it and click Uninstall.

**Step 2 – Remove Residual Folders**

After uninstalling, manually delete the following folders to ensure no leftover files remain:

- C:\Program Files\OPSWAT\MOCM
- C:\ProgramData\OPSWAT\MOCM

**Step 3 – Reinstall CM10**

1. Download the latest CM10 On-Premise installer from the My OPSWAT Portal.
2. Run the installer and follow the on-screen instructions.
3. Complete the installation and verify the CM10 services are running.

> **Support:**
>
> If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
