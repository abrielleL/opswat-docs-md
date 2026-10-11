<!-- source: https://www.opswat.com/docs/fenddiode/configuration-settings/input-side-interface-settings -->

# Input Side Interface Settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Interface Select Radio Buttons](/docs/fenddiode/configuration-settings/input-side-interface-settings#interface-select-radio-buttons)

The options in this section will set the current communication interface mode for the inbound side of the diode. The diode operates in a single mode at a time (RS485 or Ethernet, but not both). Once a selection is made, the settings for that communication mode will be displayed below.

- RS485 – Sets the diode to use the serial port for inbound data communication
- Ethernet – Sets the diode to use the ethernet port for inbound data communication

## [RS485](/docs/fenddiode/configuration-settings/input-side-interface-settings#rs485)

- Baud Rate – Sets the diode serial port baud rate for serial protocols.

  - [9600, 19200, 36400, 57600, 115200]
- Parity – Sets the diode serial port parity

  - [None, Odd, Even]
- Data – Sets the diode serial port number of data bits

  - [8, 9]
- Stop Bits – Sets the diode serial port stop bits

  - [1 bit, 2 bits]

## [Ethernet](/docs/fenddiode/configuration-settings/input-side-interface-settings#ethernet)

- MAC Address – Displays the MAC address of the input side of the diode.
- DHCP Mode – Determines whether the IP address of the input side of the diode will use a static IP or will request a dynamic IP. The recommended default setting is “Static IP”

  - [Static IP, DHCP]
- Diode IP – If in “Static IP” mode, sets the IP address of the input side of the diode. Note: If you change the IP address of the input side of the diode. You must record and use this new IP address when attempting to log into the diode in the future.

  - [IP address in format: ###.###.###.###]
- Subnet Mask – Sets the network subnet mask of the input side of the diode.

  - [IP address in format: ###.###.###.###]
- Gateway IP Address – Sets the network gateway address of the input side of the diode.

  - [IP address in format: ###.###.###.###]
