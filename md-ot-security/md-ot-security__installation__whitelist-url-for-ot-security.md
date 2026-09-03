<!-- source: https://www.opswat.com/docs/md-ot-security/installation/whitelist-url-for-ot-security -->

# Notes for deployment of MD OT Security | Firewall Allow-listed Configurations

### [This document outlines the URLs and ports that must be allowed in the firewall to ensure proper functionality of the Network Sensor, Site Manager, and Enterprise Manager.](/docs/md-ot-security/installation/whitelist-url-for-ot-security#this-document-outlines-the-urls-and-ports-that-must-be-allowed-in-the-firewall-to-ensure-proper-functionality-of-the-network-sensor-site-manager-and-enterprise-manager)

## [Allow-listed URLs](/docs/md-ot-security/installation/whitelist-url-for-ot-security#allow-listed-urls)

The following URLs are required for system operations and updates:

- [**https://my.opswat.com**](https://my.opswat.com/)**:** Access to the OPSWAT business support portal.
- [**https://activation.dl.opswat.com**](https://activation.dl.opswat.com/): License activation and validation.
- [**https://mdots-cdn.opswat.com**](https://mdots-cdn.opswat.com/): Content delivery for updates and resources.

## [Allow-listed Ports](/docs/md-ot-security/installation/whitelist-url-for-ot-security#allow-listed-ports)

The following ports must be open for communication between components

### [Network Sensor](/docs/md-ot-security/installation/whitelist-url-for-ot-security#network-sensor)

- **1443**:

  - Purpose: Using for communication from Site Manager to Network Sensor.
  - Only required when communication between Site Manager and Network Sensor is **Bi-Directional**. (ie: no need if communication between Site Manager and Network Sensor is **Uni-Directional**.)
  - Communication is secured by TLS 1.3.
  - Authentication is token-based.
  - Token lifecycle:

    - Version < 3.5.0: Token never expires until next established connection.
    - From version 3.5.0: Token will expire according to configuration.
- **443:**

  - Purpose: Using for user to perform initial configuration via web console.
  - Communication is secured by TLS 1.3.
  - Authentication: User account credentials.

### [Site Manager](/docs/md-ot-security/installation/whitelist-url-for-ot-security#site-manager)

- **3006**:

  - Purpose: For the communication between Site Manager with Network Sensor and Enterprise Manager.

    - From Network Sensor to Site Manager (Uni-Directional and Bi-Directional)
    - From Enterprise Manager to Site Manager (Bi-Directional)
- **5672**:

  - Purpose: Using for sending and receiving message queue service between Site Manager with Network Sensor and Enterprise Manager.

    - Receiving and sending message from Network Sensor to Site Manager (Uni-Directional and Bi-Directional)
    - Receiving message from Enterprise Manager to Site Manager (Bi-Directional)
- **443:**

  - Purpose: Using for user to perform initial configuration via web console.
  - Communication is secured by TLS 1.3.
  - Authentication: User account credentials.

### [Enterprise Manager](/docs/md-ot-security/installation/whitelist-url-for-ot-security#enterprise-manager)

- **443**:

  - Purpose: For user to work with MD OT Security Enterprise via web console.
  - Communication is secured by TLS 1.3.
  - Authentication: User account credentials.
- **3003**:

  - Purpose:

    - For user to work with MD OT Security Enterprise via web console.
    - For the communication between from Enterprise Manager to Site Manager. (Uni-Directional and Bi-Directional)
- **5673**:

  - Purpose: Using for receiving message queue service from Site Manager (Uni-Directional and Bi-Directional)

### [**Summary of open Ports on MD OT Security components for inbound connections**](/docs/md-ot-security/installation/whitelist-url-for-ot-security#summary-of-open-ports-on-md-ot-security-components-for-inbound-connections)

| **Purpose/ Usage** | **Network Sensor** | **Site Manager** | **Enterprise Manager** |
| --- | --- | --- | --- |
| For users to use/ interact with the component via web console | 443 (main use-case: initial configurations) | 443 (main use-case: initial configurations) | 443 (User’s daily use of MD OT Security via Enterprise Management Console) |
| For the **lower** component to communicate with the component | N/A (There is no MDOTS component under the sensor component) | 3006, 5672 (for Sensors to communicate with Site Manager) | 3003, 5673 (for Site Managers to communicate with Enterprise Manager) |
| For the **upper** component to communicate with the component (only applicable if the communication between the two components is set to **Bi-directional**) | 1443 (For Site Manager to communicate with Sensor) | 3006, 5672 (for Enterprise Manager to communicate with Site Manager) | N/A (There is no MDOTS component above Enterprise Manager) |
| For SSH Access | 22 | 22 | 22 |

### [**Summary of open Ports for outbound connections from MD OT Security components**](/docs/md-ot-security/installation/whitelist-url-for-ot-security#summary-of-open-ports-for-outbound-connections-from-md-ot-security-components)

| **Purpose/ Usage** | **Connection from Network Sensor** | **Connection from Site Manager** | **Connection from Enterprise Manager** |
| --- | --- | --- | --- |
| LDAP Authentication  (For communicating with LDAP Server) |  |  | 636 (secure)  389 (insecure) |
| Integration with NAC  (For communicating with ClearPass Policy Manager Server) |  | 443 |  |
| For Smart Asset Profiling | 80: HTTP for ABB profile  47808: UDP for BACnet/IP profile  80: HTTP for B&R Industrial Automation profile  18245: UDP for Emerson (GE-SRTP) profile  80: HTTP for Emerson (HTTP) profile  44818: TCP for EtherNet/IP profile  5562: TCP Mitsubishi profile  502: TCP for Modbus-TCP profile  34964: UDP for PROFINET IO (DCE/RPC) profile  102: TCP for S7COMM-PLUS profile - Extended  102: TCP for S7COMM profile  161: UDP for SNMP profile |  |  |

## [Notes](/docs/md-ot-security/installation/whitelist-url-for-ot-security#notes)

- Ensure that traffic is allowed for the listed URLs and ports.
- Verify that no intermediate proxies or firewalls block these connections.
- Contact the system administrator or OPSWAT support if additional configuration is required.
