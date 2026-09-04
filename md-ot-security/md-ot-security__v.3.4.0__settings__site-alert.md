<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/settings/site-alert -->

# Site - Alert

Alert setting is accessible under **Settings > Alert**

On the alert setting page, the user can configure how MetaDefender OT Security behaves when there is an alert triggered: make an on-screen alert and notify the operator by sending a Syslog message.

**Make on-screen alert**

Users can choose how alerts can be displayed:

- **When "Make On-screen alert" is checked for criticality levels (Medium, High, Severe):** The user will be navigated to the alert screen whenever an alert based on the specified criticality level is triggered. All alerts must be resolved before the user can leave the alert screen.
- **When "Make On-screen alert" is unchecked for criticality levels (Medium, High, Severe):** Alerts will only appear on the alert list pages with an Acknowledge button beside them, allowing the user to resolve them later.
- At criticality levels, If users check on **“Provide a reason for acknowledgment”**, users need to provide one when acknowledging an alert.

In addition, you can apply this configuration for all sensors belonging to this site by checking on **“Overwrite for all sensors”**

Note: Alert with Medium criticality level will not be shown on screen by default.

**Send Syslog message**

Enable Send Syslog message if users want MetaDefender OT Security to send users a Syslog message.

Fill in the Server Address, Port, and Transport to receive the syslog. Users can also choose the Facility of the syslog message.

MetaDefender OT Security complies with [**RFC 3164**](https://www.ietf.org/rfc/rfc3164.txt) and [**RFC 5424**](https://datatracker.ietf.org/doc/html/rfc5424) **, and CEF format**

## [Syslog message format](/docs/md-ot-security/v.3.4.0/settings/site-alert#syslog-message-format)

**Alert with CEF format**

#### [Log format](/docs/md-ot-security/v.3.4.0/settings/site-alert#log-format)

CEF:[Version]|[Device Vendor]|[Device Product]|[Device Version]|[Signature ID]|[Name]|[Severity]|[Extension]

| Prefix field | Sample value | Description |
| --- | --- | --- |
| CEF:[Version] | CEF:0 | Version 0.x |
| Device Vendor | OPSWAT |  |
| Device Product | MDOTS | MDOTS = MetaDefender OT Security |
| Device Version | 3.2.0 | MetaDefender OT Security version |
| Signature ID | dev-unauthorized | **Asset Alert Type**   - dev-baseline - dev-unauthorized - dev-communicate - dev-country-of-origin - dev-cve - dev-open-port - dev-mis-configuration   **Connection Alert Type**   - conn-baseline - conn-unauthorized - conn-country-of-origin - conn-communicate - conn-source-port - conn-destination-port - conn-period |
| Name | Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [Medium] A Device PLC ABB 047 has violation: Device of type Industrial Device is detected. Industrial Device is not allowed on the network | Alert Message |
| Severity | medium | severe  high  medium |
| Extension | site=10.40.163.144  sensor=10.40.163.172  sproc=PLC ABB 047  src=192.168.1.120 | **Asset Alert**   - site: Site IP - sensor: Sensor IP - sproc: Device Name - src: Device IP   **Connection Alert**   - site: Site IP - sensor: Sensor IP - sproc: Source Device Name - src: Source Device IP - spt: Source Device Port - dproc: Destination Device Name - dst: Destination Device IP - dpt: Destination Device Port - start: Start time (local time, format: YYYY.MM.DD HH:mm:ss) - app: Protocol |

#### [Log sample](/docs/md-ot-security/v.3.4.0/settings/site-alert#log-sample)

#### [Connection Alert](/docs/md-ot-security/v.3.4.0/settings/site-alert#connection-alert)

> CEF:0|OPSWAT|MDOTS|3.2.0|conn-destination-port|Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [Severe] Device HMI Delta Electronic 049 (192.168.1.204) (192.168.1.204) - Device PLC Schneider Electric Modicon M221 045 (192.168.1.104) (192.168.1.104) with Modbus-TCP protocol [duration: 131.15, start time: 2024.08.29 14:17:27, source port: 49449, destination port: 502] has violation: Destination port 502 is in disallowed policy|severe|site=10.40.163.144 sensor=10.40.163.172 sproc=HMI Delta Electronic 049 (192.168.1.204) src=192.168.1.204 spt=49449 dproc=PLC Schneider Electric Modicon M221 045 (192.168.1.104) dst=192.168.1.104 dpt=502 start=2024.08.29 14:17:27 app=Modbus-TCP

#### [Asset Alert](/docs/md-ot-security/v.3.4.0/settings/site-alert#asset-alert)

> CEF:0|OPSWAT|MDOTS|3.2.0|dev-cve|Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [Severe] A Device PLC Siemens SIMATIC S7-1500 004 has violation: Vulnerability (CVE) CVE-2019-10936 with score of 7.5 is found on the device. CVE in score range [7.0-10.0] is to be notified|severe|site=10.40.163.144 sensor=10.40.163.172 sproc=PLC Siemens SIMATIC S7-1500 004 src=192.168.1.109

**Alert with RFC format**

#### [Log format](/docs/md-ot-security/v.3.4.0/settings/site-alert#log-format)

[Name]

| Prefix field | Sample value | Description |
| --- | --- | --- |
| Name | <81>Aug 29 11:31:44 opswat-otssm-AMC5N002110405N50 Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [High] Device Generic BIZLINK TECHNOLOGY, INC. 007 (192.168.1.224) (192.168.1.224) - Device PLC Schneider Electric Modicon M221 045 (192.168.1.104) (192.168.1.104) with DNS protocol [duration: 3.02, start time: 2024.08.29 11:30:27, source port: 137, destination port: 137] has violation: Connection violates unauthorized policy from Purdue level 5 to Purdue level 1 | Alert Message |

#### [Log sample](/docs/md-ot-security/v.3.4.0/settings/site-alert#log-sample)

> <81>Aug 29 11:31:44 opswat-otssm-AMC5N002110405N50 Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [High] Device Generic BIZLINK TECHNOLOGY, INC. 007 (192.168.1.224) (192.168.1.224) - Device PLC Schneider Electric Modicon M221 045 (192.168.1.104) (192.168.1.104) with DNS protocol [duration: 3.02, start time: 2024.08.29 11:30:27, source port: 137, destination port: 137] has violation: Connection violates unauthorized policy from Purdue level 5 to Purdue level 1

> <81>1 2024-08-29T04:41:49+00:00 opswat-otssm-AMC5N002110405N50 - - - Site: Site 10.40.163.144 - Sensor: Sensor 10.40.163.172 [Severe] A Device Generic REALTEK SEMICONDUCTOR CORP. 017 has violation: Device of type Generic is detected. Generic is not allowed on the network
