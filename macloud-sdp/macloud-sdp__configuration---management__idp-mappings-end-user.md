<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/idp-mappings-end-user -->

# IdP Mappings - End User

Within MetaDefender IT Access, administrators have the ability to create users (both end-users and console users). This document covers how to set up console users who will access the MetaDefender IT Access console, and end-users, who will access Secure IT Access on a client device, by using IdP.

*Note: IdP users are a paid feature in MetaDefender IT Access, you can learn more about MetaDefender IT Access. Pricing* [*here*](https://www.opswat.com/uploads/assets/files/Product-Guide_compressed-1.pdf)*.*

## [Add a end-user (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-end-user#add-a-end-user-idp)

To add IdP end-users to your account, you will need to set up Single Sign On (SSO) first. Steps on how to do this can be found [here](https://docs.opswat.com/macloud-sdp/3.16.0/configuration---management/setup-sso). Once SSO is established, to set up IdP groups:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups SDP**.
3. Select **Add**.
4. Enter the IdP Group established in your third-party service provider. This will create the name used in MetaDefender IT Access as well. If you'd like the group to have a different name in MetaDefender IT Access, it can be changed at any time. Additionally, in cases where the external value provided in the SAML Assertion is not human friendly, such as cases where a UUID is returned rather than an actual group name, the MetaDefender IT Access IDP Group's name serves to provide a more helpful alias when working with the group within MetaDefender IT Access.
5. Optional: Enable **User Group Permission.** This setting prompts end users to use their IdP login to authorize installation of the MetaDefender Endpoint. Note: For this feature to work, you will need to force registration upon installation of the MetaDefender Endpoint. More information on that, [here](https://docs.opswat.com/macloud-sdp/configuration---management/global-settings).
6. Optional: Select the **Applications** tab, and assign applications to the IdP Mapping. If you are not using Secure IT Access, this is not required.
7. Enter your PIN to confirm the action.
8. Click on the **Save** button to send out the invitation.
9. Once completed, IdP users will be able to access this application through their provider.

## [Update an end-user (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-end-user#update-an-end-user-idp)

IdP Group names and application access can be updated after being added. To update an IdP group:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups** **Secure IT Access**.
3. Select the **Edit** (pencil icon) button by the group.
4. Make the appropriate changes to the group.
5. Optional: to change their application assignment, navigate to **Applications** and update the group's access.
6. Enter your PIN to confirm the action.
7. Click **Update**.

## [Delete an end-user (IdP)](/docs/macloud-sdp/configuration---management/idp-mappings-end-user#delete-an-end-user-idp)

To remove an IdP group and their access to Secure IT Access:

1. Log into MetaDefender IT Access console
2. Go to **User Management > IdP Groups > IdP Groups** **Secure IT Access**.
3. Select the group you wish to remove by checking the box next to the group name.
4. Select **Delete**.
5. Enter your PIN to confirm the action.
6. Select **Delete.**
