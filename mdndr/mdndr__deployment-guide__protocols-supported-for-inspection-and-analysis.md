<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/protocols-supported-for-inspection-and-analysis -->

# Protocols Supported For Inspection and Analysis

Our NDR provides full protocol decode, anomaly detection, structured log, and file extraction support for the protocols below.

**Detailed protocol support table:**

| Protocol Category | Protocol | Decode | Anomaly Detection | File Extraction | Logging | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Link / L2 | Ethernet / VLAN / QinQ | Yes | Yes | No | Yes | Full header parse |
| Network | IPv4 / IPv6 / ICMP | Yes | Yes | No | Yes | Fragment reassembly |
| Transport | TCP / UDP | Yes | Yes | No | Yes | Stream reassembly |
| Application (IT) | HTTP / HTTP2 | Yes | Yes | Yes | Yes | URI, headers, body |
| Application (IT) | TLS | Yes | Yes | No | Yes | JA3 / JA4 / certs |
| Application (IT) | DNS | Yes | Yes | No | Yes | Query/response |
| Application (IT) | SMTP | Yes | Yes | Yes | Yes | Attachments |
| Application (IT) | SSH | Yes | Yes | No | Yes | Version / key exchange |
| Application (IT) | SMB (v1–v3) | Yes | Yes | Yes | Yes | File transfers |
| Application (IT) | FTP | Yes | Yes | Yes | Yes | Data channel |
| Application (IT) | RDP | Yes | Yes | No | Yes | Basic session |
| Application (IT) | QUIC | Yes | Yes | No | Yes | JA4 / ALPN |
| OT / ICS | Modbus | Yes | Yes | Yes | Yes | Industrial commands |
| OT / ICS | DNP3 | Yes | Yes | No | Yes | SCADA |
| OT / ICS | ENIP / CIP | Yes | Yes | Yes | Yes | Rockwell |
| OT / ICS | S7comm | Yes | Yes | Yes | Yes | Siemens |
| OT / ICS | BACnet | Yes | Yes | No | Yes | Building automation |
| OT / ICS | IEC104 | Yes | Yes | No | Yes | Power grid |
| VoIP | SIP / SDP | Yes | Yes | No | Yes | Session setup |
