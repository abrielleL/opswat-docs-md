<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/chained-authentication-servers -->

# Chained Authentication Servers

Chained authentication sources allow multiple sources to be used by a single authentication policy. The configuration for authentication can be found in the ‘Network Inputs > Authentication Sources > Chained Authentication Sources’ section of Configuration Manager.

For Active Directory and LDAP Authentication Setup click [here](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup).

## [Create Authentication Chain](/docs/manac/nac-v8.1.1/configuration/chained-authentication-servers#create-authentication-chain)

Define and manage individual connections to your authentication sources, or group them into chains.

1. To configure a new authentication server chain, click “**Create Authentication Chain**".
2. To pick your desired from **Available Authentication Sources** from the left to the right.
3. When in use, authentication sources will be checked on the order they are placed.

   1. You may reorder your authentication sources top to bottom. Top being the highest priority
4. **Auth Chain Label** enter the name of your combined authentication scheme, as you would like it to appear in the Policy Manager and in the Device Manager
5. After the configuration is complete, click on **Save**.

Info

In a chained authentication server scenario, a user will check against each server in the chain in the order specified until a match is made. If a match is made in the first server of the chain, the remaining servers will not be checked for an authentication match.

Note

An Authentication Chain should NOT have the same name as an Authentication Server.

## [Edit Authentication Chain](/docs/manac/nac-v8.1.1/configuration/chained-authentication-servers#edit-authentication-chain)

1. To edit an existing chain click on the edit icon under **Modify**.
2. Servers can be added to or removed from a chain by moving the authentication source under **Chosen Authentication Sources** from right to left.
3. After changes are completed click **Save**.
