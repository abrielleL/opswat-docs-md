<!-- source: https://www.opswat.com/docs/netwall/5.14.0/configuration/iccp-connector -->

# ICCP Connector

ICCP (Inter-Control Center Communications Protocol) is a standard communication protocol used in the field of energy management and control systems for supervisory control and data acquisition applications. The ICCP protocol is primarily designed to facilitate information exchange between different control centers or SCADA systems in the energy industry.

ICCP Connector allows you to transfer ICCP data unilaterally across MetaDefender Security Gateway. ICCP Connector should be configured on the MetaDefender Security Gateway BLUE and RED nodes.

The OPSWAT ICCP connector on MetaDefender Security Gateway BLUE collects data from ICCP Servers in the BLUE zone and transfers that data to the OPSWAT ICCP connector configured on MetaDefender Security Gateway RED. An ICCP server the RED zone can be connected to the OPSWAT ICCP connector to monitor the transferred data.

### [Security Gateway BLUE](/docs/netwall/5.14.0/configuration/iccp-connector#security-gateway-blue)

Important

To configure ICCP Connector, a security dongle should be inserted in the BLUE server.

After login in MetaDefender Security Gateway BLUE, go to ICCP menu in Connectors section, deploy Action button and select Add Client.

1. Type values in the following boxes:

   1. **Channel:** Channel of the ICCP stream, this should be the same channel in both sides, RED and BLUE.
   2. **Server IP:** IP address of the ICCP Server MetaDefender Security Gateway BLUE will connect to collect data from.
   3. **Server Port:** TCP port number where the ICCP server is listening on. Default value is 102 or 3782 if using TLS.
   4. **Major Version:** ICCP Specification version (Major). Default value is 2014.
   5. **Minor Version:** ICCP Specification version (Minor). Only version 8 is supported.
   6. **Scan (ms):** Scan rate in miliseconds. Default value is 1000 ms, accepted values are from 100 to 604800000 ms.
   7. **ISO 8073/X.224 Connection Oriented Transport Protocol:**

      1. **Source TSAP:** Source Transport Service Access Point hexadecimal value. The maximum length for this field is 510 hex chars.
      2. **Destination TSAP:** Destination Transport Service Access Point hexadecimal value. The maximum length for this field is 510 hex chars.
      3. **TPDU Size:** Transaction Protocol Data Unit size. Default value is 1024.
   8. **ISO 8327-1 OSI Session Protocol:**

      1. **Calling Session Selector:** Session Protocol Calling Session Selector hexadecimal value. The maximum length for this field is 510 hex chars.
      2. **Called Session Selector:** Session Protocol Called Session Selector hexadecimal value. The maximum length for this field is 510 hex chars.
   9. **ISO 8823 OSI Presentation Protocol:**

      1. **Calling Presentation Selector:** Presentation Protocol Calling Presentation Selector hexadecimal value. The maximum length for this field is 510 hex chars.
      2. **Called Presentation Selector:** Presentation Protocol Called Presentation Selector hexadecimal value. The maximum length for this field is 510 hex chars.
   10. **ISO 8650-1 OSI Association Control Service Element:**

       1. **Calling AP Title:** Calling Application Process Title Object Indentifier. Maximum lenght for this field is 32 chars.
       2. **Calling AE Qualifier:** Calling Application Entity Qualifier. Valid values are from 0 to 65535.
       3. **Calling AP Invocation Identifier:** Calling Application Process Invocation Identifier. Valid values are from 0 to 65535.
       4. **Calling AE Invocation Identifier:** Calling Application Entity Invocation Identifier. Valid values are from 0 to 65535.
       5. **Called AP Title:** Called Application Process Title Object Indentifier. Maximum lenght for this field is 32 chars.
       6. **Called AE Qualifier:** Called Application Entity Title Object Indentifier. Maximum lenght for this field is 32 chars.
       7. **Called AP Invocation Identifier:** Called Application Process Invocation Identifier. Valid values are from 0 to 65535.
       8. **Called AE Invocation Identifier:** Called Application Entity Invocation Identifier. Valid values are from 0 to 65535.
   11. **Encryption:** Deploy the dropdown list to select no encryption or TLS.

       1. TLS Layer

          1. **CA Certificate:** MetaDefender Security Gateway needs a CA certificate to verify the authenticity of the ICCP server certificate. You can import CA certificates in Advanced -> Encryption -> X509 Certificates.
          2. **Client Certificates:** Select the certificate that the ICCP Client will use on TLS Layer. You can generate or import certificates in Advanced -> Encryption -> SSL/TLS Credentials.
          3. **Depth:** Maximum depth of the certificate chain to be verified during the TLS authentication process. Default value is 10, valid values are from 1 to 255.
       2. MMS Layer

          1. **CA Certificate:** MetaDefender Security Gateway needs a CA certificate to verify the authenticity of the ICCP server certificate. You can import CA certificates in Advanced -> Encryption -> X509 Certificates.
          2. **Client Certificates:** Select the certificate that the ICCP Client will use on MMS Layer. You can generate or import certificates in Advanced -> Encryption -> SSL/TLS Credentials.
          3. **Depth:** Maximum depth of the certificate chain to be verified during the MMS authentication process. Default value is 10, valid values are from 1 to 255.
   12. **Description:** User friendly description of the configured ICCP client.
   13. **Enabled:** Check/Uncheck this checkbox to enable/disable the client.
2. Click on Submit button to save the changes.

### [Security Gateway RED](/docs/netwall/5.14.0/configuration/iccp-connector#security-gateway-red)

Important

To configure ICCP Connector, a security dongle should be inserted in the RED server

After login in MetaDefender Security Gateway RED, go to ICCP menu in Connectors section, deploy Action button and select Add Server.

1. **Type values in the following boxes:**

   1. **Channel:** Channel of the IEC 104 stream, this should be the same channel in both sides, RED and BLUE.
   2. **Server Port:** TCP port number where the ICCP server will be listening on. Default value is 102 or 3782 if using TLS.
   3. **Major Version:** ICCP Specification version (Major). Default value is 2014.
   4. **Minor Version:** ICCP Specification version (Minor). Only version 8 is supported.
   5. **Scan (ms):** Scan rate in miliseconds. Default value is 1000 ms, accepted values are from 100 to 604800000 ms.
   6. **Allowed Clients (IPs or range):** IP address, addresses or IP range of the clients allowed. IPs should be separated by semicolon. Leave it blank for any.
   7. **ISO 8073/X.224 Connection Oriented Transport Protocol:**

      1. **Destination TSAP:** Destination Transport Service Access Point hexadecimal value. The maximum length for this field is 510 hex chars.
      2. **TPDU Size:** Transaction Protocol Data Unit size. Default value is 1024.
   8. **ISO 8327-1 OSI Session Protocol:**

      1. **Session Selector:** Session Selector hexadecimal value. Maximum lenght for this field is 510.
   9. **ISO 8823 OSI Presentation Protocol:**

      1. **Presentation Selector:** Session Selector hexadecimal value. Maximum lenght for this field is 510.
   10. **ISO 8650-1 OSI Association Control Service Element:**

       1. **AP Title:** Application Process Title Object Indentifier. Maximum lenght for this field is 32 chars.
       2. **AE Qualifier:** Application Entity Title Object Indentifier. Maximum lenght for this field is 32 chars.
       3. **AP Invocation Identifier:** Application Process Invocation Identifier. Valid values are from 0 to 65535.
       4. **AE Invocation Identifier:** Application Entity Invocation Identifier. Valid values are from 0 to 65535.
   11. **Encryption:** Deploy the dropdown list to select no encryption or TLS.

       1. **TLS Layer**

          1. **CA Certificate:** MetaDefender Security Gateway needs a CA certificate to verify the authenticity of the ICCP client certificate. You can import CA certificates in Advanced -> Encryption -> X509 Certificates.
          2. **Client Certificates:** Select the certificate that the ICCP Server will use on TLS Layer. You can generate or import certificates in Advanced -> Encryption -> SSL/TLS Credentials.
          3. **Depth:** Maximum depth of the certificate chain to be verified during the TLS authentication process. Default value is 10, valid values are from 1 to 255.
       2. **MMS Layer**

          1. **CA Certificate:** MetaDefender Security Gateway needs a CA certificate to verify the authenticity of the ICCP client certificate. You can import CA certificates in Advanced -> Encryption -> X509 Certificates.
          2. **Client Certificates:** Select the certificate that the ICCP Server will use on MMS Layer. You can generate or import certificates in Advanced -> Encryption -> SSL/TLS Credentials.
          3. **Depth:** Maximum depth of the certificate chain to be verified during the MMS authentication process. Default value is 10, valid values are from 1 to 255.
   12. **Description:** User friendly description of the configured ICCP client.
   13. **Enabled:** Check/Uncheck this checkbox to enable/disable the client.
2. Click on Submit button to save the changes.
