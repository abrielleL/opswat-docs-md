<!-- source: https://www.opswat.com/docs/fenddiode/troubleshooting-and-support/diode-syslog -->

# Diode Syslog

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Enabling syslog in your config will allow the diode to publish system logs to a specified server on the outbound side. Syslog data can be delivered to a remote server via either TCP or UDP. All Syslog traffic is sent from the output side of the diode. Meaning, the remote syslog server needs to be on the output sides network, or accessible through routing.

Syslog messages follow this specified format:

TIME DIODEIP [SIDE_OF_DIODE:APPLICATION] MESSAGE

2026-03-05T18:51:17-05:00 192.168.0.203 [Input: FTP] Server start success2026-03-05T18:51:18-05:00 192.168.0.203 [Output: SFTP] Sending event log
## [Configuring a Diode to Report Syslog](/docs/fenddiode/troubleshooting-and-support/diode-syslog#configuring-a-diode-to-report-syslog)

Using a web browser, log into the diode’s configuration settings.

1. Go to “System” -> “Remote Syslog”
2. Set Mode to “On”
3. Set Level of Info to the desired level, “Info” only is recommended to begin with. You can increase the verbosity (level of detail) as needed if the issue is not visible or solved with this setting.
4. Set the retry timer to the desired level. This simply determines how long between connection attempts the diode will wait.
5. Set the Target Server IP Address to the IP address of the system where you collect your logs. This should be an address accessible from the output side of the diode.
6. Set the Target Server Port Number to the port set in the Fend Diagnostic Tool as configured above.
7. The default transport mode for remote syslog is UDP, you can change it to TCP in the "Transport" dropdown.

Click “Save and Exit” to close the configuration session and allow the diode to reboot. Allow the diode to return to operational mode. Syslog will be sent to the remote server as it is generated. If you are troubleshooting an issue and the messages generated are insufficient to diagnose the issue, repeat the steps above increasing the message verbosity.

***For information on legacy diagnostics (for diodes using firmware versions <4.3.0), please see the appropriate version of the manual for your firmware. The image below indicates how to access legacy versions of this manual, by changing the version number in the upper-lefthand corner of the screen.***
