<!-- source: https://www.opswat.com/docs/mdemail/configuration/trustedsenders -->

# Trusted senders

MetaDefender Email Gateway Security supports a global trusted senders list. This list can be used to bypass Anti-Spam and Anti-Phishing checks for emails sent from specific IP addresses/ranges and/or senders.

## [Overview](/docs/mdemail/configuration/trustedsenders#overview)

The Trusted Senders is available by navigating to **Settings > Trusted senders**.

## [Adding trusted sender entries](/docs/mdemail/configuration/trustedsenders#adding-trusted-sender-entries)

### [IP address](/docs/mdemail/configuration/trustedsenders#ip-address)

To trust a specific IP address, click on the 'Add sender IP address to filter' option and specify the IP (v4 or v6) address and click 'Save' to store the changes. Any emails from that specific address will bypass any anti-spam/anti-phishing checks in MetaDefender Email Gateway Security.

### [IP range](/docs/mdemail/configuration/trustedsenders#ip-range)

To block CIDR IP address range, click on the 'Add sender IP address to filter' option and specify the range, for example: 192.168.129.23/17 and click 'Save' to store the changes.

### [Sender email address](/docs/mdemail/configuration/trustedsenders#sender-email-address)

Trusting a specific sender (SMTP *MAIL FROM* or email header *From*) is done by clicking on 'Add sender domain or address filter' and specifying the address to be trusted. Please note that a Regular Expression can also be used to trust multiple addresses with a single filter entry. If a regular expression is used as value, make sure to change the drop-down value to 'Regex'

### [Sender email domain](/docs/mdemail/configuration/trustedsenders#sender-email-domain)

To trust emails from a specific sender domain (SMTP *MAIL FROM* or email header *From*), simply specify the email domain to be trusted. If using a Regular Expression to define a domain filter, make sure to select 'Regex' in the drop-down to the right of the value entered.

Identify a trusted sender email

Any email received from a trusted sender will have a check-mark next to it in the Email History / Quarantine:

### [Importing from CSV](/docs/mdemail/configuration/trustedsenders#importing-from-csv)

Entries can be imported from comma separated value (CSV) files. The values imported from a file are added only on the GUI, ignoring values that already have an entry.

Valid syntax

Due to technical limitations, lines in CSV files must be with the following syntax:

**Sender IP address filter**

`"<IP address>","Ip","Global","false",""`

**Sender domain or address filter**

*Global entries*

`"<sender email address>","Email","Global","<whether field is regex: Normal:false; RegEx: true>",""`

*User entries*

"<sender email address>","Email","User","<whether field is regex: Normal:false; RegEx: true>","<user email address>"__

### [Exporting to CSV](/docs/mdemail/configuration/trustedsenders#exporting-to-csv)

Visible values are exported

The values exported to a CSV file export only what is visible on the GUI. The export ignores what values are actually present in the database in case the modifications have not been saved yet.

### [Allow Trusted senders for specific recipients](/docs/mdemail/configuration/trustedsenders#allow-trusted-senders-for-specific-recipients)

To trust emails between specific people, specify the email sender to be trusted and switch the filter type from `Global` to `User`.

### [Trusting senders from the Email History](/docs/mdemail/configuration/trustedsenders#trusting-senders-from-the-email-history)

It is supported to trust a sender based on the details of an email in the Email History.

For details see [Email History](/docs/mdemail/operating/email-history).
