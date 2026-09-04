<!-- source: https://www.opswat.com/docs/fenddiode/troubleshooting-and-support/diode-diagnostic-mode-and-the-fend-diagnostic-tool -->

# Diode Diagnostic Mode and the Fend Diagnostic Tool

Enabling diagnostic mode on the diode will allow the diode to publish error messages to a specified server on the outbound side and is recommended for use with the Fend Diagnostic Tool.

Diagnostic Mode was designed for use in troubleshooting installations and it is not generally recommended to be left on permanently, unless continuous logging is needed. The additional overhead associated with diagnostic mode may slow the performance/throughput of the diode in certain protocol modes. If continuous logging is not needed, turning off diagnostic mode may improve performance.

## [Downloading and Installing the Fend Diagnostic Tool](/docs/fenddiode/troubleshooting-and-support/diode-diagnostic-mode-and-the-fend-diagnostic-tool#downloading-and-installing-the-fend-diagnostic-tool)

Download the latest Fend Diagnostic Tool from <https://my.opswat.com>.

Log in using your OPSWAT account username and password. Go to “Product Downloads” and then to the Fend Data Diodes “Download” button. On the top tab, click on "Fend Supporting Utilities". Select your diode series and current firmware version, then download the Fend Diagnostic Tool installer.

Install the Fend Diagnostic Tool on a computer that will have access to the same network as the output side of the diode using the downloaded installer software. Follow the on-screen prompts to complete the installation. If this is the first time you have installed the Fend Diagnostic Tool, it may ask you to restart your computer.

## [Setting Up the Fend Diagnostic Tool to Receive Diagnostic Messages](/docs/fenddiode/troubleshooting-and-support/diode-diagnostic-mode-and-the-fend-diagnostic-tool#setting-up-the-fend-diagnostic-tool-to-receive-diagnostic-messages)

To set up the Fend Diagnostic Tool to listen for and receive diagnostic messages from the diode, do the following:

1. Ensure that tool is installed on a computer that is on the same network as the output side of the diode and that the diode is visible to the computer on the network
2. Open the Fend Diagnostic Tool.
3. From the “Host:” dropdown menu, select the IP you wish to use for the server
4. From the “Port:” menu, set the port to open for the server
5. Click “Listen” to start the server

   1. If this is the first time using this tool, your computer may ask to allow the program through the Windows firewall. Please select “Allow access” when prompted.
   2. If you do not receive this prompt, or hit cancel, you will need to manually add the program to the exceptions list in the Windows firewall.

6. Diagnostic messages from the diode will begin appearing in the “Input Side” or “Output Side” windows once the diode is set up in diagnostic mode.

## [Configuring a Diode for Diagnostic Mode](/docs/fenddiode/troubleshooting-and-support/diode-diagnostic-mode-and-the-fend-diagnostic-tool#configuring-a-diode-for-diagnostic-mode)

Using a web browser, log into the diode’s configuration settings.

1. Go to “System” -> “Diagnostics”
2. Set Mode to “On”
3. Set Level of Info to the desired level, “Errors” only is recommended to begin with. You can increase the verbosity (level of detail) as needed if the issue is not visible or solved with this setting.
4. Set the retry timer to the desired level, 60 seconds is recommended.
5. Set the Target Server IP Address to the IP address of the system running the Fend Diagnostic Tool as configured above.
6. Set the Target Server Port Number to the port set in the Fend Diagnostic Tool as configured above.

Click “Save and Exit” to close the configuration session and allow the diode to reboot. Allow the diode to return to operational mode. Diagnostic messages will be sent to the Fend Diagnostic Tool when/if they are generated. If the issue continues and messages generated are insufficient to diagnose the issue, repeat the steps above increasing the message verbosity.

Once an issue has been identified and fixed, log back into the diode Using the Fend Configuration Tool and turn diagnostic mode off by setting Mode to “Off”
