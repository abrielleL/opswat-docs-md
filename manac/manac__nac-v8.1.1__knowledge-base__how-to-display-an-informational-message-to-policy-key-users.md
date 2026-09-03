<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-to-display-an-informational-message-to-policy-key-users -->

# How to display an informational message to Policy Key users?

This article applies to the current NAC API, Web UI, and all Windows and MacOS systems running the latest NAC Policy Key.

Please Note:

The following process will only work on devices running NAC’s Policy Key, and requires administrators to set up a customized web page to which users will be linked in a browser pop-up window triggered by the Policy Key messaging feature.

This should not be considered as the primary user notification method for security alerts and emergencies.

In order to provide managed, Policy Key device end users with a custom message, administrators should follow the instructions below.

1. Create a custom web page on which to display the desired message.

   1. Download the template JSP file
   2. Modify the file to contain your custom message
   3. Click “Choose File” and browse to your modified JSP file
   4. Click “Upload and Preview” to verify the result looks as intended
   5. Click “Save” to save the new web sessage

2. Create a custom policy that contains a check for both the Windows and macOS Policy Key processes.
3. Set the custom condition to fail if any of the conditions are met.
4. Set the enforcement level to **Audit**, so that all assigned groups and users will see the message.

Pro Tip:

This can be set to drop to **Warning** level after a desired interval, as required, in which case the page will be displayed to policy-assigned users who are currently online, but offline users will only see it when they log back into the network. Once the set interval has passed, administrators can reset the enforcement system by setting the enforcement level back to **Audit**.

5. Set the page displayed to your custom web page.

6. Apply the policy to all groups for which you wish the message to be displayed.

Support:

If you have followed the instructions above but have been unable to **Display An Informational Message To Your Policy Key Users**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
