<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/configuration/smtp-connector -->

# SMTP Connector

The SMTP Connector allows you to transfer SMTP data unilaterally across Security Gateway. There is a built in SMTP server in Security Gateway BLUE that will receive mail from SMTP clients in the BLUE network. SMTP traffic will be transferred from Security Gateway BLUE to Security Gateway RED, where we will configure a built in SMTP client that will send the traffic to a SMTP server in RED network.

### [Security Gateway BLUE](/docs/netwall/v5.13.2/configuration/smtp-connector#security-gateway-blue)

Important

To configure SMTP Connector, a security dongle should be inserted in the BLUE server.

To configure SMTP server in BLUE MetaDefender Security Gateway, click on SMTP option in the menu, click on Edit button and fill in the fields:

- Connection Security, you can choose the security level for the communications between clients and server in BLUE:

  - None: No security added.
  - STARTTLS: STARTTLS security, a new field will appear so you can add the certificate.
  - SSL/TLS: SSL/TLS security, a new field will appear so you can add the certificate.
- Port: Port is automatically populated depending on the Security you have selected. You can change the selection if you want to operate in a non-default port.
- Certificate: If you select STARTTLS or SSL/TLS in Connection Security, you need to include a certificate. Available certificates will be listed in the dropdown list. You can add new certificate or import them into MetaDefender Security Gateway in Advanced > Encryption > SSL/TLS credentials. Check [Advanced menu](/docs/netwall/v5.13.2/configuration/advanced-menu) for more details.
- Enabled: Tick this checkbox to enable SMTP Transfer

### [Security Gateway RED](/docs/netwall/v5.13.2/configuration/smtp-connector#security-gateway-red)

Important

To configure SMTP Connector, a security dongle should be inserted in the RED server.

To configure SMTP server in RED MetaDefender Security Gateway, click on SMTP option in the menu, click on Edit button and fill in the fields:

- Connection Security, you can choose the security level for the communications between MetaDefender Security Gateway RED SMTP client and the server:

  - None: No security added.
  - STARTTLS: STARTTLS security.
  - SSL/TLS: SSL/TLS security, a new field will appear so you can add the certificate.
- Mail Server IP: IP for the mail server configured in RED side where MetaDefender Security Gateway will transfer the SMTP traffic comming from BLUE.
- Certificate: If you select SSL/TLS in Connection Security, you need to include a certificate. Available certificates will be listed in the dropdown list. You can add new certificate or import them into MetaDefender Security Gateway in Advanced > Encryption > x509 Certificates. Check [Advanced menu](/docs/netwall/v5.13.2/configuration/advanced-menu) for more details.
- Enabled: Tick this checkbox to enable SMTP Transfer
