<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/installation/wizard -->

# Wizard

When the installation is complete (for details see [Installation/Installation](/docs/mdemail/6.4.1/installation/installation)), MetaDefender Email Gateway Security icon is placed on your desktop.

The configuration wizard will guide you through the most important setup steps to have Email Gateway Security up and running. For a more comprehensive setup see Configuration section.

To proceed with the configuration wizard:

1. Double click Email Gateway Security icon on your desktop

2. The wizard gets started. The wizard language may be selected on the starting page

3. Accept the terms in the license agreement

4. Optionally activate the product (activation may be performed later, for details about activation see [Installation/Licensing](/docs/mdemail/6.4.1/installation/licensing)) Best is to activate online immediately directly in the wizard.

5. Set up and administrator account. This account will be the only one having access to the system initially.

5. Perform a basic (only the bare necessary settings) or advanced (some more options atop the necessary settings) configuration

## [Basic configuration](/docs/mdemail/6.4.1/installation/wizard#basic-configuration)

With basic configuration provide the SMTP server URI (mail server or email gateway) where emails will be forwarded after processing on Email Gateway Security

## [Advanced configuration](/docs/mdemail/6.4.1/installation/wizard#advanced-configuration)

1. Select deployment mode (for details see [Installation/Evaluation](/docs/mdemail/6.4.1/installation/evaluation))

1. Configure server profiles (for details see [Configuration/Server profiles](/docs/mdemail/6.4.1/configuration/server-profiles)):
2. Provide the SMTP server URI (mail server or email gateway) where emails will be forwarded after processing on Email Gateway Security
3. Enable or disable Zero-Day Malware Prevention (for details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy))
4. Enable or disable Proactive Data Loss Prevention (for details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy))
5. Provide the Active Directory server where users for licensing and groups for policy enforcement will be found

After the wizard has been completed, Email Gateway Security needs to be inserted into the email flow to do email processing (for details see [Installation/Insertion](/docs/mdemail/6.4.1/installation/insertion)).

Further reading

For further setup possibilities see Configuration section.
