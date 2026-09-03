<!-- source: https://www.opswat.com/docs/cm/user-management/map-idp-groups -->

# Map IdP groups

This guideline walks you through steps to map your IdP user groups to My OPSWAT Central Management and assign a specific role to that group.

## Add an IdP group

Before doing this, you will need to [add your own IdP](https://www.opswat.com/docs/cm/user-management/through-your-own-idp) to My OPSWAT Central Management to allow your IdP users log into the management console. Once your IdP is configured, to set up console IdP groups:

1. Log into My OPSWAT Central Management console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select **Add**.
4. Enter the IdP Group established in your third-party service provider. This will create the name used in My OPSWAT Central Management as well. If you'd like the group to have a different name in My OPSWAT Central Management, it can be changed at any time. Additionally, in cases where the external value provided in the SAML Assertion is not human friendly, such as cases where a UUID is returned rather than an actual group name, the My OPSWAT Central Management IDP Group's name serves to provide a more helpful alias when working with the group within My OPSWAT Central Management.
5. Select a user role you wish them to have on the Invitation popup.
6. Enter your PIN to confirm the action.
7. Click on the **Save** button to send out the invitation.
8. Once completed, users in this IdP group will be able to access the management console through the IdP app dashboard and will be assigned with the role you assigned to this group.

## Update a console IdP user group

IdP Group names and roles can be updated after being added. To update an console IdP group:

1. Log into My OPSWAT Central Management console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select the pencil icon of a group you would like to update.
4. Make the appropriate changes to the group.
5. Enter your PIN to confirm the action.
6. Click **Update**.

## Delete a console IdP user group

To delete a console IdP group and their access to My OPSWAT Central Management:

1. Log into My OPSWAT Central Management console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select a group you wish to delete by checking the box next to the group name.
4. Select **Delete** action
5. Enter your PIN to confirm the action and click **Delete** button
