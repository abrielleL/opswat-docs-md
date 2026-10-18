<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-to-configure-smtp-server-on-metadefender-storage-security-to -->

# How to configure SMTP server on MetaDefender Storage Security to send notification to Gmail mailbox?

> **Check Your Product:**
>
> This article applies to MetaDefender Storage Security releases version 3.3.0 or newer   deployed on Windows or Linux systems.

To be able to send notification to your Gmail mailbox from MetaDefender Storage Security the following fields should be configured properly under MetaDefender Storage Security:

- HOST: smtp.gmail.com
- Port: 587
- Base URL: the address to use in the email for links; this address should point to the MetaDefender Storage Security web interface
- Sender email address (Optional): Ex.: [MDSS_no-reply@test.com](mailto:MDSS_no-reply@test.com)
- Sender name (Optional): Ex.: MDSS_No-Reply
- Username: username of the Gmail mailbox used for SMTP integration.
- Password: App password created for Gmail mailbox provided under “Email” field.
- Please choose a security option: Auto

In order to achieve that, the following configuration should be done on Gmail mailbox account:

1. Create App password for Gmail account

- Login to [https://myaccount.google.com/security](https://myaccount.google.com/security)
- Under "Signing in to Google":

![](https://uploads.developerhub.io/prod/k8zL/g1kqol4jyc1y6p2cfj843wnofn695wvstps4bbfgtld0ieyugn976bybgtkv4oqs.png)

- Click on Two-Step Verification
- Scroll down to section “App passwords” and click arrow in front of “App passwords”

![](https://uploads.developerhub.io/prod/k8zL/zk69nli2amqzdzp9987dw2gi8buismuz2p3k68g4i27xc54qloieszfix1q3h7vq.png)

- In new page opened, write a name for your App password and click “Creates”

![](https://uploads.developerhub.io/prod/k8zL/jwchqjqa60302wy16oeksazblgkumxy1h71fpa8rruago1rj4f3eqjnj7p6qwdme.png)

- Save the App password generated and click “Finished”. Further we will use the App password generated as password for mailbox used for MetaDefender Storage Security configuration as mentioned above and as in below example.

Example:

![](https://uploads.developerhub.io/prod/k8zL/4c5ktsqy2xbl3sf85lpnn14f06k8vzcsgul92li56vleuj8q4avzkmqdn14dp7sq.png)

IMPORTANT: For field “Password” use App password created under Gmail account and not use the password which you use to login on Gmail mailbox.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
