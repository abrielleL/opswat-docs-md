<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/sftp-examples -->

# SFTP Examples

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [SFTP Buffered vs Streaming](/docs/fenddiode/deployment-examples/sftp-examples#sftp-buffered-vs-streaming)

SFTP has two modes of operation named “Buffered” mode and “Streaming” mode.

- In buffered mode, the diode will accept an SFTP connection, transfer the data internally to the output side, and wait for the file to be fully received before uploading that file to the destination SFTP server. This offers greater stability in delivering a file as the output side maintains all of the file data internally until it is either uploaded successfully or the retry timer runs out. But it comes with a limitation of file size, due to the diode storing the whole file at once, and speed, due to the need to space out large SFTP transfers. (See [**Appendix I: Recommended Transfer Timings by Protocol**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol))
- In streaming mode, the output side will begin uploading data to the destination SFTP server as soon as it begins receiving a new file. This mode eliminates the file size limitation and the need to wait between SFTP transfers but is more sensitive to network interruption. If the network connection is lost during a data transfer the file will be lost and the output side will not be able to retry the upload. In this case, once the network connection has been restored, an error log file will be uploaded detailing the time the event occurred, the name of the file, the directory it was destined for, and a description of the error.

If you are transferring small files (<60MB) and network stability is of concern, use buffered mode (Leave the setting “Streaming Enabled” unchecked). If you need to transfer large files, check the option for “Streaming Enabled”.

See [**Diode Settings Overview -> Output Side -> SFTP Client**](https://www.opswat.com/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-client) for setting specifics.

## [Network/System Requirements](/docs/fenddiode/deployment-examples/sftp-examples#networksystem-requirements)

For a diode to be installed in an SFTP application, you must have a data source and destination that would, in the absence of a diode, be able to create an SFTP client/server setup, with files being pushed from the client to the server. The diode can be placed in the middle to provide a physically-enforced one-way flow of files. The input side of the diode will act as an SFTP server, connecting to the existing SFTP client. The output side of the diode will act as an SFTP client, connecting to the existing SFTP server connection.

## [Setting up a new SFTP client (data source)](/docs/fenddiode/deployment-examples/sftp-examples#setting-up-a-new-sftp-client-data-source)

If you do not have an existing SFTP client/server setup or your existing setup does not meet the requirements above, the following is the Fend recommended setup. The client side of this SFTP arrangement will be responsible for sending files to the diode. The diode does not request files to be sent to it. An SFTP client program will need to be selected. The Fend Data Diode has been tested and verified to work with the following SFTP client/server software:

- Windows Native SFTP
- Linux Native SFTP
- WinSCP

Configure the following settings in the SFTP Client software of your choice on the data source machine:

- File protocol: SFTP
- Host name: The static IP you assigned to the input side of the diode
- Username and Password to match those on the didoes input side server

For a list of SFTP commands currently supported see [**Appendix II: List of Supported FTP Commands**](https://www.opswat.com/docs/fenddiode/appendices/appendix-ii-list-of-supported-ftp-commands)

## [Automating the SFTP client](/docs/fenddiode/deployment-examples/sftp-examples#automating-the-sftp-client)

It is also possible to script the sending of files from the SFTP client to the diode. One example of this could be a file that is generated on a computer once a day needs to be sent to a server each night for storage or backup.

## [Directory/folder handling in SFTP mode](/docs/fenddiode/deployment-examples/sftp-examples#directoryfolder-handling-in-sftp-mode)

When transferring files through the diode and moving directories, all change directory (“cd” or “CWD”) commands will be sent to the output side SFTP client and mimicked. So, if you need to move to a sub directory you simply change to that directory when communicating with the input side SFTP server, and the output side client will make sure the file makes it to that directory.

To assist with this, a setting is available in the diode output side FTP client settings called “Relative Pathing Enabled”. When this setting enabled, all change directory requests will be assumed to be relative to the starting directory of the target FTP server when the diode output side FTP client logs in. This may be a user’s home directory (e.g. “/home/user/”) or it may be a virtual directory denoted as “/” or “Root”. In either case directory changes will be made relative to this folder. When this setting is disabled, a change directory request will be treated as an absolute path. Meaning, if you request to go to root or “/” the diode will attempt to go to the root of the system its logged into. This may be the root of a Linux filesystem, which will most likely be protected, or it could be the root of a virtual filesystem and allowed. Please use the appropriate setting for your environment.

## [Setting up a new SFTP server (data destination)](/docs/fenddiode/deployment-examples/sftp-examples#setting-up-a-new-sftp-server-data-destination)

The server side of this SFTP setup will be responsible for receiving files from the diode. An SFTP server program will need to be selected. The Fend Data Diode has been tested and verified to work with the following SFTP server software:

- OpenSSH server for Windows and Linux

For instructions on how to set up OpenSSH for Windows please refer to [this detailed guide from WinSCP.](https://winscp.net/eng/docs/guide_windows_openssh_server)

## [Diode Settings for Local (On-Prem) SFTP](/docs/fenddiode/deployment-examples/sftp-examples#diode-settings-for-local-on-prem-sftp)

For an SFTP use case, the input side of the diode will be configured as an SFTP server, receiving existing connections (if any). The output side of the diode will be configured as an SFTP client, potentially replacing an existing client and connecting to the SFTP server. This allows the diode to be a “bump in the wire” for new and existing connections, with only minimal configuring for the latter.

### [Configuring Diode SFTP Input-Side Settings](/docs/fenddiode/deployment-examples/sftp-examples#configuring-diode-sftp-input-side-settings)

On the main configuration screen there will be three columns, Input Side, System and Output Side. First, configure the input side.

1. Select “Ethernet” under Input Side -> Interface Settings

   1. Under DHCP Mode select “Static IP”
   2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
   3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.
2. Select “SFTP” from the dropdown under Input Side -> Protocol Settings. Enter the settings for the input side diode SFTP server:

   1. Authentication Mode: Select which Authentication mode should be used for the input side SFTP server.
   2. Diode SFTP Server Username: Set the username for the client to use to log in to the Diode SFTP Server. Configure the SFTP client to use this username.
   3. Diode SFTP Server Password: Set the Diode SFTP Server password. Configure the SFTP client to use this password.
   4. Private Host Key: Upload a Private Key from an SSH Private/Public Key pair.
   5. Public Host Key: Upload a Public Key from an SSH Private/Public Key pair.
   6. Public Auth Key: Upload a Public Key from an SSH Private/Public Key pair.

### [Configuring a Data Diode SFTP Output-Side Settings](/docs/fenddiode/deployment-examples/sftp-examples#configuring-a-data-diode-sftp-output-side-settings)

This process should be very similar to the input side of the diode. The output side of the diode will be configured as an SFTP client, which needs to be provided with the credentials of the external SFTP server. This includes its IP address and login information.

1. Select the “Ethernet” radio button under Output Side -> Interface Settings

   1. Under DHCP Mode select “Static IP”
   2. Set the Diode IP Address of the output side to ensure that it has a unique address on the network.
2. Select “SFTP” from the dropdown under Output Side -> Protocol Settings. Enter the settings required to connect to the external SFTP server:

   1. Target SFTP Server Address: Enter the IP address or URL of the target server
   2. Authentication Mode: Select which Authentication mode should be used for the input side SFTP server.
   3. Target SFTP Server Username: Enter the username configured in the SFTP server
   4. Target SFTP Server Password: Enter the password configured in the SFTP server
   5. Retry Timer: Set to 5 minutes.
   6. Log File Save Directory: Choose a directory to save error logs too. (Optional)
   7. Log File Enabled: Enable or disable logs as needed.
   8. Streaming Enabled: Enable streaming if you wish. For more info see: [**SFTP Buffered vs Streaming**](https://www.opswat.com/docs/fenddiode/deployment-examples/sftp-examples#sftp-buffered-vs-streaming)
   9. Relative Pathing Enabled: With this option checked/enabled, all directory changes made during an SFTP transfer will be assumed to be relative to the starting directory (e.g. “/home/pi”). If unchecked/disabled all directories will be treated as absolute.
   10. Private Auth Key: Upload a Private Key from an SSH Private/Public Key pair.
   11. Public Auth Key: Upload a Public Key from an SSH Private/Public Key pair.
   12. Public Host Key: Upload a Public Key from an SSH Private/Public Key pair.

## [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/sftp-examples#installing-the-data-diode-after-configuration)

1. Connect the source network (the external SFTP client) to the input side of the diode with an ethernet cable.
2. Connect the destination network (the external SFTP server) to the output side of the diode with an ethernet cable.
3. Plug in the power supplies on both sides of the diode.
4. Confirm that files are transferring successfully.

Note: If you are having trouble receiving files on the destination SFTP server and you have verified the diode configuration is correct, the first thing to check would be firewall settings. Windows firewall will block incoming SFTP traffic by default, so make sure it’s set to allow this traffic.
