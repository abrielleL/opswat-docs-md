<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/blocklist -->

# Blocklist

MetaDefender Email Gateway Security supports a global IP address & sender email blocklist. This list can be used to prevent specific IP addresses/ranges and/or senders to submit emails for processing.

## [Overview](/docs/mdemail/6.4.1/configuration/blocklist#overview)

The Blocklist is available by navigating to **Settings > Blocklist**.

Refused emails

Emails rejected by the Blocklist can be found among the refused emails in [Audit > Refused Emails](/docs/mdemail/6.4.1/operating/refused-emails).

## [Adding blocklist entries](/docs/mdemail/6.4.1/configuration/blocklist#adding-blocklist-entries)

### [Block IP address](/docs/mdemail/6.4.1/configuration/blocklist#block-ip-address)

To block a specific IP address, click on the 'Add sender IP address to filter' option and specify the IP (v4 or v6) address and click 'Save' to store the changes. Any attempt to send emails from that specific address will be rejected by MetaDefender Email Gateway Security.

### [Block IP range](/docs/mdemail/6.4.1/configuration/blocklist#block-ip-range)

To block CIDR IP address range, click on the 'Add sender IP address to filter' option and specify the range, for example: 192.168.129.23/17 and click 'Save' to store the changes.

### [Block sender email address](/docs/mdemail/6.4.1/configuration/blocklist#block-sender-email-address)

Blocking a specific sender is done by clicking on 'Add sender domain or address filter' and specifying the address to be blocked. Please note that a Regular Expression can also be used to block multiple addresses with a single filter entry. If a regular expression is used as value, make sure to change the drop-down value to 'Regex'

### [Block sender email domain](/docs/mdemail/6.4.1/configuration/blocklist#block-sender-email-domain)

To block a specific sender domain, simply specify the email domain to be blocked. If using a Regular Expression to define a domain filter, make sure to select 'Regex' in the drop-down to the right of the value entered.

### [Importing from CSV](/docs/mdemail/6.4.1/configuration/blocklist#importing-from-csv)

Entries can be imported from comma separated value (CSV) files. The values imported from a file are added only on the GUI, ignoring values that already have an entry.

Valid syntax

Due to technical limitations, lines in CSV files must be with the following syntax:

**Sender IP address filter**

`"<IP address>","Ip","false"`

**Sender domain or address filter**

`"<sender email address or domain>","Email","<whether field is regex: Normal:false; RegEx: true>"`

example:

`"opswat.com","Email","false"`

`"evil.+\.com","Email","true"`

### [Exporting to CSV](/docs/mdemail/6.4.1/configuration/blocklist#exporting-to-csv)

Visible values are exported

The values exported to a CSV file export only what is visible on the GUI. The export ignores what values are actually present in the database in case the modifications have not been saved yet.

## [Blocklist response](/docs/mdemail/6.4.1/configuration/blocklist#blocklist-response)

Any blocklisted clients attempting to send emails to MetaDefender Email Gateway Security will receive the following SMTP response:

**IP addresses/ranges:** 550 IP address '1.2.3.4', is blocklisted, rejecting

**Email addresses/domain:** 550 Email address 'spammer@organization.com', is blocklisted, rejecting
