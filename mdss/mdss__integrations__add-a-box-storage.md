<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-box-storage -->

# Add a Box Storage

In order to integrate Box with MetaDefender Storage Security please follow these steps:

Info

Steps 4 and 5 are optional. Perform them in order to set up a specific location for file processing.

1. From the left side menu, navigate to **Inventory**, click on **Add unit** and choose **Box**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

2. Upload your **Credentials** file. Scroll down for more details.
3. (Optional) Enter the Webhook ID, you can find more details in this page [Event-based handling for Box](/docs/mdss/configuration/event-based-handling-for-box)
4. Click Next and after account is successfully created, please add a unit to it

5. Enter an unique name for your unit.
6. Assign the unit to a Group.
7. Set up a specific location as a source of files that should be processed By MetaDefender Storage Security

   1. **All Users** - process files from all users created by the custom application, from the application itself and also from all the Enterprise users, depending on the Application Access provided
   2. **A specific user or custom app** - process only the files from a specific user/custom app. Additionally you can set up a location as a source of files, by filling in the full path of the folder. Make sure it’s a valid path corresponding to the User or Custom App name you previously added. Note that it could take up to 10-15 minutes for newly added folders to be discovered.
   3. **A specific group***-* process only the files from a group of users
8. Select **Add** in order to finish the process.

Info

For most Box applications “All Files” is considered the root of the folder structure. To be able to scan entire structure of folders from a user or custom application, Folder Path field should remain empty.

### [How can I generate a Public / Private key pair](/docs/mdss/integrations/add-a-box-storage#how-can-i-generate-a-public--private-key-pair)

To generate a file that contains all the necessary information to connect MetaDefender Storage Security to your Box storage please follow these steps:

1. Log in to [**Box**](https://www.box.com/) and then go to [Dev Console](https://app.box.com/developers/console)
2. From the console, choose **Create New App**

3. Select **Custom App** and click **Next**

4. Choose **OAuth 2.0 with JWT (Server Authentication)** as the authentication method and give your app a name, for example **MetaDefender Storage Security** and then click **Create App**

5. You will receive a message saying that your app has been successfully created. Click **View Your App**.
6. You will be redirected to the app **General Settings** page, switch to **Configuration**.
7. Scroll down to the **Application Access** section and choose **App Access Only** or **App Access + Enterprise Access**. Selecting **App Access only** will allow MetaDefender Storage Security to be able to process files from the users created by the custom application and also from the application itself. Selecting **App Access + Enterprise Access** will allow MetaDefender Storage Security to be able to process files from the users created by the custom application, from the application itself and also from the Enterprise users.

8. Scroll down to the **Application Scopes** section and make sure that the following permissions are checked:

   1. Read all files and folders stored in Box
   2. Read and write all files and folders stored in Box
   3. Manage users
   4. Manage groups

9. Next, please scroll down to the **Advanced Features** section and make sure that both **Perform Actions as Users** and **Generate Users Access Tokens** are enabled

10. Make sure you **save your changes.**
11. The next step will be to generate a Public/Private Keypair

**Note:** When performing this action you may be required to re-authenticate using a two-factor authentication method. If this happens, after re-authenticating, please go back and click **Generate Public/Private Keypair** again

12. A configuration file with all of your app settings will be downloaded. Please store it securely as you will need it a bit later
13. Click to **Authorization** menu.

14. Click **Review and Submit**. From the popup that will appear, please make a copy of the **Client ID**

15. Click **Submit**
16. From the left-side menu, please press **Back to My Account** and switch to **Admin Console**.
17. Using the Admin Console left-side menu, navigate to **Apps** and then **Custom Apps**

18. Click “**+”** and paste the previously copied **Client ID** and then click **Next**

19. Review the application permissions once again and then click **Authorize**

20. Almost done! All you need to do is go back to the MetaDefender Storage Security web interface and upload the **Public/Private Keypair** that you generated earlier in the **Credentials** field.

### [How my metadata is managed](/docs/mdss/integrations/add-a-box-storage#how-my-metadata-is-managed)

Warning

In Box, we support metadata, but with some limitations:

1. If the remediation actions are enabled and the file needs to be moved between accounts of the same enterprise, the metadata will be fully transferred.
2. If the remediation actions are enabled and the file needs to be moved between accounts of different enterprises, the metadata and its fields must be the same in these accounts in order to match. Otherwise, the metadata that does not match will be lost.
