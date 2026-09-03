<!-- source: https://www.opswat.com/docs/cm/configurations/email-server -->

# Email Server

This section guides you steps to configure an SMTP server to allow My OPSWAT Central Management to send email alerts and notifications.

**Steps:**

- Go to **Settings > Servers > Email Server**.
- Check the option **"Enable SMTP Server"**.
- Fill the **required** fields

![](https://uploads.developerhub.io/prod/97qW/8znechfrwzqqvu24fbozkamsj3goiivlqwwsayt2az7tzjhc658w04e3lqw5zh0a.png)

| **Field** | **Description** |
| ---- | ---- |
| **Send From Email** | The email address used to send emails. Example: `test@gmail.com` |
| **SMTP Server** | The address of the SMTP server. Example: `smtp.gmail.com` |
| **Port** | The port used for the SMTP connection. Common Gmail SMTP port: `587` |
| **Connection Security** | The security protocol used for email transmission. Select: **None** &#124; **StartTLS** &#124; `**TLS**` |
| **Authentication Method** | The method used to authenticate the SMTP server. Select: **None** &#124;`**Login**` |
| **Username** | The account name (usually the same as the sender email). |
| **Password** | The application-specific password or account password (hidden for security). |

- Click **Save**
