<!-- source: https://www.opswat.com/docs/fenddiode/introduction/diode-operation -->

# Diode Operation

Fend Data Diodes have two distinct working modes, operational mode and configuration mode. The diode only operates in a single mode at any given time. When in operational mode, settings cannot be changed. When in configuration mode, no data will be transmitted, and protocol tasks will not run. These modes function as follows:

- **Operational Mode:** When powered on, the Fend Data Diode boots automatically into operational mode. In operational mode, the diode attempts to connect to the data source and destination using the protocol(s) specified in the diode settings. Once connected, the diode will begin transmitting data.
- **Configuration Mode:** Configuration Mode can be entered by logging into the Fend Data Diode with via your web browser (see [**Configuring a Fend Data Diode**](https://www.opswat.com/docs/fenddiode/configuring-a-data-diode)). Configuration mode allows the user to change the diode’s settings. Entering configuration mode will disable operational mode. When in configuration mode, the diode will not connect to any data sources, run any protocol tasks, or transmit data. To apply settings changes and return to operational mode, you must click the “Save and Exit” button in the upper righthand corner of the web configuration interface. The diode will then reboot and enter operational mode.
