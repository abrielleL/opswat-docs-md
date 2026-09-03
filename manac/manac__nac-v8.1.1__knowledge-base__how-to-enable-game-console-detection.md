<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection -->

# How to Enable Game Console Detection?

## [Overview](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#overview)

This document outlines the process for connecting gaming consoles to a NAC managed network.

## [Xbox](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#xbox)

Detection Overview: The user connects the Xbox to the network and receives an IP address. NAC detects the device on the network and blocks it as an unknown detection client. The user connects to Xbox Live, which provides NAC with sufficient traffic to properly classify the device as a Microsoft Gaming Console.

- Connect the Xbox to the network.
- The initial network connection test may fail at this time.

- Sign in to Xbox Live via the Xbox Dashboard.

## [Xbox One](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#xbox-one)

**Detection Overview**: When an Xbox One first comes on to the network, it will have limited functionality and will force the user to perform a network test. This will generate the necessary traffic to identify it as an Xbox One. If an Xbox One is identified as a different host type, have the admin expire and purge it from the Dashboard and have the end user perform a network test. This will generate the necessary traffic to identify it as an Xbox One

To run the Network Connection Test on your console, follow these steps:

1. Scroll left from **Home** to open the guide.
2. Select **Settings**.
3. Select **All Settings**.
4. Select **Network**.
5. Select **Network settings**. Any known outages will appear in the middle of the screen.
6. On the right side of the **Network settings**screen, select **Test network connection**.

## [Wii](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#wii)

**Detection Overview**: The user connects the Wii to the network and receives an IP address. NAC detects the device on the network and blocks it as an unknown detection client. The User then launches the Internet Channel and attempts to access and external resource which provides NAC with sufficient traffic to properly classify the device as a Nintendo Gaming Console.

**Internet Channel installed:**

- Connect the Wii to the network.
- Open the Internet Channel from the home screen and click “start”.

- Attempt to search/access and external web resource.
- The NAC dashboard should now show the device as a “Wii Gaming Console”

**Internet Channel not installed:**

- Grant the End User a 1-time Open Access window to acquire it for free from the Wii shopping channel.

- Open the Internet Channel from the home screen and click “start”.

## [Wii U](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#wii-u)

**Detection Overview**: The user connects the Wii U to the network and receives an IP address. NAC detects the device on the network and blocks it as an unknown detection client. The user then launches the Internet Browser and attempts to access and external resource which provides NAC with sufficient traffic to properly classify the device as a Nintendo Gaming Console.

**Internet Channel installed:**

- Connect the Wii U to the network.
- Open the Internet Browser from the home screen and click “start”.

- Attempt to search/access and external web resource.
- The NAC dashboard should now show the device as a “Wii Gaming Console”.

## [PS3](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#ps3)

**Detection Overview**: The user connects the PS3 to the network and receives an IP address. NAC detects the device on the network and blocks it as an unknown detection client. The user connects to the PlayStation Network which provides NAC with sufficient traffic to properly classify the device as a Sony Gaming Console.

- Connect the PS3 to the network.
- When configuring the internet connection, skip the “Test Connection” option as this test may fail the first time.

- Sign in to the PlayStation Network via the XMB.

## [PS4](/docs/manac/nac-v8.1.1/knowledge-base/how-to-enable-game-console-detection#ps4)

**Detection Overview**: The user connects the PS4 to the network and receives an IP address. NAC detects the device on the network and blocks it as an unknown detection client. The user connects to the PlayStation Network which provides NAC with sufficient traffic to properly classify the device as a Sony Gaming Console.

- Connect the PS4 to the network.
- When configuring the internet connection, skip the “Test Connection” option as this test may fail the first time.

- Sign in to the PlayStation Network via the XMB.

**Related articles**
