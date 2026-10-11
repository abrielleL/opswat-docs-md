<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands -->

# Appendix IV: List of Supported BACnet Commands

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [PDU Types](/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands#pdu-types)

- complex-ack-pdu (3)

## [BACnetConfirmedServiceChoice:](/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands#bacnetconfirmedservicechoice)

- read-property (12)
- read-property-multiple (14)

## [BACnetPropertyIdentifier:](/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands#bacnetpropertyidentifier)

This list is not exhaustive. It is a list of properties that we have seen successfully parsed in our testing

- active-text (3)
- description (28)
- event-state (36)
- inactive-text (46)
- object-identifier (75)
- object-name (77)
- object-type (79)
- out-of-service (81)
- polarity (84)
- priority-array (87)
- present-value (85)
- relinquish-default (104)
- status-flags (111)
- units (117)
- vendor-identifier
- firmware-revision
- protocol-services-supported
- object-list
- device-address-binding
- system-status
- apdu-timeout
- model-name
- vendor-name
- application-software-version
- number-of-APDU-retries
- database-revision

## [Unsupported BACnetPropertyIdentifier:](/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands#unsupported-bacnetpropertyidentifier)

- weekly-schedule (123)
- EventTimeStamps (130)
- TimeOfDeviceRestart (203)

## [Other Notes:](/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands#other-notes)

1. Multi-datagram BACnet response packets are currently not supported.
