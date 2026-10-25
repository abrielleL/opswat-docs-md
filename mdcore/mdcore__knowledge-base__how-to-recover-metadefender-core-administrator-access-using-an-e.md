<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e -->

# How to recover MetaDefender Core administrator access using an existing admin API key

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [Overview](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#overview)

If you have forgotten your MetaDefender Core administrator password, you can use the **Forgot password?** option when SMTP is configured and the account has a valid, accessible email address.

If SMTP is not configured, but you still have a valid administrator API key, you can create a temporary administrator account through the API. You can then sign in with this account and reset the original administrator’s password.

If you have also forgotten the original administrator username, the procedure below explains how to retrieve it.

## [Prerequisites](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#prerequisites)

- A valid administrator API key with permission to manage users.
- Access to the MetaDefender Core API and Web Management Console.
- A MetaDefender Core version that provides the **Admin direct reset** option.

The commands below use the default address `http://localhost:8008`. Replace the address with your MetaDefender Core endpoint and HTTPS if applicable. Use the Linux/macOS examples in Bash-compatible shells. On Windows, use the separate `curl.exe` PowerShell examples because PowerShell uses different line continuation and quoting rules.

## [Procedure](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#procedure)

### [Step 1: Retrieve the original administrator username](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-1-retrieve-the-original-administrator-username)

If you have forgotten the original administrator username, run the following request to list existing users.

**Linux/macOS:**

curl -sS --request GET \
--url "http://localhost:8008/admin/user" \
--header "apikey: <ADMIN_API_KEY>"

**Windows PowerShell:**

curl.exe -sS --request GET `
--url "http://localhost:8008/admin/user" `
--header "apikey: <ADMIN_API_KEY>"

Replace `<ADMIN_API_KEY>` with your existing administrator API key.

Locate the original administrator account in the response and record its `name` value. This is the username used to sign in.

If you still know the password, you can use this username to sign in without completing the remaining recovery steps.

### [Step 2: Create a temporary administrator account](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-2-create-a-temporary-administrator-account)

Run the following request.

**Linux/macOS:**

curl -sS --request POST \
--url "http://localhost:8008/admin/user" \
--header "apikey: <ADMIN_API_KEY>" \
--header "Content-Type: application/json" \
--data '{
"name": "recovery_admin",
"display_name": "Recovery Administrator",
"email": "recovery@example.com",
"password": "<TEMPORARY_ADMIN_PASSWORD>",
"roles": ["1"],
"directory_id": 1
}'

**Windows PowerShell:**

$body = @'
{
"name": "recovery_admin",
"display_name": "Recovery Administrator",
"email": "recovery@example.com",
"password": "<TEMPORARY_ADMIN_PASSWORD>",
"roles": ["1"],
"directory_id": 1
}
'@
Invoke-RestMethod -Method Post -Uri "http://localhost:8008/admin/user" `
-Headers @{ apikey = "<ADMIN_API_KEY>" } `
-ContentType "application/json" `
-Body $body

Before running the request:

- Replace `<ADMIN_API_KEY>` with your existing administrator API key.
- Replace `<TEMPORARY_ADMIN_PASSWORD>` with a unique password that meets the configured password policy.
- Replace `recovery@example.com` with an appropriate administrator-controlled email address.
- Use a different temporary username if `recovery_admin` already exists.

Review the API response and confirm that the account was created successfully.

### [Step 3: Sign in using the temporary administrator](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-3-sign-in-using-the-temporary-administrator)

1. Open the MetaDefender Core Web Management Console.
2. Sign in using `recovery_admin` and the password specified in Step 2.
3. Navigate to **User Management > Users and groups**.

### [Step 4: Reset the original administrator’s password](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-4-reset-the-original-administrators-password)

1. Locate the original administrator account.
2. Click the three-dot menu next to the account and select **Reset password**.
3. Enter a new temporary password that meets the configured password policy.
4. Set **Reset type** to **Admin direct reset**.
5. Click **Reset** to apply the change.

### [Step 5: Sign in using the original administrator account](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-5-sign-in-using-the-original-administrator-account)

1. Sign out of the temporary administrator account.
2. Sign in using the original administrator username and the temporary password set in Step 4.
3. When prompted, change the temporary password to a new password.
4. Confirm that you can access the Web Management Console and administrator functions.

### [Step 6: Remove the temporary administrator account](/docs/mdcore/knowledge-base/how-to-recover-metadefender-core-administrator-access-using-an-e#step-6-remove-the-temporary-administrator-account)

After confirming that access to the original administrator account has been restored, delete `recovery_admin` from **User Management > Users and groups**.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
