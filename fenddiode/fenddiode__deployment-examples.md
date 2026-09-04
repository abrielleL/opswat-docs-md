<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples -->

# FTP and FTPS Examples

## [FTP and FTPS Local (On-Prem) Installations](/docs/fenddiode/deployment-examples#ftp-and-ftps-local-on-prem-installations)

### [FTP Buffered vs Streaming](/docs/fenddiode/deployment-examples#ftp-buffered-vs-streaming)

Fend Data Diodes have two modes of operation when it comes to FTP. These are named “Buffered” mode and “Streaming” mode.

- In buffered mode, the diode will accept an FTP connection, transfer the data internally to the output side, and wait for the file to be fully received before uploading that file to the destination FTP server. This offers greater stability in delivering a file as the output side maintains all of the file data internally until it is either uploaded successfully or the retry timer runs out. But comes with a limitation of file size, due to the diode storing the whole file at once, and speed, due to the need to space out large FTP transfers. (See [**Appendix I: Recommended Transfer Timings by Protocol**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol))
- In streaming mode, the output side will begin uploading FTP data to the destination FTP server as soon as it begins receiving a new file. This mode eliminates the file size limitation and the need to space out large FTP transfers, but more sensitive to network interruption. If the network connection is lost during a data transfer the file will be lost and the output side will not be able to retry the upload. In this case, once the network connection has been restored, an error log file will be uploaded detailing the time the event occurred, the name of the file, the directory it was destined for, and a description of the error.

If you are transferring small files (<60MB) and network stability is of concern, use buffered mode (Leave the setting “Streaming Enabled” unchecked). If you need to transfer large files, check the option for “Streaming Enabled”.

See [Diode Settings Overview -> Output Side -> FTP/FTPS](https://www.opswat.com/docs/fenddiode/configuration-settings/output-side-protocol-settings#ftp-client) for setting specifics.

### [Network/System Requirements](/docs/fenddiode/deployment-examples#networksystem-requirements)

For a diode to be installed in an FTP application, you must have a data source and destination that would, in the absence of a diode, be able to create an FTP client/server setup, with files being pushed from the client to the server. The diode can be placed in the middle to provide a physically-enforced one-way flow of files. The input side of the diode will act as an FTP server, connecting to the existing FTP client. The output side of the diode will act as an FTP client, connecting to the existing FTP server connection.

### [Setting up a new FTP client (data source)](/docs/fenddiode/deployment-examples#setting-up-a-new-ftp-client-data-source)

If you do not have an existing FTP client/server setup or your existing setup does not meet the requirements above, the following is the Fend recommended setup. The client side of this FTP arrangement will be responsible for sending files to the diode. The diode does not request files to be sent to it. An FTP client program will need to be selected. The Fend Data Diode has been tested and verified to work with the following FTP client/server software:

- Windows Native FTP
- Linux Native FTP
- WinSCP
- XLReporter
- CoreFTP
- FileZilla – Note: By default, FileZilla client is set to use multiple simultaneous data channels which is incompatible with Fend devices. Please see [Why am I having trouble sending a file with the FileZilla FTP Client?](https://www.opswat.com/docs/fenddiode/deployment-examples/ftp-and-ftps-examples#why-am-i-having-trouble-sending-a-file-with-the-filezilla-ftp-client) for more information on how to configure FileZilla client.

Configure the following settings in the FTP Client software of your choice on the data source machine:

- File protocol: FTP
- Encryption: No Encryption
- Host name: The static IP you assigned to the input side of the diode server
- Port number: 21
- Data channels: Single data channel
- Username and Password to match those on the input side of the diode server

For a list of FTP commands currently supported see [**Appendix II: List of Supported FTP Commands**](https://www.opswat.com/docs/fenddiode/appendices/appendix-ii-list-of-supported-ftp-commands)

### [Automating the FTP client](/docs/fenddiode/deployment-examples#automating-the-ftp-client)

It is also possible to script the sending of files from the FTP client to the diode. One example of this could be a file that is generated on a computer once a day needs to be sent to a server each night for storage or backup.

### [Directory/folder handling in FTP mode](/docs/fenddiode/deployment-examples#directoryfolder-handling-in-ftp-mode)

When transferring files through the diode and moving directories, all change directory (“cd” or “CWD”) commands will be sent to the output side FTP client and mimicked. So, if you need to move to a sub directory you simply change to that directory when communicating with the input side FTP server, and the output side client will make sure the file makes it to that directory.

To assist with this, a setting is available in the diode output side FTP client settings called “Relative Pathing Enabled”. When this setting enabled, all change directory requests will be assumed to be relative to the starting directory of the target FTP server when the diode output side FTP client logs in. This may be a user’s home directory (e.g. “/home/user/”) or it may be a virtual directory denoted as “/” or “Root”. In either case directory changes will be made relative to this folder. When this setting is disabled, a change directory request will be treated as an absolute path. Meaning, if you request to go to root or “/” the diode will attempt to go to the root of the system its logged into. This may be the root of a Linux filesystem, which will most likely be protected, or it could be the root of a virtual filesystem and allowed. Please use the appropriate setting for your environment.

### [Setting up a new FTP server (data destination)](/docs/fenddiode/deployment-examples#setting-up-a-new-ftp-server-data-destination)

The server side of this FTP setup will be responsible for receiving files from the diode. An FTP server program will need to be selected. The Fend Data Diode is compatible with the following FTP server software:

- Windows Native FTP
- Linux Native FTP
- WinSCP
- XLReporter
- CoreFTP
- FileZilla

First, create an account on the target FTP server. This will allow the diode to log into the server. Give the account a strong password and keep it safe. Next create a folder in the target FTP server. This folder will be where the diode sends its files. Lastly, configure the firewall on the FTP server computer to allow FTP traffic. Otherwise, no files will be received.

### [Setting up FTPS](/docs/fenddiode/deployment-examples#setting-up-ftps)

To add additional data security, you may wish to select FTPS mode. In order to use FTPS on the diode you will need a certificate and key pair. This pair will need to be used at each stage of the FTP transfer. Both the diode server (input side of the diode) and destination FTPS server need the certificate and the key. The diode client (output side of the diode) and the source FTPS client will need the certificate. To get a certificate key pair, you will need to generate them from your FTPS Server, or with a tool like OpenSSL.

#### [Generating a TLS Certificate and Key Pair](/docs/fenddiode/deployment-examples#generating-a-tls-certificate-and-key-pair)

The following example uses OpenSSL on Linux. The same commands can be used in any operating system using OpenSSL. To generate a private key and certificate for the input side diode TCP server perform the following 3 commands, replacing file names as desired.

Example 1Example 2Copyopenssl genpkey -algorithm RSA -out example.key
openssl req -new -key example.key -out csr.pem
openssl req -x509 -days 365 -key example.key -in csr.pem -out example.crt# Non-interactive and 10 years expiration
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"

The second command will prompt for a few questions, this information will be visible in the certificate generated. See below for a full example of the commands above.

To use the newly generated certificate and key pair in FileZilla Server see below.

### [Diode Settings for Local (On-Prem) FTP](/docs/fenddiode/deployment-examples#diode-settings-for-local-on-prem-ftp)

For an FTP use case, the input side of the diode will be configured as an FTP server, receiving existing connections (if any). The output side of the diode will be configured as an FTP client, potentially replacing an existing client and connecting to the FTP server. This allows the diode to be a “bump in the wire” for new and existing connections, with only minimal configuring for the latter.

#### [Configuring Diode FTP Input-Side Settings](/docs/fenddiode/deployment-examples#configuring-diode-ftp-input-side-settings)

On the main configuration screen there will be three columns, Input Side, System and Output Side. First, we will be configuring the input side.

1. Select “Ethernet” under Input Side -> Interface Settings

   1. Under DHCP Mode select “Static IP”
   2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
   3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.
2. Select “FTP Server” (or “FTPS Server”) from the dropdown under **Input Side -> Protocol Settings**. Enter the settings for the input side diode FTP server:

   1. Diode FTP Server Username: Set the username for the client to use to log in to the Diode FTP Server. Configure the FTP client to use this username.
   2. Diode FTP Server Password: Set the Diode FTP Server password. Configure the FTP client to use this password.
3. If you are using FTPS, navigate to the “Certificate” tab and click ‘Open’ to select the certificate file that you created earlier by extracting the Certificate from the Key Pair. Do the same for the Private Key.

#### [Configuring a Data Diode FTP Output-Side Settings](/docs/fenddiode/deployment-examples#configuring-a-data-diode-ftp-output-side-settings)

This process should be very similar to the input side of the diode. The output side of the diode will be configured as an FTP client, which needs to be provided with the credentials of the external FTP server. This includes its IP address and login information.

1. Select the “Ethernet” radio button under Output Side -> Interface Settings

   1. Under DHCP Mode select “Static IP”
   2. Set the Diode IP Address of the output side to ensure that it has a unique address on the network.
2. Select “FTP” (or “FTPS”) from the dropdown under Output Side -> Protocol Settings. Enter the settings required to connect to the external FTP server:

   1. Target FTP Server IP: Enter the IP address of the target server
   2. Target FTP Server Username: Enter the username configured in the FTP server
   3. Target FTP Server Password: Enter the password configured in the FTP server
   4. Data Mode: Set to Binary
   5. Data Socket Mode: Set to Passive
   6. Socket Timeout: Set to 20 seconds
   7. Retry Timer: Set to 5 minutes.
   8. Streaming Enabled: Enable streaming if you wish. For more info see: [FTP Buffered vs Streaming](https://www.opswat.com/docs/fenddiode/deployment-examples/ftp-and-ftps-examples#ftp-buffered-vs-streaming)
   9. Relative Pathing Enabled: With this option checked/enabled, all directory changes made during an FTP transfer will be assumed to be relative to the starting directory (e.g. “/home/pi”). If unchecked/disabled all directories will be treated as absolute.

3. If you are using FTPS, navigate to the “Certificate” tab and click ‘Open’ to select the certificate file that you created earlier by extracting the Certificate from the Key Pair.

4. Finally, when done updating all settings **press the “Save & Exit” button** located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples#installing-the-data-diode-after-configuration)

1. Connect the source network (the external FTP client) to the input side of the diode with an ethernet cable.
2. Connect the destination network (the external FTP server) to the output side of the diode with an ethernet cable.
3. Plug in the power supplies on both sides of the diode.
4. Confirm that files are transferring successfully.

Note: If you are having trouble receiving files on the destination FTP server and you have verified the diode configuration is correct, the first thing to check would be firewall settings. Windows firewall will block incoming FTP traffic by default, so make sure its set to allow this traffic.

## [FTP and FTPS Remote (Over the Internet) Port-Forwarding Installations](/docs/fenddiode/deployment-examples#ftp-and-ftps-remote-over-the-internet-port-forwarding-installations)

These instructions provide an overview of how to configure a diode for an internet-based FTP transfer to a remote location. For the basics of FTP/FTPS setup see [**FTP and FTPS Local (On-Prem) Installations**](https://www.opswat.com/docs/fenddiode/deployment-examples#ftp-and-ftps-local-on-prem-installations) then continue with the instructions below for remote FTP server targets.

### [Network/System Requirements](/docs/fenddiode/deployment-examples#networksystem-requirements)

For the diode to connect to an FTP server that is on another location or network it will need access from that location’s gateway. Usually, this means opening a port on the destination’s router. When the port is opened, it is also given explicit instructions of where to go in the local network to find its destination. If the destination is not set up to receive the connection, it will fail.

### [Setting up a Destination FTP Server](/docs/fenddiode/deployment-examples#setting-up-a-destination-ftp-server)

You will need a server username and password, along with permissions to write files to specified locations. The additional step for a remote setup is the specification of data channel ports or a port range. The example below uses FileZilla Server. For simplicity, it is configured so that the server only uses one port. In the example below, this port is 50,000, but you can use any acceptable FTP data port value. This port number assignment is very important for the port forwarding section that follows.

### [Port Forwarding](/docs/fenddiode/deployment-examples#port-forwarding)

This process can differ significantly depending on the router model being used and the overall IT environment; but generally, the steps are:

1. Log in to the network router and create two port forwarding listings. These will be for the two ports needed to perform FTP actions, namely:

   1. Command channel port 21 – This is the FTP command channel and must always be port 21
   2. Data channel port – This is the data channel you specified in the FTP server. In the example above, port 50000.
2. Add other information as needed for the port forwarding including, device IP (device running the FTP server) and what protocol to forward (TCP/UDP/Both).

### [Diode Settings for Remote FTP](/docs/fenddiode/deployment-examples#diode-settings-for-remote-ftp)

Follow the same instructions found in FTP and FTPS Local (On-Prem) Installations, but in addition to the following:

1. In the “Ethernet” settings under Output Side -> Interface Settings make sure the default gateway and subnet mask are set
2. In FTP Client settings under Output Side -> Protocol Settings, for the target Server IP address, use the external IP of the destination network.
3. Ensure the diode is on a network with access to the internet.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples#installing-the-data-diode-after-configuration)

1. Connect the source network (the FTP client) to the input side of the diode with an ethernet cable.
2. Connect the destination network with internet connectivity to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that files are transferring successfully.

## [FTP Frequently Asked Questions](/docs/fenddiode/deployment-examples#ftp-frequently-asked-questions)

### [What is the maximum transfer rate for FTP/FTPS?](/docs/fenddiode/deployment-examples#what-is-the-maximum-transfer-rate-for-ftpftps)

The maximum cross-diode transfer rate for FTP on 5-Series diodes (Models XE5, SE5, and CE5) is 5.0 Mbps. and on 15-Series diodes (Models XE15, SE15, and CE15) it is 15.0 Mbps. The maximum cross-diode transfer rate for FTPS is 4.0 Mbps.

### [What is the maximum file size that can be transferred over FTP/FTPS?](/docs/fenddiode/deployment-examples#what-is-the-maximum-file-size-that-can-be-transferred-over-ftpftps)

If you are using the streaming mode option, “Streaming Enabled” is checked, there is no file size limit.

If you are using buffered mode, “Streaming Enabled” is unchecked, the maximum file size is 60MB

### [Can you send multiple files concurrently to the input side of the diode?](/docs/fenddiode/deployment-examples#can-you-send-multiple-files-concurrently-to-the-input-side-of-the-diode)

No, the diode accepts one file at a time. A subsequent file can be sent after the current file transfer is complete.

### [Do I need to wait between sending files?](/docs/fenddiode/deployment-examples#do-i-need-to-wait-between-sending-files)

If you are using the streaming mode option, “Streaming Enabled” is checked, you do not need to wait between files.

If you are using buffered mode (“Streaming Enabled” is unchecked), you will need to pause between file transfers. Because the diode prevents any backward flow of data, the input side cannot see the status of the output side file transfer. To ensure that the current file has sufficient time to transfer to the target server on the output side in buffered mode, we recommend that timed delays be added between each file sent to the input side. For a table of recommended wait times between file transfers by file size, please see [**Appendix I: Recommended Transfer Timings by Protocol**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol)

### [How do I tell the diode to send a file to a specific destination directory on the target FTP server?](/docs/fenddiode/deployment-examples#how-do-i-tell-the-diode-to-send-a-file-to-a-specific-destination-directory-on-the-target-ftp-server)

By default, the diode will attempt to upload the file in the default directory for the target FTP server. If you wish to change that directory, you can send the change directory command to the input side of the diode to change to the desired working directory for that session. The working directory is not stored when a session is terminated. When a new FTP session is started, the diode will revert back to the default directory until a new change directory command is received. Commands sent to the input side of the diode are forwarded to the output side where they are received by the destination FTP server.

A setting is available in the diode output side FTP client settings called “Relative Pathing Enabled”. When this setting is enabled, all change directory requests will be assumed to be relative to the starting directory of the target FTP server. This may be a user’s home directory (e.g. “/home/user/”) or it may be a virtual directory denoted as “/” or “Root”. In either case directory changes will be made relative to this folder. When this setting is disabled, a change directory request will be treated as an absolute path. Meaning, if you request to go to root or “/” the diode will attempt to go to the root of the system its logged into. This may be the root of a Linux filesystem, which will most likely be protected, or it could be the root of a virtual filesystem and allowed. Please use the appropriate setting for your environment. For Linux users we recommend enabling relative pathing. For a full list of supported FTP commands please see [**Appendix II: List of Supported FTP Commands**](https://www.opswat.com/docs/fenddiode/appendices/appendix-ii-list-of-supported-ftp-commands).

### [After a file is transferred to the input side of the diode, can I “see” the file in the diode?](/docs/fenddiode/deployment-examples#after-a-file-is-transferred-to-the-input-side-of-the-diode-can-i-see-the-file-in-the-diode)

No, files that are transferred to the diode are not stored on the diode. All files are streamed real time through to the target FTP server on the output side network. The success of file transfer can be confirmed at the target FTP server on the output network.

### [After the file is transferred to the output side of the diode is the file deleted?](/docs/fenddiode/deployment-examples#after-the-file-is-transferred-to-the-output-side-of-the-diode-is-the-file-deleted)

Files are not permanently stored on the diode, only remaining in memory while the file is being transferred. Once the file is transferred, or after the retry timer has elapsed, the memory is cleared.

### [Can I send an entire folder full of files at once?](/docs/fenddiode/deployment-examples#can-i-send-an-entire-folder-full-of-files-at-once)

No, you cannot send a folder. You must send each file in the folder individually in sequence.

### [If both sides of the diode can either be configured as FTP or FTPS, what combinations of FTP and FTPS are allowed?](/docs/fenddiode/deployment-examples#if-both-sides-of-the-diode-can-either-be-configured-as-ftp-or-ftps-what-combinations-of-ftp-and-ftps-are-allowed)

If your diode is configured in buffered mode (the configuration option “Streaming Enabled” is unchecked), then any combination of FTP and FTPS is allowed.

If your diode is set to streaming mode, the configuration option “Streaming Enabled” is checked, only the configurations of FTP/FTPS->FTP and FTPS->FTPS are allowed.

### [What is the timeout for making FTP connections from the output side of the diode?](/docs/fenddiode/deployment-examples#what-is-the-timeout-for-making-ftp-connections-from-the-output-side-of-the-diode)

This setting can be changed by adjusting the “Socket Timeout” setting.

### [Is your FTPS protocol implicit or explicit?](/docs/fenddiode/deployment-examples#is-your-ftps-protocol-implicit-or-explicit)

Our diode supports both implicit and explicit FTPS. Please see [Diode Settings Overview](https://www.opswat.com/docs/fenddiode/configuration-settings) for more info.

### [When I connect with FTP, everything seems fine until I send a file, then I get a connection error, what is happening?](/docs/fenddiode/deployment-examples#when-i-connect-with-ftp-everything-seems-fine-until-i-send-a-file-then-i-get-a-connection-error-what-is-happening)

This is likely an issue with the FTP client attempting to establish multiple data channel connections simultaneously with the input side of the diode. Fend diodes support a single data channel connection at a time. Please make sure the FTP client is configured to use only one data channel connection.

### [Why am I having trouble sending a file with the FileZilla FTP Client?](/docs/fenddiode/deployment-examples#why-am-i-having-trouble-sending-a-file-with-the-filezilla-ftp-client)

The default settings with FileZilla are incompatible with our diode. FileZilla’s client will attempt to open multiple connections to the FTP Server to send multiple files concurrently. Our diode supports one FTP command and data channel connection at a time, so these default settings need to be changed. See instructions below for configuring FileZilla FTP Client to work with a Fend diode.

1. Go to Edit -> Settings

2. Select “Transfers” on the left column and make sure “Maximum Simultaneous Transfers” is set to 1.

3. Click “OK” to save those settings.
4. When connecting to the diode use the “Site Manager” tool.

5. Fill out the standard FTP info including Server IP, Username and Password.

6. Navigate to “Transfer Settings” and ensure “Limit number of simultaneous connections” is checked and the value is set to 1.

7. You will now be able to connect to the diode and send files as expected.
