<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples -->

# Fend TCP/JSON Server Tool Examples

The Fend TCP/JSON Server Tool is a lightweight TCP server designed to receive and log JSON TCP output from the diode. Use of the Fend TCP Server Tool is not required to use the diode’s TCP Client (JSON Protocol Conversion) output feature but may be helpful for testing or logging.

If you wish to use/develop your own TCP server, the communications interface with the output side of the diode is relatively straightforward. No handshake is needed for the output side to connect to a TCP server. The output side is configured to connect to a specific IP address and port. Upon startup the output side of the diode will attempt to connect to the configured IP address. If it fails to connect, the output side will attempt a re-connection every few seconds. If the connection is successful the output side of the diode will begin delivering ASCII encoded JSON strings delimited by a "CRLF". CR = Carriage Return (\r , 0x0D in hexadecimal, 13 in decimal). LF = Line Feed (\n, 0x0A, 10 in decimal). If the output side ever loses connection, it will continue storing data until the connection is reestablished.

## [Network/System Requirements](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#networksystem-requirements)

### [Downloading and Installing the Fend TCP Server Tool](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#downloading-and-installing-the-fend-tcp-server-tool)

Download the latest Fend TCP Server Tool from <https://app.fend.tech/login>. Log in using your Fend account user name and password. Go to “Support” and then to the “Downloads” section. Look for the Fend TCP Server Tool. If you have issues logging in or downloading the tool, contact us at [support@fend.tech](mailto:support@fend.tech).

Save the Fend TCP Server Tool executable to a computer that will have access to the same network as the output side of the diode.

### [Network Requirements](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#network-requirements)

Before launching the tool, you’ll need to gather some information about the host machine that the Fend TCP Server Tool will be running on. The host machine will be the “Target” point for the data coming from the data diode. You’ll need to record the host system’s IP address (IPv4), which will be used to tell the diode where to send data. You’ll also need it to configure the Fend TCP Server Tool, so it knows which IP use for incoming data.

To begin, open the start menu, and type “cmd” and press enter. Type “ipconfig” and press enter. You should see a display similar to the following:

The relevant information from this listing should be any Ethernet adapters. There should only be one for most systems. If there are multiple listings this will be out of the scope of the document. Take note of the IPv4 Address.

## [Setting Up the Fend TCP Server Tool](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool)

### [Session Configuration](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#session-configuration)

Upon startup, the user will be presented with one of two prompts. If the server has been run before, and the software found a valid config file, it will report it has found settings from a previous session and ask if you would like to continue with those settings. Pressing “y” will continue with the preloaded settings shown on the screen and pressing “n” will allow the user to enter new settings.

### [New Settings Setup](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#new-settings-setup)

If it’s the first time launching the program, or no valid config data was found, the process for setting up a new server will be run. This process will gather all of the configuration information needed for operation. Starting with IP Address.

1. IP Address - The IP addresses need to be both properly formatted and one that is currently set to a network interface on the host system. The diode client will look for this IP to connect to the host machine and the Fend TCP Server Tool. At the prompt enter the host system’s IP address and press enter.
2. Log File Directory - Where log files should be stored. Enter in the desired directory as a complete directory location. An example can be seen below. If the entered directory does not exist, the server will create it.
3. Port Number - The port the server should listen on. Simply enter the same port number as the one set on the diode’s “Target Port” setting (see [Diode Settings for Use with TCP Server](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#diode-settings-for-use-with-tcp-server) on how to find and configure this) and press enter.
4. File Size Limit - Enter a max file size for the individual log files generated during runtime. When a timestamped log file reaches the max file size it will be closed and a new timestamped log file will be started. The range allows for file sizes in integer increments between 1MB (min) and 10MB (max).
5. Indented vs Inline JSON - The last option is the choice of inline or indented JSON. Data written inline is one JSON statement per line. This can be much easier to parse in a script. Indented prints the JSON data in a more human-readable format allowing users to verify data by hand easily. This option will require more work to import individual JSON statements with a script. Answer “y” or “n” for indented or inline respectively.

### [Runtime](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#runtime)

Once the configuration has been completed, the server will now enter runtime. During this mode, the server is actively listening for diodes to begin connections to the server. While this is the case, the only notification will be “Waiting for a connection…”. If this is the only text on screen, a diode has not connected yet.

Once a diode connects, a message will appear saying “Connection from: <IP Address>” where the IP address listed is the IP of the output side of the connecting diode. Two things will occur. First, the server will start listening for new connections, indicated by a “Waiting for a connection” output on the console. Second, the server will be receiving all TCP transactions, parsing the JSON, and writing the message to the associated diode file.

When you are confident that data is being sent to the server, check for log files in the set directory.

## [Diode Settings for Use with TCP Server](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#diode-settings-for-use-with-tcp-server)

The Fend TCP Server Tool is compatible with Modbus, BACnet, and LON input protocols. Using the Fend Configuration Tool, connect to the diode, and configure the input side of the diode for your application.

Note: For a detailed guide on how to configure your diode please refer to the [**Configuring a Fend Data Diode**](https://www.opswat.com/docs/fenddiode/configuration-settings) section.

Once you have the diode’s input side configured, the following additional diode settings are required for connecting to the Fend Diode Config Tool:

- Output Side -> Ethernet -> Diode IP Address. The “Diode IP Address” is the IP address assigned to the output side of the diode. This IP can be set to any open IP address, but it needs to be on the same subnet as your target server host system IP address. Generally, this means it should look like your system IP, but with the last number changed a bit.
- Example:

  - Server Host System IP: 192.168.1.20
  - Data Diode IP: 192.168.1.28
- Output Side -> Protocol -> TCP Client (JSON Protocol Conversion) -> Target IP Address. The “destination IP” address setting in the diode is the IP address where you intend to send the data. In this case, it should be set to the IP address of your host system where you will run the Fend Diode TCP Server.
- Output Side -> Protocol -> TCP Client (JSON Protocol Conversion) -> Target Port. The destination TCP Port can be any port that is available on your host system, just make sure to remember what is entered. This port number will be required when setting up the Fend Diode TCP Server. Generally, port 502 is used.

Finally, when done updating all settings press the “Disconnect” button located at the top left of the Diode Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#installing-the-data-diode-after-configuration)

1. Connect the diode’s input side to the input protocol network.
2. Connect the diode’s output side to the computer or network containing the computer running the TCP Server Tool.
3. Plug in power to both sides of the diode.
4. Verify data is received on the outbound network.
