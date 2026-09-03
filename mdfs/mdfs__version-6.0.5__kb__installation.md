<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/kb/installation -->

# How to Install MetaDefender for Salesforce

## [Installation Guide](/docs/mdfs/version-6.0.5/kb/installation#installation-guide)

Info

Prior to installing the MetaDefender for Salesforce application, ensure that you have obtained your API key by following a series of straightforward steps:

1. Register an email address on the [OPSWAT Portal](https://id.opswat.com/register?app=appOCM0001&SAMLRequest=jZJRb4IwEMe%2FCul7KSBObATDNMtMNDrFPeytlE6bQMu44rZvvw4wcS9mD31o73%2F3v%2FtdZ%2FOvqnQuogGpVYx810OOUFwXUp1idMyecITmyQxYVQY1TVtzVnvx0Qowjk1UQPtIjNpGUc1AAlWsEkANp4d0s6aB69G60UZzXSInBRCNsVYLraCtRHMQzUVycdyvY3Q2pgZKCKulW327uoZPZlyuq98Xwm2GLgUp9Ukq0tkSAE16GXKWtiepmOnmuJaSxW2ZLnXO6jq2Z7vYeJ7nI2e1jFG6fwlH01BEBZ7mOcdhXoxx5I8n2PcYzycTHhb83WoBWrFSYJgyMQq8IMB%2BgAMv8yPqB3QUutHo4Q05u2HiR6l6kvfw5L0I6HOW7fBue8iQ83rdiBWggT%2Ft3Jtb8PcLsyttlPyP7UC13wm2a7vIQjS4EoYVzLCB9YzctpMM17%2B%2FI%2FkB&RelayState=null)
2. Verify your email address via the confirmation email that will be sent to you from our system
3. Log into the [OPSWAT Portal](https://metadefender.opswat.com/account) and copy your API Key, you will need it after installation.
### [I. Installing the application](/docs/mdfs/version-6.0.5/kb/installation#i-installing-the-application)

**Step 1**: Go to the Cloud Security for Salesforce [listing](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000FeG3eUAF&tab=e) on AppExchange and click Get it now

**Step 2:** Select Install for Install for Admins only, then click Install.

Info

By installing for admins only, only your Salesforce administrators will be able to access and view data within the MetaDefender for Salesforce application. If you install for all users, everyone with Salesforce access in your organization will have full access to the MetaDefender for Salesforce app.

**Step 3:** Check on the box “Yes, grant access to these third-party web sites” and then click  Continue to allow the app to send and receive data to/from Metadefender

Wait while the system installs the OPSWAT | MetaDefender for Salesforce.

**Step 4:**  When the installation is complete, a Get-Started message will appear in your browser window and guide you on how to set up the app. In case you need to revisit these instructions, this message can also be found on the app home page. You can click done after reading.

Info

Please check [this instruction](https://www.opswat.com/docs/mdfs/kb/how-to-check-insufficient-privileges-issue-) to be sure that all users have proper permission sets

**Important note:** Please check [this instruction](https://www.opswat.com/docs/mdfs/kb/how-to-check-insufficient-privileges-issue-) to be sure that all users have proper permission sets

You will now be able to view the OPSWAT | Cloud Security for Salesforce application in your App Launcher.

Once you have successfully installed the Cloud Security for Salesforce app, please make sure that you register for an account on the [OPSWAT Portal](https://id.opswat.com/register?redirect=https://my.opswat.com&app=appOCM0001). This will provision you an API key that you will need to plug into the OPSWAT Settings --> MetaDefender.

### [II. Adding your API Key](/docs/mdfs/version-6.0.5/kb/installation#ii-adding-your-api-key)

**Step 1:** Return to the Cloud Security for Salesforce app you just installed, OPSWAT Settings page, and paste your API key in the box pointed out below:

**Step 2:** From the Available Users, select the Users you want to be the app administrators:

**Step 3:** From the Available Users, select the Users you want to be the Approvers within the app (the users you want to receive release request emails):

### [Note:](/docs/mdfs/version-6.0.5/kb/installation#note)

- User with System Admin profile will have the access to the page regardless they are in the list or not. To remove their permission, please remove the "MDFS Admin" permission set on their users.
- Only users who are in selected MDFS Admin can be in the Approver list.

You can refer to [File Security - Configuration and Settings](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings) for more info on the other settings that are configurable on the page shown above.
