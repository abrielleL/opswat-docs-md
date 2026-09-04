<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-vi-secondary-communication-indicator-light-patterns -->

# Appendix VI: Secondary Communication Indicator Light Patterns

This section contains tables for cross-referencing patterns from the Red/Green Secondary Communication Indicator LED bank. Bank B is the secondary communication indicator bank for the input side of the diode. Bank D is the secondary communication indicator bank for the output side of the diode.

## [Physical Connection Status for Ethernet](/docs/fenddiode/appendices/appendix-vi-secondary-communication-indicator-light-patterns#physical-connection-status-for-ethernet)

| Red | Green | Description |
| --- | --- | --- |
| Slow Alternate Red/Green | Slow Alternate Red/Green | Resolving DHCP |

## [Physical Connection Status for Serial](/docs/fenddiode/appendices/appendix-vi-secondary-communication-indicator-light-patterns#physical-connection-status-for-serial)

| Red | Green | Description |
| --- | --- | --- |
| Off | On | Serial Interface Ready / Standby |
| N/A | *Blink on Tx* | Data Transmitting (RS485 data only) |
| *Blink on Rx* | N/A | Data Receiving (RS485 data only) |

## [Physical Connection Status for Cellular](/docs/fenddiode/appendices/appendix-vi-secondary-communication-indicator-light-patterns#physical-connection-status-for-cellular)

| Red | Green | Description |
| --- | --- | --- |
| Slow Alternate Red/Green | Slow Alternate Red/Green | Resolving DHCP |
| N/A | Slow Blink | Cellular Connecting to Network |
| N/A | On | Cellular Connected |
| N/A | Off | Cellular Powered Off |
