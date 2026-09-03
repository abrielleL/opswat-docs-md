<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/idp-mappings-console -->

# IdP Mappings - Console User

Within MetaDefender IT Access, administrators have the ability to create users (both end-users and console users). This document covers how to set up console users who will access the MetaDefender IT Access console, and end-users, who will access Secure IT Access on a client device, by using IdP.

*Note: IdP users are a paid feature in MetaDefender IT Access, you can learn more about MetaDefender IT Access Pricing* [*here*](https://www.opswat.com/uploads/assets/files/Product-Guide_compressed-1.pdf)*.*

## [Add a Console User (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-console#add-a-console-user-idp)

To add IdP console users to your account, you will need to set up Single Sign On (SSO) first. Steps on how to do this can be found [here](https://docs.opswat.com/macloud-sdp/3.16.0/configuration---management/setup-sso). Once SSO is established, to set up console IdP groups:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select **Add**.
4. Enter the IdP Group established in your third-party service provider. This will create the name used in MetaDefender IT Access as well. If you'd like the group to have a different name in MetaDefender IT Access, it can be changed at any time. Additionally, in cases where the external value provided in the SAML Assertion is not human friendly, such as cases where a UUID is returned rather than an actual group name, the MetaDefender IT Access IDP Group's name serves to provide a more helpful alias when working with the group within MetaDefender IT Access.
5. Select a user role you wish them to have on the Invitation popup. For more information on user roles, please click [here](https://docs.opswat.com/macloud-sdp/configuration---management/roles).
6. Enter your PIN to confirm the action.
7. Click on the **Save** button to send out the invitation.
8. Once completed, IdP users will be able to access this application through their provider.

## [Update a console user (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-console#update-a-console-user-idp)

IdP Group names and roles can be updated after being added. To update an console IdP group:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select the **Edit** (pencil icon) button by the group.
4. Make the appropriate changes to the group.
5. Enter your PIN to confirm the action.
6. Click **Update**.

## [Delete a console user (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-console#delete-a-console-user-idp)

To remove a console IdP group and their access to MetaDefender IT Access:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups Console**.
3. Select the group you wish to remove by checking the box next to the group name.
4. Select **Delete**.
5. Enter your PIN to confirm the action.
6. Select **Delete.**
