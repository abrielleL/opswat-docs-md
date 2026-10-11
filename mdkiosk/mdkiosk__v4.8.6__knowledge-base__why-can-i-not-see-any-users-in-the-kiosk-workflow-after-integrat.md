<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-can-i-not-see-any-users-in-the-kiosk-workflow-after-integrat -->

# Why can I not see any users in the Kiosk workflow after integrating with EntraID (SAML)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to the MD Kiosk (Windows)

“After integrating the MD Kiosk with the EntraID (SAML) user directory, I cannot see any users/groups to assign to the MD Kiosk workflow.”

When this behavior occurs, it is not an issue with the MD Kiosk. Instead, it happens because the integration does not include this capability by default. To allow the MD Kiosk to retrieve user and group information, you must complete additional steps to grant the necessary permissions for the MD Kiosk to query users and groups in the Entra ID directory through the GraphAPI application.

For the detailed steps, you can follow the instructions in this article <https://www.opswat.com/docs/mdkiosk/advanced-deployment/microsoft-entra-id-integration#integrate-with-microsoft-graphapi-and-fetching-usersgroups>

Warning:

Make sure that you access the [Microsoft Entra admin center](https://entra.microsoft.com/) using your administrative credentials to perform the steps above

If you have already done the configuration with the GraphAPI application but still have the same behavior, you may need to double-check the required permissions on the API:

- **User.Read.All** permission to query users from the tenant.
- **Group.Read.All** permission to query groups from the tenant.
- **GroupMember.Read.All** permission to query users within groups.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
