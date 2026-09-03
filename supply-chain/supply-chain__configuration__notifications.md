<!-- source: https://www.opswat.com/docs/supply-chain/configuration/notifications -->

# Mail Notifications

> **Info**
>
> In order to send email notifications, make sure that an SMTP server is available.
>
> Please see [SMTP](https://www.opswat.com/docs/supply-chain/configuration/smtp) for more details.

Workflow can be configured to send email notifications as a remediaton for scan events via SMTP email to a list of email addresses. This can be done if MetaDefender Software Supply Chain has access to an SMTP server.

If no SMTP server is provided then the email notification option is disabled in the edit workflow diagram. (Read more about how to create a Workflow here: [Workflows](https://www.opswat.com/docs/supply-chain/configuration/workflow-creation))

If a SMTP server was registered then the user will have the following options:

![](https://uploads.developerhub.io/prod/jdK6/78k0cmzht4lckljiwhovnm2aeid73wkvtq3z457l13dahhs3itsa3grhpr9fqgcx.png)

Multiple email addresses can be introduced.

#### Email Report Example

An example email report for completed scan would look like this:

![](https://uploads.developerhub.io/prod/jdK6/xt7sayfde1k936ukjq2hfnd63m9ph575hrcx0r21a1ala6pv4f2nesp221k5nzl9.png)

> **Info**
>
> To ensure that scan reports are included as email attachments, the user must configure an API key in advance.
>
> Please see [Configuring an API Key](https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key) for more details.
