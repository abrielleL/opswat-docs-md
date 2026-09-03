<!-- source: https://www.opswat.com/docs/mdmediafirewall/setup/getting-started -->

# Getting Started

For MetaDefender Media Firewall (MMF) to operate, it will need the public key of the signing certificate in order validate media processed by Kiosk. The following sections outline the setup process and configuration of the Media Firewall.

## [Setup Steps](/docs/mdmediafirewall/setup/getting-started#setup-steps)

1. Setup Media Manifest usage

   1. [Windows Kiosk](https://docs.opswat.com/mdkiosk/knowledge-base/how-do-i-set-up-a-media-manifest) (`Core` + `Kiosk` sections only)
   2. [Linux Kiosk](https://docs.opswat.com/mdkiosk-linux/configuration#media-manifest)
2. Unpack the MMF

   1. connect the power cable
   2. connect the MMF to a host system via the `COMP` port
3. Power on the MMF - it will immediately start in [Setup Mode](https://docs.opswat.com/mdmediafirewall/setup/getting-started#setup-mode)

   1. Power indicator shows solid GREEN and the USB-A indicator shows flashing RED
   2. `FirewallCfg` drive appears on the Host
4. Drag and drop the public certificate into the drive root

   1. If the certificate is valid and correctly formatted, the USB-A indicator will switch to a solid GREEN display
5. Restart the MMF by powering off & on

Info

Only the certificate is mandatory for setup.

The MMF can be optionally configured to connect to the internet and associated to a `My OPSWAT` account.

Minimum supported Kiosk versions

**Windows Kiosk: 4.6.3**

**Linux Kiosk: 5.5.2**

It is highly recommended to use these Kiosk versions, at a minimum, in order for the reports from Media Firewall to contain accurate information.

---

## [Setup Mode](/docs/mdmediafirewall/setup/getting-started#setup-mode)

Setup Mode provides the ability to configure the MMF and provision the public certificate for validation.

When the MMF is started for the first time, it will automatically start in Setup Mode.

The [USB-A indicator will be flashing red](https://docs.opswat.com/mdmediafirewall/troubleshooting#setup-mode) and a drive named `FirewallCfg` with a `config.ini` file will be displayed when connected to a Host system.

Once the certificate has been approved the MMF will be operational after a power cycle.

Info

Apart from the certificate, all other configuration is optional and the MMF will operate normally if any config is invalid.

Accessing & modifying the configuration can only be done in Setup Mode.

Setup Mode is only accessible on first startup or after a [Factory Reset](https://docs.opswat.com/mdmediafirewall/troubleshooting#system-reset).

---

## [Configuration](/docs/mdmediafirewall/setup/getting-started#configuration)

In Setup Mode, MMF will mount a drive named `FirewallCfg` when connected to a Host.

This drive is used to contain the public certificate for the MMF to validate manifests and a `config.ini` for configuring the firewall.

config.ini

Warning

Renaming or deleting the `config.ini` will result in it reverting back to default configuration

### [[Certificate]](/docs/mdmediafirewall/setup/getting-started#certificate)

This section specifies attributes of the public certificate used to validate a media manifest.

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **Format** | Format of the public certificate | `PEM` | `PEM` - certificate is in PEM format |

### [[Network]](/docs/mdmediafirewall/setup/getting-started#network)

This section allows to connect the MMF to a network.

By connecting the MMF to a network, updates will automatically be retrieved when released and allow the ability for the unit to be centrally managed.

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **Address** | IP address of the unit | `DHCP` | Allowed values:   - `DHCP` - negotiate auto IP configuration - *(ip address)* - static IP will be established - *(empty)* - no connection will be negotiated |
| **NetMask** | 32-bit subnet mask | *(empty)* |  |
| **Gateway** | IP of the network gateway | *(empty)* |  |
| **DNS** | IP of the domain name server | *(empty)* |  |

### [[Management]](/docs/mdmediafirewall/setup/getting-started#management)

This section sets the connection to the Central Management server to view statistics, reports and health details of the MMF.

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **URL** | URL of the management server | *(empty)* | [My OPSWAT](https://docs.opswat.com/my/product-management/enroll-an-instance) is only supported |
| **RegCode** | Registration code of the account | *(empty)* | Log into your My OPSWAT account to obtain your [registration code](https://docs.opswat.com/my/product-management/enroll-an-instance#registration-code) |
| **InstanceName** | Name of the device displayed in the management server | *(empty)* |  |

### [[SecureDataWrite]](/docs/mdmediafirewall/setup/getting-started#securedatawrite)

This section sets the ability to allow copying files from the Host to the media inserted.

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **Enabled** | To enable the feature | `true` | Allowed values:   - `true` - allow copying files from Host to Media - `false` - disallow copying files from Host to Media |

### [[PortAlarmProtection]](/docs/mdmediafirewall/setup/getting-started#portalarmprotection)

This section sets the ability to monitor blocked ports and the connection to the Host. If any disconnect is detected, the Media Firewall will alert.

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **Enabled** | To enable the feature | `false` | Allowed values:   - `true` - allow monitoring and alert - `false` - disallow monitoring and alert |

### [[syslog]](/docs/mdmediafirewall/setup/getting-started#syslog)

| Setting | Description | Default Value | Note |
| --- | --- | --- | --- |
| **ServerEnabled** | Enable sending messages | *(empty)* | Allowed values:   - `true` - allow sending messages - `false` - disallow sending messages |
| **ServerIpAddress** | IP address of the syslog server | *(empty)* |  |
| **ServerPort** | Port of the syslog server | *(empty)* |  |
| **ServerProtocol** | Protocol to utilize for message transmission | *(empty)* | __ Allowed values:   - TCP - `UDP` |

Verify syslog is successfully configured

Upon applying any changes to the syslog configuration, Media Firewall will attempt to log: `Logging to remote syslog configured`.

If this message is seen, the syslog configuration can be confirmed valid and working.

If no message is seen, the Media Firewall's connection may not have to ability to reach the server.
