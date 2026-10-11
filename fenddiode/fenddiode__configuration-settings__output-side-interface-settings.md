<!-- source: https://www.opswat.com/docs/fenddiode/configuration-settings/output-side-interface-settings -->

# Output Side Interface Settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Interface Select Radio Buttons](/docs/fenddiode/configuration-settings/output-side-interface-settings#interface-select-radio-buttons)

The options in this section will set the current communication interface mode for the outbound side of the diode. The diode operates in a single mode at a time (RS485, Ethernet or Cellular). Once a selection is made, the settings for that communication interface mode will be displayed below.

- RS485 – Sets the diode to use the serial port for outbound data communication
- Ethernet – Sets the diode to use the ethernet port for outbound data communication
- Cellular - Sets the diode to use the ethernet port for outbound data communication

## [RS485 (Supported on SE models only)](/docs/fenddiode/configuration-settings/output-side-interface-settings#rs485-supported-on-se-models-only)

- Baud Rate – Sets the diode serial port baud rate

  - [9600, 19200, 36400, 57600, 115200]
- Parity – Sets the diode serial port parity

  - [None, Odd, Even]
- Data Bits – Sets the diode serial port number of data bits

  - [8, 9]
- Stop Bits – Sets the diode serial port stop bits

  - [1 bit, 2 bits]

## [Ethernet](/docs/fenddiode/configuration-settings/output-side-interface-settings#ethernet)

- MAC Address – Displays the MAC address of the output side of the diode.
- DHCP Mode – Determines whether the IP address of the output side of the diode will use a static IP or will request a dynamic IP. Also, has options for using DHCP for the diode IP, but making DNS or NTP static. The recommended default setting is “Static IP”.

  - [Static IP, DHCP, DHCP w/ Static DNS, DHCP w/ Static NTP, DHCP w/ Static DNS and NTP]
- Diode IP – Sets the IP Address of the output side of the diode.

  - [IP address in format: ###.###.###.###]
- Subnet Mask – Sets the network subnet mask of the output side of the diode.

  - [IP address in format: ###.###.###.###]
- Gateway IP Address – Sets the network gateway address of the output side of the diode.

  - [IP address in format: ###.###.###.###]
- DNS Server – Sets the location of the DNS server (used to resolve endpoint URLs)

  - [IP address in format: ###.###.###.###]
- NTP Server – Sets the location of the NTP server (used data timestamps)

  - [IP address in format: ###.###.###.### or URL UTF8 string, max 32 characters]

## [Cellular (Supported on CE models only)](/docs/fenddiode/configuration-settings/output-side-interface-settings#cellular-supported-on-ce-models-only)

There are no additional settings for cellular at this time.
