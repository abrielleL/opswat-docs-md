<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-test-sftp-connection-and-file-transfer-via-cli- -->

# How to test sftp connection and file transfer via CLI?

Summarize Page    Connect to Cursor Connect to VS Code Info:

This article provides steps to troubleshoot and further test SFTP file transfer.

Requirements:

- A sftp users credentials with permissions to read and/or write to the intended source/destination folder.
## [Testing Connection:](/docs/mdmft/knowledge-base/how-to-test-sftp-connection-and-file-transfer-via-cli-#testing-connection)

1. To test the connection to your SFTP server, please follow the syntax below:

HtmlCopysftp -P <PORT> [your_sftpuser]@[your_sftp_server_IP]

1. 1. **sftp** : sftp protocol/command
   2. **-P**: Port enabled for sftp connections on the SFTP server. By default this is 22.
   3. **your_sftpuser**: The sftp user that is allowed to establish connections.
   4. **your_sftp_server_IP**: destination SFTP server
2. If the connection is successful, you will get a prompt to enter your sftp user password.
3. If the connection is not successful, you can run the same command and add a `-v` flag before the port flag to obtain more debug information.

## [Testing File Transfer:](/docs/mdmft/knowledge-base/how-to-test-sftp-connection-and-file-transfer-via-cli-#testing-file-transfer)

To test the transfer of files you can:

1. Locate/Move to the destination/source folder of your remote machine. This will set the folder where you will uploading files from; or where you will be downloading files to.

HtmlCopysftp> lcd [DESTINATION_OR_SOURCE_FOLDER]

2. (Optional) Move to the source or destination of your local SFTP server:

HtmlCopysftp> cd [SFTP_FOLDER_PATH]

3. To upload files to your SFTP server:

HtmlCopysftp> put [Local_machine_filename] [DESTINATION_FOLDER_PATH]

4. To download files from your SFTP server:

HtmlCopysftp> get [filename_path_on_remote_SFTP_server]
## [Check Folder Permissions](/docs/mdmft/knowledge-base/how-to-test-sftp-connection-and-file-transfer-via-cli-#check-folder-permissions)

1. To check the permissions on a folder, you can run the command below from inside an sftp session

HtmlCopyls -alSupport:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
