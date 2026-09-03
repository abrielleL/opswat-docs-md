<!-- source: https://www.opswat.com/docs/filescan/configuration/engine -->

# Engine

Engine configurations is being described inside the Configurations part on this part of the page.

**Admin Panel > Setting > Configurations > Engine**

These configurations together define how the MetaDefender Sandbox communicates with its embedded malware analysis engine, including the protocol, host, port, and authentication mechanism.

Screenshot of Engine settings inside Configuration part on MetaDefender Sandbox webpage

| Field | Description |
| --- | --- |
| *ENGINE_SCHEMA* | Specifies the protocol or schema used for communication with embedded MetaDefender Sandbox. In this case, it's set to "https", indicating that HTTPS (HTTP Secure) protocol is used for secure communication. |
| *ENGINE_HOST* | Specifies the IP address or hostname of the server where the malware analysis engine is hosted. In this configuration, the IP address needs to be provided. |
| *ENGINE_PORT* | Specifies the port number used for communication with the malware analysis engine |
| *ENGINE_SECRET* | This is internal secret key used for communication between components of MetaDefender Sandbox. The value is masked for security reasons. The default value is set by the Sandbox installer. The default value should not be changed. |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
