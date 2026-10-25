<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/installation/evaluation -->

# Evaluation

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Email Gateway Security is evaluation friendly. With its straightforward onboarding and intuitive user interface, PoC-ing the product is simpler than ever before.

## [Deployment modes](/docs/mdemail/6.4.2/installation/evaluation#deployment-modes)

Besides *protection mode* –that is to protect production environments, Email Gateway Security supports the following monitoring modes for evaluation purposes:

1. Out-of-band monitoring mode

2. Inline monitoring mode

## [SPAN/TAP support](/docs/mdemail/6.4.2/installation/evaluation#spantap-support)

Email Gateway Security can extract and process emails from SPAN mirrored or TAP monitored network traffic. Using this setup it is possible to evaluate the product under real production conditions but without affecting production performance or employee productivity.

## [Simple PoC environment](/docs/mdemail/6.4.2/installation/evaluation#simple-poc-environment)

It is simply possible to set up an evaluation environment on a standalone machine.

Limitations

A simple PoC environment is unable provide the performance and response times that a real production environment can.

### [Prerequisites](/docs/mdemail/6.4.2/installation/evaluation#prerequisites)

#### [Hardware](/docs/mdemail/6.4.2/installation/evaluation#hardware)

For a simple PoC environment any modern personal computer hardware should be adequate.

Virtualization

It is also possible to implement the simple PoC environment in a virtual machine.

The **benefit** is that the host operating system will be unchanged.

The **drawback** may be that the performance and response times will be even more poor.

#### [Software](/docs/mdemail/6.4.2/installation/evaluation#software)

|  |  |
| --- | --- |
| **Operating system** | For details, see [Installation/Prerequisites](/docs/mdemail/6.4.2/installation/prerequisites) |
| **Mail server** | [hMailServer](https://www.hmailserver.com/) |
| **Email client** | [Mozilla Thunderbird](https://www.thunderbird.net/) |

### [Architecture](/docs/mdemail/6.4.2/installation/evaluation#architecture)

### [Setup](/docs/mdemail/6.4.2/installation/evaluation#setup)

#### [hMailServer](/docs/mdemail/6.4.2/installation/evaluation#hmailserver)

1. [Download](https://www.hmailserver.com/download) and [install](https://www.hmailserver.com/documentation/v5.6/?page=howto_install) hMailServer with default settings
2. Start *hMailServer Administrator* to set up the mail server
3. Set up your test [domains and and accounts](https://www.hmailserver.com/documentation/v5.6/?page=basic_configuration)

   1. Select *Domains* and click *Add domain…* to create your domains

2. Select *Accounts* in your domains, and create your accounts

#### [Email Gateway Security](/docs/mdemail/6.4.2/installation/evaluation#email-gateway-security)

1. Install Email Gateway Security (for details see [Installation/Installation](/docs/mdemail/6.4.2/installation/installation))
2. Complete the Wizard, use default settings where possible (for details see [Installation/Wizard](/docs/mdemail/6.4.2/installation/wizard))
3. For the *SMTP server settings* specify hMailServer’s SMTP port, smtp://localhost:25

#### [Mozilla Thunderbird](/docs/mdemail/6.4.2/installation/evaluation#mozilla-thunderbird)

1. [Install](https://support.mozilla.org/en-US/kb/installing-thunderbird-windows) and start Mozilla Thunderbird
2. Add your email accounts created in *hMailServer / 3 / b* section in this article

Apply the following settings:

| Direction | Protocol | Server hostname | Port |
| --- | --- | --- | --- |
| Incoming | IMAP | localhost | 143 |
| Outgoing | SMTP | localhost | 10025 |
