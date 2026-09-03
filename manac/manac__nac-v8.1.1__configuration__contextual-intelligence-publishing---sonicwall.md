<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall -->

# Contextual Intelligence Publishing - SonicWALL

## [Overview](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#overview)

Using Contextual Intelligence Publisher (CIP), Single Sign-On can be enabled for SonicWALL and non-managed devices. Once configured, end users will no longer need to authenticate to SonicWALL since the user credentials will be passed transparently from CIP. Integrating the two allows seamless identity-aware firewalling and greater ease of use for matching firewall traffic to individual users. The CIP integration currently provides the following values to SonicWALL:

- Machine IP Address
- MAC Address
- Username

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to SonicWALL.

Prior to working through this document, SonicWALL and NAC must be installed and functional on the network. CIP must also be installed in the NAC system.

## [Configure SonicWALL](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#configure-sonicwall)

## [Configure LDAP](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#configure-ldap)

LDAP is required for SonicWALL to associate role information to user accounts that are published by CIP.

In the SonicWALL console, navigate to “Users > Settings”, select “LDAP” as the “User authentication method” and click “Configure LDAP…”.

In the pop-up windows, carefully input the information for your LDAP server. Ensure that all tabs are reviewed so that the most optimal configuration is present. When complete, test the configuration using the “Test” tab by entering a valid username and password.

When complete, click “OK” on the bottom of the page.

## [Configure RADIUS SSO](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#configure-radius-sso)

In the SonicWALL console, navigate to “Users > Settings” and click “Configure SSO…”.

In the pop-up window, choose the “Users” tab and ensure “Use LDAP to retrieve user group information” is selected.

In the pop-up window, choose the “RADIUS Accounting tab > General Settings tab” tab and ensure “Enable SSO by RADIUS accounting” is checked and the Port number is set to 1813.

In the pop-up window, choose the “RADIUS Accounting tab > Accounting Client tab” and click “Add…” to create a new RADIUS client.

In the “Settings” tab, enter the IP address of the NAC appliance (for cluster environments, enter the manager IP) and a shared secret that will be specific to this integration.

In the “RADIUS” tab, ensure “Log user out if no interim updates are received” is set to “Disabled”.

Click “OK” at the bottom of the window when completed.

## [Additional Settings](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#additional-settings)

In the SonicWALL console, navigate to “Users > Settings” and ensure the following items are configured:

- **User Authentication Settings > Case-sensitive user names**: unchecked

- **User Session Settings > Inactivity timeout (minutes):** This number should be set relatively high to prevent users from timing out prematurely. OPSWAT recommends starting at 720 and adjusting up or down as needed.

- **User Session Settings for SSO-Authenticated Users > On inactivity timeout make all users inactive instead of logging out:** Set this to true
- **User Session Settings for SSO-Authenticated Users > Age out inactive users after (minutes):** This number should be set relatively high to prevent users from timing out prematurely. OPSWAT recommends starting at 720 and adjusting up or down as needed.

When complete, click “Accept” at the top of the page.

## [Configure Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#configure-contextual-intelligence-publisher)

Once SonicWALL is configured, open the NAC Configuration at <https://auth.impulse.com:8443/ConnectUI> ([auth.impulse.com](http://auth.impulse.com) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence Publisher.” Click on “Add” and enter the following information:

- **Publisher:** RADIUS Accounting
- **Name:** A name to describe where CIP is publishing Data.
- **IP:** The IP of the SonicWALL appliance
- **Port:** RADIUS accounting port – the default of 1813 is recommended
- **Protocol:** UDP
- **Shared Secret:** The shared secret configured in SonicWALL.

Once everything is entered, click “Submit”. Once save, data will start being published to SonicWALL.

## [Verify Integration](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---sonicwall#verify-integration)

In the SonicWALL console, navigate to “Users > Status”. When the integration is fully configured, users will appear in “Active User Sessions” section of the status page with “Auth. By SSO/RADIUS Acct.” as the Type/Mode.
