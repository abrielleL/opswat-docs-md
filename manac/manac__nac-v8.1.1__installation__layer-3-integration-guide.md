<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide -->

# Layer 3 Integration Guide

Learn the steps required to integrate NAC into a customer Layer 3 network environment and validate the integration with a test policy. Note that this page only provides the minimum requirements needed to achieve network integration.

## [Add a Layer 3 switch/router to NAC](/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide#add-a-layer-3-switchrouter-to-nac)

To access the NAC UI, navigate to the link below and login with NAC Admin credentials (admin/admin is the default username and password). <https://x.x.x.x:8443/manage>

Once logged into the NAC UI, the network integration options are located under Configuration Manager.

Once logged into Configuration Manager, click on Routers/Switches under Enforcement Setup in the left pane.

In the right pane, click on the New Connection button.

Click on the edit button to enter a Label, Description, IP address and credentials for NAC to login to the router. For the “Enforcer” field, select your system’s IP address from the drop down list.

Info
#### [Optional Fields if Full Configuration Access is Default](/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide#optional-fields-if-full-configuration-access-is-default)

The Configuration Prompt fields and second set of passwords are only required if a network admin has to type “enable” and a second password to login. If full configuration access is enabled by default with the credentials entered, then those three fields must be blank. After the credentials have been entered, select the appropriate vendor from the Connection Type drop down list. If an Exit Delay or Measured Commit option is available, it is recommended to select that option for optimum performance.

## [Verify NAC/Router Connection](/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide#verify-nacrouter-connection)

To verify the connection, click the Verify Connectivity and Configuration button. The text box should display a successful login and the addition of a test IP to the configuration.

If there is no output or an error message indicating “No router is open for this IP”, double check for access-lists (including VTY ACLs), firewall rules or other issues that would prevent the NAC system IP from connecting to the router. A manual connection attempt using a terminal emulator is also a valuable tool when troubleshooting issues specifically related to credentials. After a successful test, change the connection state to Enabled and click Save changes.

Once enabled, the connection should display a green checkmark.

## [Apply NAC script to Layer 3 switch/router](/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide#apply-nac-script-to-layer-3-switchrouter)

Now that the Layer 3 switch/router has been added to NAC and connectivity from NAC to the router has been verified, a script must be applied to the switch/router to complete the integration setup.

Example scripts are provided on [Layer 3 Integration Scripts](/docs/manac/nac-v8.1.1/metadefender-nac/nac-v8.1.0/installation/layer-3-integration-guide). The scripts are designed to be cut and paste. Locate the appropriate script for the make/model, fill in the variables in the script with the appropriate information and apply the script.

Success

This concludes the steps required for Layer 3 integration. To test the integration, proceed to the [Configure Identity for Unmanaged Devices](/docs/manac/nac-v8.1.1/installation/configure-identity-for-unmanaged-devices) section.
