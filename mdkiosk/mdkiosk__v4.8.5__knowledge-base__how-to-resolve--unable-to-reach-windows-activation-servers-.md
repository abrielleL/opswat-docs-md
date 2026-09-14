<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve--unable-to-reach-windows-activation-servers- -->

# How to resolve "Unable to reach Windows Activation Servers"

This article applies to the OPSWAT Kiosk Image only.

When flashing the Kiosk hardware with a Hardened Image or Secured Image in an offline environment, Windows may display the error **'Unable to reach Windows Activation Servers'** because it cannot connect to Microsoft's activation servers to verify the license on the new hardware.

Below are 2 methods to resolve this issue:

## [**Connect the computer to the Internet:**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve--unable-to-reach-windows-activation-servers-#connect-the-computer-to-the-internet)

You can connect the Kiosk to the Internet and then run Windows Update. This will force the system to connect to the Windows Server, and the license will be updated automatically.

## [**Use the Windows Offline Activation via call support:**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve--unable-to-reach-windows-activation-servers-#use-the-windows-offline-activation-via-call-support)

In cases where Internet access is restricted, you can activate Windows using offline phone support by following these steps:

1. Open CMD and run the command `slui 4`

2. The Windows Activation will pop up. Choose your **country or region.**

3. On the next page, you will see the Installation ID displayed as 9 groups of numbers.

4. Requesting the Confirmation ID:

   1. Call the **Toll-free** number shown on the same screen and follow the prompts to obtain the Confirmation ID.
   2. If you need OPSWAT Support to make the call on your behalf, please create a support case and include the Installation ID. After verification with Microsoft, the Confirmation ID will be sent to you via support case.
5. After receiving the Confirmation ID, click the **'Enter confirmation ID'** button to input the code into Windows and complete the activation. If you've already closed that screen, you can resume the process by running the command `slui 4`. The Confirmation ID consists of 8 groups of digits, labeled in order from A to H.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
