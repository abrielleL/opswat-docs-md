<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup -->

# Active Directory and LDAP Authentication Sources Setup

NAC provides the ability to define multiple authentication servers. These servers can be any variety of LDAP or a MySQL database server. When using Active Directory, Windows domain member machines will be able to use single sign on to authenticate to NAC.

The purpose of this document is to go through the steps necessary to configure and use LDAP and/or MySQL authentication within a NAC policy group. Once configured, authentication servers can be set up in an authentication chain so that a single user’s credentials can be validated against multiple authentication servers in cases where there are multiple directories in use. The entire process will be completely transparent to the end users.

For SQL Authentication Server Setup click [here](/docs/manac/nac-v8.1.1/configuration/sql-authentication-server-setup).

To configure Chained Authentication Sources click [here](/docs/manac/nac-v8.1.1/configuration/chained-authentication-servers).

## [AD/LDAP server setup](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#adldap-server-setup)

The configuration for authentication can be found in the ‘Network Inputs > Authentication Sources’ section of the Configuration Manager page. To configure a new AD/LDAP authentication server, click on the “Add” button.

## [Step 1: Define the Connection Information](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#step-1-define-the-connection-information)

This step tests your ability to physically connect to the authentication server and to login using the information provided.

1. In the **URL** field, enter the host name or IP address of your directory server, in the format “ldap://” or “ldaps://”.
2. If you are using the standard ports (389 for ldap, 636 for ldaps), a port number is not needed.
3. If you are connecting to a Global Catalog Server, or if you need to use another non-standard port please enter the port number after the URL in the typical format: “ldap://dc.organisation.org:3268”.
4. In the **Admin DN** field, include the full distinguished name of the username you have created for the NAC Appliance.
5. When connecting to Microsoft Active Directory, you may need to specify the value in the format: “username@domain”.
6. In the **Password** field, enter the password corresponding to the Admin DN from the previous box.

Info

Example

**LDAP:** "uid=nac,ou=users,ou=accounts,o=organization"

**Active Directory:** "cn=opswat,ou=users,ou=accounts,dc=organization,dc=org", or “opswat@[organization.org](http://organization.org)”

### [LDAPS Certificates](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#ldaps-certificates)

When using a public CA (Thawte, Verisign, GoDaddy, etc.), a copy of the domain certificate from the LDAP server is required in order to query your LDAP server over SSL. With a certificate signed by a trusted CA, root certificate is not needed, just the domain certificate. These should be in PEM or Base64-encoded, format.

If using self-signed SSL certs, a copy of the appropriate machine certs for any devices NAC will interact with, as well as the institution's Trusted Root cert will need to be provided. These should be in PEM or Base64-encoded, format.

1. Remove the check under 'Use Default Certificates'
2. Select Choose File.
3. Browse to the directory where the certs are stored.
4. Select the certificate.
5. Click Open
6. Click Test

Note

If you want NAC to perform searches over SSL **AND** your organization is using a self-signed SSL cert, you will need to contact NAC support at [OPSWAT Support](https://opswat.com/support/).

## [Step 2: Define the searching parameters](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#step-2-define-the-searching-parameters)

This step tests your ability to find the supplied user in the directory tree based on the information provided.

1. **Base DN** field should contain a string that indicates which portion of directory tree will be searched, starting with the most specific level and going to the least.

   1. If you would like the NAC Appliance to search your whole directory structure, you can simply include the highest level of the tree

      1. Examples: "dc=organization,dc=org" or "ou=accounts,o=organisation".
2. **Naming Attribute** field represents how individual usernames are stored at the bottom level of the tree.

   1. In typical LDAP, this is usually **CN** or **UID**.
   2. Active Directory servers use the **sAMAccountName** value by default.

      1. If your users enter their usernames in the “user@domain” format, **UserPrincipalName OR sAMAccountName** may need to be selected.
      2. The “Advanced” option should only be used after consulting the OPSWAT Support team at [opswat.com/support](https://www.opswat.com/support/).
3. **Valid Username** field must contain a username that you know can already authenticate against the current server.
4. Once all information for this section has been entered, the settings can be validated by clicking on the “**Test**” button.

   1. The **Common Configuration Errors** section below contains a chart of common error messages and the resolutions. If the indicator changes to green, your server information is valid.

### [Optional AD/LDAP server fields](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#optional-adldap-server-fields)

- **Root DSE –** This option should only be selected if the authentication server has multiple directory trees and NAC should only be used with one.
- **Secondary Auth Filter –** Checks for additional filters such as group membership.

Example1: User must be have ResNet specified in their personAffiliation attribute
personAffliation=StudentExample2: User must NOT have Faculty OR Staff specified in their personAffiliation attribute
(&(!(personAffiliation=Faculty)(personAffiliation=Staff)Example3: User must have either Faculty OR Staff specified in their personAffiliation attribute
(&(|(personAffiliation=Faculty)(personAffiliation=Staff)

- **Group Search Type –** If AD/LDAP group membership is used as a qualifier in a policy group and is not working as expected, setting this will specify the attribute being used to store the group membership information. If you are using nested groups with standard Active Directory attributes, “tokengroup” should be selected here. In many cases, setting this value will not be necessary.
- **Group Membership Filter –** This field is used to specify a non-standard attribute where the group name is stored. If this is left blank, NAC will only look for a group name using standard AD/LDAP attributes. If this option is used, anything selected in the Group Search Type field will be ignored.

### [Active Directory not Recognizing Tokengroups](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#active-directory-not-recognizing-tokengroups)

Tokengroups are sometimes referred to as nested groups. If a user assigned to a child group cannot authenticate properly when the parent group is required, in some configurations, a shorter BaseDN may be needed. In some configurations, too many OU’s in the BaseDN will prevent tokengroups from returning any memberships to NAC.

## [Common Configuration Errors](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#common-configuration-errors)

| **Message:** | Connection refused. |
| --- | --- |
| **Meaning:** | NAC reached the directory server, but the remote machine actively refused to handle the authentication request. |
| **Suggestions:** | - The IP, hostname, port number in the URL may be inaccurate. - If the URL is accurate, the target machine may not be running a directory server. - You may need to explicitly configure the directory server’s firewall to accept connections from the NAC Appliance. |
|  |  |
| **Message:** | Unknown Host |
| **Meaning:** | A DNS lookup of your URL failed. NAC was never able to reach the directory server. |
| **Suggestions:** | - The hostname in the URL may be inaccurate. - You may have used an internal alias (i.e., ldap://auth) as opposed to the full name (i.e., ldap://authentication.organization.lcl) - DNS resolution may be down for some reason. You can test this by using a directory server’s IP address in the URL instead of its hostname. |
|  |  |
| **Message:** | Connection timed out. |
| **Meaning:** | NAC couldn’t reach the directory server. |
| **Suggestions:** | - The hostname or IP in the URL may be inaccurate. - If the URL is accurate, something in the network is preventing the communication. Common culprits are firewalls and networking configurations. |
|  |  |
| **Message:** | User not found. |
| **Meaning:** | In LDAP, NAC submitted the bind credentials, but the directory server couldn’t find the bind account in the location specified by the DN. |
| **Suggestions:** | - Verify that the bind DN is entered correctly. - Verify that the bind account has not expired or been deleted. - Verify that the bind account has not been moved to a different group or container. |
|  |  |
| **Message:** | Invalid Credentials |
| **Meaning:** | NAC submitted the bind credentials, but the directory server couldn’t verify them.   - In AD: Either the DN or password are invalid. - In LDAP: The password is invalid. |
| **Suggestions:** | - Verify that the password is entered correctly. - Verify that the password has not expired or been reset. - If you’re using AD, instead of the FQDN, try entering the username in “user@domain” format. |

## [LDAP Error Codes](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup#ldap-error-codes)

| Error Code | Error | Description |
| --- | --- | --- |
| 0 | LDAP_SUCCESS | Indicates the requested client operation completed successfully. |
| 1 | LDAP_OPERATIONS_ERROR | Indicates an internal error. The server is unable to respond with a more specific error and is also unable to properly respond to a request. It does not indicate that the client has sent an erroneous message. In NDS 8.3x through NDS 7.xx, this was the default error for NDS errors that did not map to an LDAP error code. To conform to the new LDAP drafts, NDS 8.5 uses 80 (0x50) for such errors. |
| 2 | LDAP_PROTOCOL_ERROR | Indicates that the server has received an invalid or malformed request from the client. |
| 3 | LDAP_TIMELIMIT_EXCEEDED | Indicates that the operation's time limit specified by either the client or the server has been exceeded. On search operations, incomplete results are returned. |
| 4 | LDAP_SIZELIMIT_EXCEEDED | Indicates that in a search operation, the size limit specified by the client or the server has been exceeded. Incomplete results are returned. |
| 5 | LDAP_COMPARE_FALSE | Does not indicate an error condition. Indicates that the results of a compare operation are false. |
| 6 | LDAP_COMPARE_TRUE | Does not indicate an error condition. Indicates that the results of a compare operation are true. |
| 7 | LDAP_AUTH_METHOD_NOT_SUPPORTED | Indicates that during a bind operation the client requested an authentication method not supported by the LDAP server. |
| 8 | LDAP_STRONG_AUTH_REQUIRED | Indicates one of the following: In bind requests, the LDAP server accepts only strong authentication. In a client request, the client requested an operation such as delete that requires strong authentication. In an unsolicited notice of disconnection, the LDAP server discovers the security protecting the communication between the client and server has unexpectedly failed or been compromised. |
| 9 |  | Reserved. |
| 10 | LDAP_REFERRAL | Does not indicate an error condition. In LDAPv3, indicates that the server does not hold the target entry of the request, but that the servers in the referral field may. |
| 11 | LDAP_ADMINLIMIT_EXCEEDED | Indicates that an LDAP server limit set by an administrative authority has been exceeded. |
| 12 | LDAP_UNAVAILABLE_CRITICAL_EXTENSION | Indicates that the LDAP server was unable to satisfy a request because one or more critical extensions were not available. Either the server does not support the control or the control is not appropriate for the operation type. |
| 13 | LDAP_CONFIDENTIALITY_REQUIRED | Indicates that the session is not protected by a protocol such as Transport Layer Security (TLS), which provides session confidentiality. |
| 14 | LDAP_SASL_BIND_IN_PROGRESS | Does not indicate an error condition, but indicates that the server is ready for the next step in the process. The client must send the server the same SASL mechanism to continue the process. |
| 15 |  | Not used. |
| 16 | LDAP_NO_SUCH_ATTRIBUTE | Indicates that the attribute specified in the modify or compare operation does not exist in the entry. |
| 17 | LDAP_UNDEFINED_TYPE | Indicates that the attribute specified in the modify or add operation does not exist in the LDAP server's schema. |
| 18 | LDAP_INAPPROPRIATE_MATCHING | Indicates that the matching rule specified in the search filter does not match a rule defined for the attribute's syntax. |
| 19 | LDAP_CONSTRAINT_VIOLATION | Indicates that the attribute value specified in a modify, add, or modify DN operation violates constraints placed on the attribute. The constraint can be one of size or content (string only, no binary). |
| 20 | LDAP_TYPE_OR_VALUE_EXISTS | Indicates that the attribute value specified in a modify or add operation already exists as a value for that attribute. |
| 21 | LDAP_INVALID_SYNTAX | Indicates that the attribute value specified in an add, compare, or modify operation is an unrecognized or invalid syntax for the attribute. |
| 22-31 |  | Not used. |
| 32 | LDAP_NO_SUCH_OBJECT | Indicates the target object cannot be found. This code is not returned on following operations: search operations that find the search base but cannot find any entries that match the search filter. Bind operations. |
| 33 | LDAP_ALIAS_PROBLEM | Indicates that an error occurred when an alias was dereferenced. |
| 34 | LDAP_INVALID_DN_SYNTAX | Indicates that the syntax of the DN is incorrect. (If the DN syntax is correct, but the LDAP server's structure rules do not permit the operation, the server returns LDAP_UNWILLING_TO_PERFORM). |
| 35 | LDAP_IS_LEAF | Indicates that the specified operation cannot be performed on a leaf entry. (This code is not currently in the LDAP specifications but is reserved for this constant). |
| 36 | LDAP_ALIAS_DEREF_PROBLEM | Indicates that during a search operation, either the client does not have access rights to read the aliased object's name or dereferencing is not allowed. |
| 37-47 |  | Not used. |
| 48 | LDAP_INAPPROPRIATE_AUTH | Indicates that during a bind operation, the client is attempting to use an authentication method that the client cannot use correctly. For example, either of the following cause this error: the client returns simple credentials when strong credentials are required...OR...The client returns a DN and a password for a simple bind when the entry does not have a password defined. |
| 49 | LDAP_INVALID_CREDENTIALS | Indicates that during a bind operation one of the following occurred: The client passed either an incorrect DN or password, or the password is incorrect because it has expired, intruder detection has locked the account or another, similar reason. See the data code for more information. |
| 49 / 52e | AD_INVALID CREDENTIALS | Indicates an Active Directory (AD) *AcceptSecurityContext* error, which is returned when the username is valid but the combination of password and user credential is invalid. This is the AD equivalent of LDAP error code 49. |
| 49 / 525 | USER NOT FOUND | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is returned when the username is invalid. |
| 49 / 530 | NOT_PERMITTED_TO_LOGON_AT_THIS_TIME | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is logon failure caused because the user is not permitted to log on at this time. Returns only when presented with a valid username and valid password credential. |
| 49 / 531 | RESTRICTED_TO_SPECIFIC_MACHINES | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is logon failure caused because the user is not permitted to log on from this computer. Returns only when presented with a valid username and valid password credential. |
| 49 / 532 | PASSWORD_EXPIRED | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is a logon failure. The specified account password has expired. Returns only when presented with valid username and password credentials. |
| 49 / 533 | ACCOUNT_DISABLED | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is a logon failure. The account is currently disabled. Returns only when presented with valid username and password credentials. |
| 49 / 568 | ERROR_TOO_MANY_CONTEXT_IDS | Indicates that during a log-on attempt, the user's security context accumulated too many security IDs. This is an issue with the specific LDAP user object/account which should be investigated by the LDAP administrator. |
| 49 / 701 | ACCOUNT_EXPIRED | Indicates an Active Directory (AD) *AcceptSecurityContext* data error that is a logon failure. The user's account has expired. Returns only when presented with valid username and password credentials. |
| 49 / 773 | USER MUST RESET PASSWORD | Indicates an Active Directory (AD) *AcceptSecurityContext* data error. The user's password must be changed before logging on the first time. Returns only when presented with valid username and password credentials. |
| 50 | LDAP_INSUFFICIENT_ACCESS | Indicates that the caller does not have sufficient rights to perform the requested operation. |
| 51 | LDAP_BUSY | Indicates that the LDAP server is too busy to process the client request at this time but if the client waits and resubmits the request, the server may be able to process it then. |
| 52 | LDAP_UNAVAILABLE | Indicates that the LDAP server cannot process the client's bind request, usually because it is shutting down. |
| 53 | LDAP_UNWILLING_TO_PERFORM | Indicates that the LDAP server cannot process the request because of server-defined restrictions. This error is returned for the following reasons: The add entry request violates the server's structure rules...OR...The modify attribute request specifies attributes that users cannot modify...OR...Password restrictions prevent the action...OR...Connection restrictions prevent the action. |
| 54 | LDAP_LOOP_DETECT | Indicates that the client discovered an alias or referral loop, and is thus unable to complete this request. |
| 55-63 |  | Not used. |
| 64 | LDAP_NAMING_VIOLATION | Indicates that the add or modify DN operation violates the schema's structure rules. For example, the request places the entry subordinate to an alias. The request places the entry subordinate to a container that is forbidden by the containment rules. The RDN for the entry uses a forbidden attribute type. |
| 65 | LDAP_OBJECT_CLASS_VIOLATION | Indicates that the add, modify, or modify DN operation violates the object class rules for the entry. For example, the following types of request return this error: The add or modify operation tries to add an entry without a value for a required attribute. The add or modify operation tries to add an entry with a value for an attribute which the class definition does not contain. The modify operation tries to remove a required attribute without removing the auxiliary class that defines the attribute as required. |
| 66 | LDAP_NOT_ALLOWED_ON_NONLEAF | Indicates that the requested operation is permitted only on leaf entries. For example, the following types of requests return this error: The client requests a delete operation on a parent entry. The client request a modify DN operation on a parent entry. |
| 67 | LDAP_NOT_ALLOWED_ON_RDN | Indicates that the modify operation attempted to remove an attribute value that forms the entry's relative distinguished name. |
| 68 | LDAP_ALREADY_EXISTS | Indicates that the add operation attempted to add an entry that already exists, or that the modify operation attempted to rename an entry to the name of an entry that already exists. |
| 69 | LDAP_NO_OBJECT_CLASS_MODS | Indicates that the modify operation attempted to modify the structure rules of an object class. |
| 70 | LDAP_RESULTS_TOO_LARGE | Reserved for CLDAP. |
| 71 | LDAP_AFFECTS_MULTIPLE_DSAS | Indicates that the modify DN operation moves the entry from one LDAP server to another and requires more than one LDAP server. |
| 72-79 |  | Not used. |
| 80 | LDAP_OTHER | Indicates an unknown error condition. This is the default value for NDS error codes which do not map to other LDAP error codes. |
