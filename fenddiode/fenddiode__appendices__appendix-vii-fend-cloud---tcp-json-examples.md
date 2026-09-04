<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples -->

# Appendix VII: Fend Cloud / TCP JSON Examples

This appendix provides example JSON outputs from the Fend Cloud API or TCP JSON modes for Modbus, BACnet, and LON data. The data received from the Fend Cloud AWS API or in TCP JSON mode will be encapsulated in an array, with each element being an object in the forms seen below. The data seen in the “payload” object is all the data sent from the diode. It will contain information about the protocol and values. Outside the “payload” object are fields populated by AWS, when using the Fend Cloud API, used for tracking and categorizing the data set, such as ingest time and diode serial number.

## [Modbus AWS](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#modbus-aws)

JsonCopy{ "payload": { "address": "192.168.1.21", "sequenceNum": 204, "hiByteFirst": 1, "valueRaw": "6A6758544A58794F", "hiWordFirst": 1, "function": 4, "dataType": "str64", "deviceID": 1, "value": "jgXTJXyO", "transactionID": 25192, "register": 108 }, "ingested": 1664891195192, "created": 1664891189152, "scope": "data", "id": "abcd", "diode": "XX-XXXX-XXXXXX", "type": "modbusTCP"}
### [Modbus JSON Field Definitions](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#modbus-json-field-definitions)

payload [object] – A single Modbus data point

- address [string] - IP address of the source device
- sequenceNum [number] – Polling cycle number. Used to collect all data associated with a single polling cycle for analysis. Sequence numbers range from 0-65535 and restart at 0 after 65556.
- hiByteFirst [Boolean] – Modbus data point byte order. 1 = High Byte First, 0 = Low Byte First.
- valueRaw [string] – The raw Modbus register data before conversion. For validation of the “value” field.
- hiWordFirst [Boolean] – Modbus data point word order. 1 = High Word First, 0 = Low Word First.
- function [number] – Modbus function code for data point.
- dataType [string] – Data type of Modbus data point.
- deviceID [number] – Modbus device ID.
- value [string] – Converted Modbus value based on the data type and byte and word orders.
- transactionID [number] – ID generated in the Modbus poll request. Used to collect all data associated with a single request.
- register [number] – Modbus register address.

ingested [number] –Cloud ingest time in Unix Milliseconds format.

created [number] – Diode data create time in Unix Milliseconds format.

scope [string] – Cloud location identifier.

id [string] – Cloud unique identifier.

diode [string] – Diode serial number.

type [string] – Type of data (protocol) sent from diode. Modbus TCP in this case.

## [BACnet AWS](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#bacnet-aws)

JsonCopy{ "payload": { "dst": "192.168.1.201", "src": "192.168.1.179", "objects": [ { "objectType": "analog-input", "objectInstance": 1, "properties": { "present-value": 4.02 } }, { "objectType": "analog-input", "objectInstance": 2, "properties": { "present-value": 5 } } ] }, "ingested": 1630630788660, "created": 1630630787587, "scope": "data", "id": "abcd", "diode": "XX-XXXX", "type": "BACnetIP"
## [LonIP AWS](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#lonip-aws)

JsonCopy{ "payload": { "destIP": "129.229.2.37", "SrcSubnet": 9, "srcIP": "129.229.2.32", "SrcNode": 2, "NVSelector": 66, "DstSubnet": 1, "Data": "8a8a", "DstNode": 126, "NVDirection": 0, "Domain": "8e" }, "ingested": 1630588036111, "created": 1630588034712, "scope": "data", "id": "abcd", "diode": "XX-XXXX", "type": "LON/IP"}
