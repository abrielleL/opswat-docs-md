<!-- source: https://www.opswat.com/docs/netwall/5.14.0/configuration/md-core-integration -->

# MetaDefender Core Integration

The MetaDefender Security Gateway (USG & BSG) can be configured to integrate with an external instance of the MetaDefender Core Advanced Threat Prevention Solution. MD Core stops file-borne threats, including ransomware, zero-day exploits, and embedded malware, before they reach users or systems. It integrates seamlessly into existing infrastructure, securing uploads, downloads, email attachments, and file transfers without disrupting workflows. MD Core must be purchased separately from the Security Gateway.

Info

The MetaDefender Security Gateway / MetaDefender Core integration is supported on the BLUE side only.

A security dongle must be inserted in the BLUE side to change configuration.

## [Security Gateway BLUE](/docs/netwall/5.14.0/configuration/md-core-integration#security-gateway-blue)

This section describes configuration of the Optical Diode BLUE to communicate with an external instance of MD Core.

### [Initial Configuration](/docs/netwall/5.14.0/configuration/md-core-integration#initial-configuration)

Navigate to **MetaDefender Core -> Connection**. Fill in the following fields:

1. **URL:** Path to external MD Core
2. **API Key:** API Key for authorized access to MD Core
3. **Timeout**: the maximum duration the Optical Diode maintains an idle TCP connection in its state table before closing it. Default = 60.
4. **Test Connection**: Press to confirm whether the connection to MD Core is successful.
5. **Enabled:** Click check box to enable communication with MD Core.
6. **Block Empty Files:** Block zero byte files
7. **Submit:** Press Submit to save configuration.

MD Core Configuration
