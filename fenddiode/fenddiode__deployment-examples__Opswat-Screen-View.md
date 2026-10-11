<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/Opswat-Screen-View -->

# OPSWAT Screen View

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Introduction](/docs/fenddiode/deployment-examples/Opswat-Screen-View#introduction)

The OPSWAT Screen View Connector allows the user to replicate the HMI screen of a Windows device from the input side network to the output side network.

The OPSWAT Screen View Recorder collects the data from the Windows machine on the input and provides an unidirectional transfer of that data (UDP packets) to the OPSWAT Screen View Player output side network.

## [Supported features](/docs/fenddiode/deployment-examples/Opswat-Screen-View#supported-features)

OPSWAT Screen View functionality provides the following features:

- Supports MPEG-1 video codec.
- Supports MPEG-2 video codec.
- Supports MPEG-4 video codec.
- Configurable Frame Rate.
- Configurable Caching.

## [Install Screen View](/docs/fenddiode/deployment-examples/Opswat-Screen-View#install-screen-view)

### [Prerequisites](/docs/fenddiode/deployment-examples/Opswat-Screen-View#prerequisites)

- You must have admin rights on any machine where you want to install OPSWAT Screen View components.
- Windows 10, Windows 11 Operating Systems.

Supported resolutions are indicated in the table below:

|  | Resolutions |  |
| --- | --- | --- |
| 640x480 | 1280x800 | 1600x1200 |
| 800x600 | 1280x1024 | 1680x1050 |
| 1024x768 | 1366x768 | 1920x1080 |
| 1280x720 | 1440x900 | 1920x1200 |
| 1280x768 | 1400x1050 | 2452x1356 |

## [Download OPSWAT Screen View](/docs/fenddiode/deployment-examples/Opswat-Screen-View#download-opswat-screen-view)

Go to https://my.opswat.com and sign in. Navigate to product downloads and search for Metadefender Netwall. Click "Download" in the middle of the screen.

In the pop up, navigate to "Netwall Connectors", then "Screen View". Download both the Recorder and Player softwares.

## [Install on Input Flanking Server](/docs/fenddiode/deployment-examples/Opswat-Screen-View#install-on-input-flanking-server)

Install OPSWAT Screen View Recorder.msi file on any machine in the Input zone where you want to stream the screen to the output side.

Double-click OPSWAT Screen View Recorder.msi and accept the defaults until the installation is complete.

## [Install on Output Flanking Server](/docs/fenddiode/deployment-examples/Opswat-Screen-View#install-on-output-flanking-server)

Install OPSWAT Screen View Player.msi file on any machine in the Output zone where you want to replicate the data coming from the Input side.

Double-click OPSWAT Screen View Player.msi and accept the defaults until the installation is complete.

## [Configuring Screen View](/docs/fenddiode/deployment-examples/Opswat-Screen-View#configuring-screen-view)

To configure the OPSWAT Screen View for use with the Fend data diode, the general configuration process is as follows. Each of these steps is described in further detail below:

1. Configure the fend diode to UDP Client/Server mode.
2. Configure Screen View Recorder on the BLUE flanker.
3. Configure Screen View Player on the RED flanker.

## [Configure the Diode](/docs/fenddiode/deployment-examples/Opswat-Screen-View#configure-the-diode)

First, you will need to configure the diode to be in UDP client server mode. Follow these steps:

1. Login into the Fend Diode Web GUI.
2. Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

   1. Set the “DHCP Mode” to “Static IP”.
   2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.

      1. Note: This is the IP address that the Screen View Recorder will use to send data to the diode’s UDP server.
   3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select UDP Server from the dropdown and set the following:

3. Set the “Diode UDP Server Port” to be any port that is available on your host system, just make sure to remember what is entered. This port number will be required when configuring the Screen View Recorder to communicate with the diode’s UDP server.
4. Disable the “Reply with an ACK” option.

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

5. Set DHCP mode as needed for the local network. If using static IPs, set the Diode IP Address for the output side to ensure that it has a unique address on the network.
6. Set the Subnet Mask and Gateway IP Address as needed for the local network.

Under Output Side -> Protocol Settings -> Select UDP Client from the dropdown and set the following fields:

8. Set the “Target UDP Server IP” to match computer's IP the Screen View Player is running on.
9. Set the “Target UDP Server Port” to be any port that is available on target host system, just make sure to remember what is entered. This port number will be required when configuring the Screen View Player to receive data from the diode’s UDP client.
10. Save & Exit.

## [Configure Screen View Recorder](/docs/fenddiode/deployment-examples/Opswat-Screen-View#configure-screen-view-recorder)

To configure Screen View Recorder:

1. Destination IP: The diodes input side IP address.
2. Destination UDP Port: The same port you entered step 4 above.
3. Configuration Name: Give a name to the configuration to recall the settings at a later date.
4. Load Configuration: User can load previously saved configurations.
5. Frame Rate: User can define the Frame Rate of the recording.
6. Video Codec: Select one of the codecs supported (MPEG-1, MPEG-2, MPEG-4).
7. Caching [ms]: User can define the amount of time they want to buffer before start streaming.

Once the configuration is finished, click on Start so Screen View recorder starts sending data to the diodes UDP server.

## [Configure Screen View Player](/docs/fenddiode/deployment-examples/Opswat-Screen-View#configure-screen-view-player)

To configure Screen View Player:

1. Configuration Name: Give a name to the configuration to recall the settings at a later date.
2. Listen UDP Port: the same port you entered in step 9.
3. Caching [ms]: User can define the amount of time they want to buffer before start reproducing.
4. Screen Name: Screen View Player, can display up to 4 different screens, Screen Name field is used to differentiate those screens.

Once the configuration is finished, click on Start so Screen View player starts playing the stream coming from diodes UDP server.

## [Save Configuration](/docs/fenddiode/deployment-examples/Opswat-Screen-View#save-configuration)

To save an specific configuration just fill in the fields and then click on Save (or Save Configuration in Screen View Player).

## [Load Configuration](/docs/fenddiode/deployment-examples/Opswat-Screen-View#load-configuration)

To load a previously saved configuration user only needs to deploy the Load Configuration dropdown list and select the saved configuration that wants to be applied.
