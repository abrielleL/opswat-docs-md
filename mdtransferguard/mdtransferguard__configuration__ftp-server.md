<!-- source: https://www.opswat.com/docs/mdtransferguard/configuration/ftp-server -->

# FTP Server

The FTP Server Connector allows the user to configure a built-in FTP Server on both the BLUE and RED sides. It provide flexibility on how FTP transfers work, transferring files from the BLUE side ( using a flanker or the built-in FTP server) to the RED side (using a flanker or the built in FTP server).

Important

For this feature the user must configure the corresponding FTP File Transfer on both sides, BLUE and RED.

FTP Server Connector supports FTP, FTPS and FTPES.

A total of 20 simultaneous FTP sessions can be configured, one per Virtual User created within the FTP Server.

## [Diode X BLUE](/docs/mdtransferguard/configuration/ftp-server#diode-x-blue)

### [FTP Server Configuration](/docs/mdtransferguard/configuration/ftp-server#ftp-server-configuration)

Important

To configure the FTP Server Connector, a security dongle must be inserted in the BLUE server.

Login into MetaDefender Diode X BLUE. If the FTP Server hasn't been previously configured the user will see an Edit button to include a new FTP Server. This feature requires that the user reserve disk space to allow it to act as a FTP Server. Once the Edit button is pushed the user will be notified via the message bellow.

Once required disk space has been reserved the user should input the following information.

1. Type or select values in the following boxes:

   1. **Allowed Source IPs or Ranges:** List of IP addresses allowed to connect to the FTP Server. User can enter several addresses or ranges separated by semicolon. Empty field means ANY IP will be allowed to connect.
   2. **Passive Min Port:** Minimum port number that the FTP Server will use in passive mode. Range from 1024 to 65535.
   3. **Passive Max Port**: Maximum port number that the FTP Server will use in passive mode. It must be higher than Passive Min Port field. The number of total ports should be higher than the number of concurrent FTP clients allowed. Range from 1024 to 65535.
   4. **Encryption:** Select the preferred Encryption schema used by the FTP Server. Options are FTP (no encryption), FTPES (explicit) and FTPS (implicit).
   5. **Control Port:** Port used by the server to listen to the FTP clients.
   6. **Log Level:** Select the Log Level using the drop down list. Options are None, Basic and High.
   7. **Description:** Free text field to include a description.
   8. **New Virtual User; Username:** Configure a user that the FTP Clients connecting to the Server needs to use for authentication. Several virtual users can be created.
   9. **New Virtual User; Password:** Configure a password that the FTP Clients connecting to the Server needs to use for authentication. Several virtual users can be created.

### [File Transfer, FTP Configuration](/docs/mdtransferguard/configuration/ftp-server#file-transfer-ftp-configuration)

As previously mentioned, the user must configure a FTP File Transfer on both BLUE and RED sides.

Important

For more information about configuring File Transfer, please refer to [File Transfer](/docs/mdtransferguard/configuration/3-file-transfer)

To configure the FTP File Transfer, follow the instructions below for these specific fields:

1. Go to **File Transfers-> FTP** and click on **Add FTP Share**.
2. **Server:** Indicate the IP of the FTP Server in BLUE side (most cases it is the same as the management IP).
3. **Share Path:** the share path for the built in FTP Server is **/files.**
4. **User:** Indicate the user configured in the FTP Server as Virtual User.
5. **Password:** Indicate the password configured in the FTP Server for the Virtual User.
6. **Encryption:** User needs to indicate the same encryption as the one configured in the FTP Server.

## [Diode X RED](/docs/mdtransferguard/configuration/ftp-server#diode-x-red)

### [FTP Server Configuration](/docs/mdtransferguard/configuration/ftp-server#ftp-server-configuration)

Important

To configure FTP Server Connector, a security dongle should be inserted in the RED server.

If the FTP Server hasn't been previously configured the user will see a Edit button to include a new FTP Server. This feature requires to reserve disk space to allow it to act as a FTP Server so, once the Edit button is pushed user would be notify of this circumstance via the message bellow.

Once the needed space has been reserved the user should input the following information.

1. Type or select values in the following boxes:

   1. **Allowed Source IPs or Ranges:** List of IP addresses allowed to connect to the FTP Server. User can enter several addresses or ranges separated by semicolon. Empty field means ANY IP will be allowed to connect.
   2. **Passive Min Port:** Minimum port number that the FTP Server will use in passive mode. Range from 1024 to 65535.
   3. **Passive Max Port**: Maximum port number that the FTP Server will use in passive mode. It must be higher than Passive Min Port field. The number of total ports should be higher than the number of concurrent FTP clients allowed. Range from 1024 to 65535.
   4. **Encryption:** Select the preferred Encryption schema used by the FTP Server. Options are FTP, FTPES (explicit) and FTPS (implicit).
   5. **Control Port:** Port used by the server to listen to the clients.
   6. **Log Level:** Select the Log Level using the drop down list. Options are None, Basic and High.
   7. **Description:** Free text field to include a description.
   8. **New Virtual User; Username:** Configure a user that the FTP Clients connecting to the Server need to use for authentication.
   9. **New Virtual User; Password:** Configure a password that the FTP Clients connecting to the Server need to use for authentication.
2. Click the **Submit** button.

### [File Transfer, FTP Configuration](/docs/mdtransferguard/configuration/ftp-server#file-transfer-ftp-configuration)

As previously mentioned, the user must configure a FTP File Transfer on both BLUE and RED sides.

To properly configure the FTP File Transfer, follow the instructions below for these specific fields:

1. Go to File Transfers-> FTP and click on **Add FTP Share**.
2. **Server:** Indicate the IP of the FTP Server in RED side (most times that would be the same as management IP).
3. **Share Path:** the share path for the built in FTP Server is **/files.**
4. **User:** Indicate the user configured in the FTP Server RED as Virtual User.
5. **Password:** Indicate the password configured in the FTP Server RED for the Virtual User.
6. **Encryption:** User needs to indicate the same encryption as the one configured in the FTP Server.
