<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/configuring-temporary-access-request -->

# Configuring Temporary Access Request

Temporary access allows an end user to gain access to remediation resources when they are not able to immediately meet policy requirements. There are situations, such as installing anti-virus software, where an end user will need network access to meet policy requirements. Prior to access requests, a user would have to call the help desk, where they would then be placed in Open Access by a help desk representative. With temporary access requests, this process can be automated, therefore reducing help desk calls. The purpose of this guide is to introduce you to the configuration and operation of the temporary access feature in NAC. This guide provides all the information needed to fully configure temporary access, and details how an end user will request access and receive subsequent notifications. Let's get started!

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/configuring-temporary-access-request#step-by-step-guide)

Configuring and Enabling Temporary Access:

1. Connect to the management portal. /manage
2. Navigate to "Configuration" > "Device Enrollment" then Click on "Enable Configuration Mode" and then edit Access Request
3. Expand the configurable controls by clicking on "Email Notification" and "Advanced" options buttons

Administrators have the ability to configure temporary access in a variety of ways:

- Max Number of Access Requests:

  - This setting controls how many times an end user may request temporary access per day. It is recommended to keep this settings default of 1 time per day.
- Access Expiration:

  - This setting allows you to specify the exact time restrictions of the temporary access the end user will receive. It is recommended to set this time to no more than 30 minutes. The default of 15 minutes should be more than enough time to access remediation resources.
- Email Notifications:

  - Email address for notification/validation settings will send an email to the configured admin address when an end user requests temporary access.
  - Email address sender settings will send an email to the end user as the configured address when an end user requests temporary access.
- Validation Level:

  - This setting controls how access is granted and whether or not to send notifications. It is recommended to set this to Active Immediately - Notification Sent. This will grant access to the end user immediately and inform the administrator (configured email address) that the end user has requested this access.
- Manipulate Access by:

  - This setting controls how the temporary access will be applied to the client record. It is highly recommended to use MAC Address or Authenticated Name. IP address can have undesirable results if the IP of the requesting end user changes. MAC Address would be best since the temporary access will be tied to the device the request originated from.
- Group Assignment:

  - This setting controls what group the end user will be moved to. It is recommended to leave this defaulted to Temporary Access.

Adding this feature to a remediation page:

4. Connect to the management portal. /manage
5. Navigate to "Policy Manager" > "Web UI Menu" then Click on "Web Messages"
6. Search for 'not installed' and select "Anti-Virus - not installed" from the Web Messages list
7. Select "Quarantine" radio button from the Preview Options and then click "Download Web Message" and save file
8. Open the downloaded file using a text editor and add the following lines to the bottom off the <! – Quarantine Section – > of the file. For ease of use, the modified file had been attached to this document.

<p>You can request temporary access for 15 minutes by clicking the 'Temporary Access Request' button below.</p>
<form action="/access">
<input type="submit" class="btn btn-primary" value="Request Temporary Access" />
</form>

The following is the full section for reference:

<!-- Quarantine version -->
<div style="<c:out value="${model.quarantineDisplay}" />" id="warning">
<p class="alert alert-warning">Your network access from this device is currently suspended.</p>
<p>Just follow the steps we've outlined for you and you'll be right back on the network.</p>
</div>
<p class="alert alert-warning">Your device does not have anti-virus software installed.</p>
<p>You can request temporary access for 15 minutes by clicking the 'Temporary Access Request' button below.</p>
<form action="/access">
<input type="submit" class="btn btn-primary" value="Request Temporary Access" />
</form>
</div>

7. Save changes to the file and **do not** change the file name. The name must be Anti-Virus - not installed.jsp
8. From the Policy Manager - click on "Browse" and select the modified file
9. Select "Upload and Preview" to see what your modifications will look like to the end user
10. Select "Upload and Save Web Message" when you are happy with the results

Warning

Saving **will** overwrite the existing, selected web message.

Info

If you want to use the attached anti-virus file, simply download it, navigate to Policy Manager > Web UI > Web Messages. Search for 'not installed' and select "Anti-Virus - not installed". Click on browse and upload and save the web message.

##

## [Related articles](/docs/manac/nac-v8.1.1/configuration/configuring-temporary-access-request#related-articles)

For environments using the classic web-messages, see the attached document.

[Access Request Configuration SafeConnect V5.4.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4084744_1_Access_Request_Configuration_SafeConnect_V5.4.pdf)
