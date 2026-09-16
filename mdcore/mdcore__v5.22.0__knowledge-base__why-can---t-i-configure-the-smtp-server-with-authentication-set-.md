<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-configure-the-smtp-server-with-authentication-set- -->

# Why can’t I configure the SMTP server with authentication set to “None” in MetaDefender Core 5.15.2?

This article is applied to MetaDefender Core deployments on Windows and Linux, version 5.15.2.

## [**Issue**](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-configure-the-smtp-server-with-authentication-set-#issue)

When configuring an SMTP server in **MetaDefender Core 5.15.2**, users may encounter an error if the authentication method is set to **None**.

**Sample error message in Core log:**

(common.workflow) Cannot login mail server with given options, id='lms::workflow::RestWorkflowExecutor(0x2b80c0a7f20, name = "WF-127.0.0.1:64159")', block='VerifyEmailBlock', error='Failed to send AUTH PLAIN command. Response code: 504' [msgid: 3523]

This issue affects **MetaDefender Core version 5.15.2** when setting up an email server with **Authentication Method: None**.

## [**Solution**](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-configure-the-smtp-server-with-authentication-set-#solution)

The issue was **addressed in MetaDefender Core version 5.16.0**. Please **upgrade to version 5.16.0 or later** to successfully configure SMTP servers using **Authentication Method: None**.

Note:

The issue **does not affect other SMTP authentication methods** such as **AUTH PLAIN** or **AUTH LOGIN**. If you are unable to schedule upgrade, you may use one of these authentication methods as a temporary workaround.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
