<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/authentication-sources-setup -->

# Authentication Sources Setup

NAC allows the configuration of multiple authentication servers, including various LDAP servers. Active Directory users on Windows domain machines can utilize single sign-on for NAC authentication.

### Setup AD/LDAP server

1. Log into the **My OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS NAC**
3. Click on **Authentication Sources** tab
4. Click **Add AD/LDAP Connection** button

### Specify your LDAP Connection Information

1. In the **URL** field, enter the host name or IP address of your directory server in the format`ldap://` or `ldaps://`
   - For standard ports (389 for LDAP, 636 for LDAPS), you do not need to specify the port number.
   - If connecting to a Global Catalog Server or using a non-standard port, append the port number to the URL in this format: ldap://dc.organisation.org:3268.
2. In the **Admin DN** field, enter the full Distinguished Name (DN) of the user account created for the NAC Appliance.
   - For Microsoft Active Directory, you may need to use the format username@domain
3. In the **Password** field, provide the password associated with the Admin DN entered in the previous step.

![](https://uploads.developerhub.io/prod/6Ad9/zjn713g0muzcx10a7d1s9xigg1j0klefeuwb7u3s1jvgynlvbv7qy5vpyq7n36ak.png)

### Define the searching parameters

1. **Base DN** field should contain a string that indicates which portion of directory tree will be searched, starting with the most specific level and going to the least.
   1. If you would like the NAC Appliance to search your whole directory structure, you can simply include the highest level of the tree
      1. Examples: "dc=organization,dc=org" or "ou=accounts,o=organisation".
2. **Naming Attribute** field represents how individual usernames are stored at the bottom level of the tree.
   1. In typical LDAP, this is usually **CN** or **UID**.
   2. Active Directory servers use the **sAMAccountName** value by default.
      1. If your users enter their usernames in the “user@domain” format, **UserPrincipalName OR sAMAccountName** may need to be selected.
      2. The “Advanced” option should only be used after consulting the OPSWAT Support team at [opswat.com/support](https://www.opswat.com/support/).

![](https://uploads.developerhub.io/prod/6Ad9/a42bkk3v0tuy4po07m188w855a3nxap5arzma04dweowmffafnj24h9v7sindofl.png)

### Confirm your LDAP Server Name

![](https://uploads.developerhub.io/prod/6Ad9/8m10x43rjq68jngyt82vwdrnrr5wewasznzj0kruu05g8ii0xnb9pv3r940gosue.png)
