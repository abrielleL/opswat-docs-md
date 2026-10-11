<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/installation/post-installation-configuration -->

# Setup Wizard - Post-Installation Configuration

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Post-installation configuration optimizes system functionality by allowing administrators to customize settings, configure security, and establish integrations.

## [Setup Wizard](/docs/mdmft/v3.11.5/installation/post-installation-configuration#setup-wizard)

The Setup Wizard is designed to guide you through the essential initial configurations required to start using MetaDefender Managed File Transfer™. The wizard ensures your application is properly set up while offering you the flexibility to skip non-essential steps if needed.

Info

Until the setup is complete, you can only access MetaDefender Managed File Transfer™ from a browser running on the same computer it was installed on.

### [Key Features of the Setup Wizard:](/docs/mdmft/v3.11.5/installation/post-installation-configuration#key-features-of-the-setup-wizard)

- Mandatory Steps: Ensure the application is ready for use.
- Skippable Steps: Provide a helpful overview of important configurations that can be revisited later.
- Final Overview: Review the status of all steps to confirm successful setup.
- Resume Work: Pick up where you left off and continue the setup.

### [Steps Overview](/docs/mdmft/v3.11.5/installation/post-installation-configuration#steps-overview)

- Welcome Step
- Encryption Key (Mandatory)
- First Admin Account (Mandatory)
- License Activation Method Chooser (Skippable)
- License Activation (Skippable)
- SMTP Server Configuration (Skippable)
- Server Configuration (Skippable)
- HTTPS Configuration (Skippable)
- Finish/Apply Configurations Step

#### [Welcome Step](/docs/mdmft/v3.11.5/installation/post-installation-configuration#welcome-step)

Welcome screen for MetaDefender Managed File Transfer™ after successfully completing the Install Wizard. The administrator can optionally adjust the application's default language.

#### [1. Encryption Key Setup](/docs/mdmft/v3.11.5/installation/post-installation-configuration#1-encryption-key-setup)

A mandatory step, where you will be provided with a unique encryption key. Copy and store this key securely, as it will be displayed only once during this process.

#### [2. First Admin Account](/docs/mdmft/v3.11.5/installation/post-installation-configuration#2-first-admin-account)

It is a mandatory step, where you have to create the primary an administrator account.

#### [3. License Activation Method Chooser](/docs/mdmft/v3.11.5/installation/post-installation-configuration#3-license-activation-method-chooser)

Select how to activation your MetaDefender Managed File Transfer™ license. Options include:

- Online: Activate your license key through Internet
- Offline: Activate the product via a license file
- Request Trial License: You do not posses a license for MetaDefender Managed File Transfer™ yet, request it from customer support.

Request Trial License will take you to OPSWAT's Customer Support page.

Skipping this step will bypass the next license activation step.

#### [4. License Activation](/docs/mdmft/v3.11.5/installation/post-installation-configuration#4-license-activation)

Activate your license based on the chosen method in the previous step. Follow the on-screen instructions for your selected method.

Online activation

Offline activation

#### [6. SMTP Server Configuration](/docs/mdmft/v3.11.5/installation/post-installation-configuration#6-smtp-server-configuration)

Integrate with your SMTP server / Microsoft Graph API to receive email notifications.

#### [7. Server Configuration](/docs/mdmft/v3.11.5/installation/post-installation-configuration#7-server-configuration)

Set up webserver details like host, port, and rate-limiting.

#### [8. HTTPS Configuration](/docs/mdmft/v3.11.5/installation/post-installation-configuration#8-https-configuration)

Use an SSL certificate to enable secure HTTPS communication.

Info

To use a Certificate, it has to be present on the host machine, where MetaDefender Managed File Transfer™ is running.

Info

When no TLS version is chosen, then the highest version available will be used.

#### [Finish/Apply Configurations Step](/docs/mdmft/v3.11.5/installation/post-installation-configuration#finishapply-configurations-step)

Every configured setting will be applied in sequence.

Outcomes

- Error: The configuration couldn't be applied, manually go back to examine the error and adjust the configuration or skip the step to finish the setup.
- Skipped: The step was skipped before, not action neeeded.
- Success: The application is ready to be used. The user will redirected to the login page after 15 seconds elapsed or can go there directly with the button.

Info

If either server or HTTPS configuration has changed, then the webserver will be restarted and the user will be redirected to the login page.

SMTP Server Setup failed with an issue

Configuration finished with skipping SMTP step
