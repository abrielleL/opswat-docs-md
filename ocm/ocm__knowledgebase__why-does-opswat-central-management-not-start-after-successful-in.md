<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/why-does-opswat-central-management-not-start-after-successful-in -->

# Why Does OPSWAT Central Management Not Start After Successful Installation?

Central Management version 7.3x

This article applies to all OPSWAT Central Management 7.3x + releases deployed on Windows systems.

After installing Central Management , the installation completes successfully but the application does not become accessible.

This issue can occur when the PowerShell Execution Policy is restricted by machine or group policy settings.

Root Cause

The PowerShell Execution Policy on the system is set to AllSigned at the Machine Policy level.

Central Management requires the execution policy to be set to RemoteSigned, which is also the default policy on a standard Windows Server installation.

When the policy is restricted to AllSigned, required scripts may fail to execute, preventing the application from starting properly even though the service is running.

Verification

1. Open Windows PowerShell or Windows Terminal
2. Run as Administrator
3. Execute the following command:

Get-ExecutionPolicy -List

4. Review the output

- If MachinePolicy is set to AllSigned, this is likely the cause of the issue

Resolution

Change the PowerShell Execution Policy to RemoteSigned.

Option 1: Change Execution Policy via PowerShell

1. Open Windows Terminal or PowerShell as Administrator
2. Run the following commands:

Get-ExecutionPolicy -List

cd "C:\Program Files\OPSWAT\Central"

Set-ExecutionPolicy RemoteSigned

Confirm the policy change when prompted

3. Reinstall the Central Management product

Option 2: Configure via Group Policy Editor (If PowerShell Change Does Not Apply)

If the execution policy is enforced by Group Policy, update it using the Local Group Policy Editor.

1. Press Win + R and type:

gpedit.msc

2. Navigate to:

Computer Configuration

> Administrative Templates

> Windows Components

> Windows PowerShell

3. Locate and open Turn on Script Execution
4. Set the policy to Enabled
5. Select Allow local scripts and remote signed scripts
6. Click Apply and OK
7. Run the following command to refresh policies:

gpupdate /force

4. Reinstall the Central Management product

Support: 

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
