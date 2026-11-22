<!-- source: https://www.opswat.com/docs/mdcloud/compliance/customer-user-lifecycle-policy -->

# Customer User Lifecycle Policy

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### [**1. Your API key**](/docs/mdcloud/compliance/customer-user-lifecycle-policy#1-your-api-key)

When you register an account with OPSWAT, at [my.opswat.com](http://my.opswat.com) or [metadefender.com](http://metadefender.com), MetaDefender Cloud creates an API key for you automatically and associates it with the email address you registered with. There is nothing to request: every registered user has one key. You can see your key, your licence and the limits that apply to it on your [account page.](https://metadefender.com/account)

Send the key in the `apikey` header of every request. The key identifies and authenticates you: every scan you submit and every result you read is tied to your account through it.

The limits of your key depend on your licence: Community, Standard, Professional or Enterprise. If you are part of an organisation, the organisation's limits apply instead, and the usage of all its users counts towards them.

Treat your key like a password: anyone who has it can scan files and read results as you. Do not share it and do not store it where others can read it. Your key does not expire, and you cannot create, regenerate or delete keys yourself. If you need a replacement, or want a key disabled, follow "Rotating and revoking API keys".

### [**2. Removing a user from your organisation**](/docs/mdcloud/compliance/customer-user-lifecycle-policy#2-removing-a-user-from-your-organisation)

As an administrator you can remove any user from your organisation at any time. As soon as the user is removed, their API key can no longer use your organisation's workflows or engine profiles, read your organisation's scan history, or consume your organisation's limits. The scans the user submitted themselves stay in their own scan history.

The user's API key is not revoked when you remove them. It keeps working as their personal key, with their personal limits, workflows and engine profiles. If the key must stop working, request its revocation as described in "Rotating and revoking API keys".

Administrators can only remove users with the role type: ‘User’ or ‘Analyst’. When removing such users administrators will be prompted in order to confirm if they want to continue with the action. In order to remove other administrators a support ticket needs to be raised.

### [**3. Rotating and revoking API keys**](/docs/mdcloud/compliance/customer-user-lifecycle-policy#3-rotating-and-revoking-api-keys)

MetaDefender Cloud API keys do not expire. Rotate a key on the schedule your security policy sets, when the person who created it leaves, or immediately if you suspect it has been exposed.

Rotation and revocation are performed by OPSWAT at your request. Open a request with OPSWAT Support stating your account or organisation, your region, whether you want rotation (a replacement key) or revocation only, the reason, the last four characters of the key, and a technical contact. OPSWAT verifies that you are authorised, revokes the key and, for a rotation, delivers the replacement through a secure channel. Plan for a short interruption between the old key being revoked and the new one being deployed.

To confirm that a revoked key no longer works, call the API key information endpoint and a test upload with it; both must return 401 Unauthorized. If either succeeds, stop using the key and contact Support.

### [**4. Users you disable in your identity provider**](/docs/mdcloud/compliance/customer-user-lifecycle-policy#4-users-you-disable-in-your-identity-provider)

If your organisation uses single sign-on, disabling a user in your identity provider does not remove them from MetaDefender Cloud and does not revoke their API keys; the keys keep working. Remove the user in MetaDefender Cloud as well, and request revocation of their keys if needed.

### [**5. Roles and permissions**](/docs/mdcloud/compliance/customer-user-lifecycle-policy#5-roles-and-permissions)

MetaDefender Cloud has three user roles. An Administrator can add other users, create sub-organisations and set their limits, change your organisation's security policies, scan files and view scan results. A User can scan files and view scan results. An Analyst can only view scan results. The table below lists what each role can do, built from the product's permission configuration.

| What you can do | Administrator | User | Analyst |
| --- | --- | --- | --- |
| Add and remove users | Yes | No | No |
| Create sub-organisations | Yes | No | No |
| Set sub-organisation limits | Yes | No | No |
| Change security policies | Yes | No | No |
| Scan files | Yes | Yes | No |
| View scan results | Yes | Yes | Yes |
