<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples -->

# Appendix VII: Industrial Protocol to JSON Conversion Examples

This appendix provides example JSON outputs from the Fend Cloud API, local MQTT or TCP JSON modes for Modbus, BACnet, and LON data. The data received from these modes will be encapsulated in an array, with each element being an object in the forms seen below. The data seen in the “payload” object is all the data sent from the diode. It will contain information about the protocol and values. Outside the “payload” object are fields populated by AWS, when using the Fend Cloud API, used for tracking and categorizing the data set, such as ingest time and diode serial number.

## [Modbus JSON](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#modbus-json)

MQTT PublisherFend CloudTCP Client with JSON ConversionCopy{ "type": "modbusTCP", "created": 0, "diode": "FD_169", "payload": { "address": "192.168.0.21", "transactionID": 3685, "sequenceNum": 15, "deviceID": 20, "function": 4, "register": 30018, "valueRaw": "3FC7173AA8380717", "value": "0.180396396768679", "dataType": "f64", "hiByteFirst": 1, "hiWordFirst": 1 }}{ "payload": { "address": "192.168.1.21", "sequenceNum": 204, "hiByteFirst": 1, "valueRaw": "6A6758544A58794F", "hiWordFirst": 1, "function": 4, "dataType": "str64", "deviceID": 1, "value": "jgXTJXyO", "transactionID": 25192, "register": 108 }, "ingested": 1664891195192, "created": 1664891189152, "scope": "data", "id": "abcd", "diode": "XX-XXXX-XXXXXX", "type": "modbusTCP"}{ "type": "modbusTCP", "created": 0, "diode": "0", "payload": { "address": "192.168.0.20", "transactionID": 46308, "sequenceNum": 0, "deviceID": 20, "function": 4, "register": 30022, "valueRaw": "724A5365", "value": "rJSe", "dataType": "str32", "hiByteFirst": 1, "hiWordFirst": 1 }}
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

*ingested [number] –Cloud ingest time in Unix Milliseconds format.

created [number] – Diode data create time in Unix Milliseconds format.

*scope [string] – Cloud location identifier.

*id [string] – Cloud unique identifier.

diode [string] – For Fend Cloud data, this will be the diodes serial number. For MQTT Publisher data this will be the [Client ID](/docs/fenddiode/configuration-settings/output-side-protocol-settings#mqtt-publisher).

type [string] – Type of data (protocol) sent from diode. Modbus TCP in this case.

*Fend Cloud Only

## [BACnet JSON](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#bacnet-json)

MQTT PublisherFend CloudTCP Client with JSON ConversionCopy{ "created": 0, "diode": "FD_169", "type": "BACnetIP", "payload": { "dst": "192.168.1.201", "src": "192.168.1.179", "objects": [ { "objectType": "analog-input", "objectInstance": 1, "properties": { "present-value": 4.02 } }, { "objectType": "analog-input", "objectInstance": 2, "properties": { "present-value": 5 } } ] }}{ "payload": { "dst": "192.168.1.201", "src": "192.168.1.179", "objects": [ { "objectType": "analog-input", "objectInstance": 1, "properties": { "present-value": 4.02 } }, { "objectType": "analog-input", "objectInstance": 2, "properties": { "present-value": 5 } } ] }, "ingested": 1630630788660, "created": 1630630787587, "scope": "data", "id": "abcd", "diode": "XX-XXXX", "type": "BACnetIP"{ "created": 0, "diode": "0", "type": "BACnetIP", "payload": { "dst": "192.168.1.201", "src": "192.168.1.179", "objects": [ { "objectType": "analog-input", "objectInstance": 1, "properties": { "present-value": 4.02 } }, { "objectType": "analog-input", "objectInstance": 2, "properties": { "present-value": 5 } } ] }}
## [LonIP JSON](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples#lonip-json)

MQTT PublisherCopy{ "created": 0, "diode": "FD_169", "type": "LON/IP",  "payload": { "destIP": "129.229.2.37", "SrcSubnet": 9, "srcIP": "129.229.2.32", "SrcNode": 2, "NVSelector": 66, "DstSubnet": 1, "Data": "8a8a", "DstNode": 126, "NVDirection": 0, "Domain": "8e" }}
