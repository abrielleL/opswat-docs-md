<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/smtp -->

# SMTP

In order to generate email reports, MetaDefender Storage Security needs to connect to an SMTP server. To configure this integration, please go to **Settings → SMTP**.

![](https://uploads.developerhub.io/prod/k8zL/ds1g6esuczq0utnluotzkd9a34z8hfhr4l817ovw6tj4bysysw80zdh6wtcifpei.png)

## Setup the integration

1. Enable SMTP by clicking the toggle
2. Input the **Host** address of your SMTP server (i.e [smtp.company.com](http://smtp.company.com))
3. Input the **Port** of your SMTP server
4. **Base URL**: the address to use in the email for links; this address should point to the MetaDefender Storage Security web interface
5. **Sender Email Address:** email address to be used as *From:* field when sending notifications (**Note:** if left empty, we will use the default email address: [*mdss@opswat.com*](mailto:mdss@opswat.com))
6. **Sender Name**: display name to be used as *From Name:* field when sending notifications (**Note:** if left empty, we will use the default sender name: *MetaDefender Storage Security*)
7. (Optionally) Input a **domain, username,** and **password** if your SMTP requires authentication
   1. You can leave these fields empty if your SMTP server does not require authentication
   2. You can leave the domain empty if your SMTP provider requires only a username and a password
8. Advanced Settings
   1. **Security option:** provides a way of specifying the SSL and/or TLS encryption that should be used for a connection. Please select one of the following options (**Note:** default option is None)
      1. **None:** No SSL or TLS encryption should be used
      2. **Auto:** Allow the system to decide which SSL or TLS options to use (default). If the server does not support SSL or TLS, then the connection will continue without any encryption
      3. **Connect using SSL or TLS immediately:** The connection should use SSL or TLS encryption immediately
      4. **Elevate the connection using StartTLS command:** Elevates the connection to use TLS encryption immediately after reading the greeting and capabilities of the server. If the server does not support the STARTTLS extension, then the connection will fail
      5. **Elevate the connection using StartTLS command if it is available:** Elevates the connection to use TLS encryption immediately after reading the greeting and capabilities of the server, but only if the server supports the STARTTLS extension
   2. **Ignore Certificate Warnings:** select this option if your SMTP does not have a valid certificate but wish to use SSL
9. **Save** your settings when you are done.

> **Info**
>
> In order to test the configuration, MetaDefender Storage Security will attempt to send a test email using the email address of the currently logged-in user. Please make sure that your account has a valid email configured.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
