<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/netwall/netwall-intro -->

# MetaDefender Security Gateway Introduction

MetaDefender Security Gateway provides unilateral or bilateral inter-zone data transfer and streaming across the zones. The zones are referred to as BLUE (inner) and RED (outer) and are joined by a PCI cable. This cable facilitates the transfer of non-routable data between the zones. No direct network connection exists and no pertinent network information (IP address, MAC address) is exchanged.

The unilateral (USG) and bilateral (BSG) versions of MetaDefender Security Gateway are separate products. MetaDefender Unidirectional Security Gateway transfers data from the BLUE zone to the RED zone only. In addition to all unilateral transfers and streams, MetaDefender Bilateral Security Gateway adds support for bidirectional TCP.

The inner zone (BLUE) corresponds to the network in the customer site that requires protection. The outer zone (RED) is the more public-facing network of the site. Usually, the inner and outer zones are isolated from one another to protect the inner zone.

For example, a water treatment plant would have all its systems in the OT (BLUE) zone. Areas such as Plant Management, Accounting, and Engineering would be in the IT (RED) zone. MetaDefender Security Gateway would pass data in a secure manner from the OT zone to the IT zone.

## [MetaDefender Security Gateway features](/docs/netwall/v5.13.2/netwall/netwall-intro#metadefender-security-gateway-features)

MetaDefender Security Gateway provides the following features:

- No network connection between inner network and outer network
- 1Gbit/sec transfer rate using PCI
- Full Protocol Break: Data Payload Only
- Guaranteed integrity of delivered data
- TPM support

## [MetaDefender Security Gateway components](/docs/netwall/v5.13.2/netwall/netwall-intro#metadefender-security-gateway-components)

MetaDefender Security Gateway consists of the following components:

- MetaDefender Security Gateway BLUE and RED UI: UI used to configure MetaDefender Security Gateway nodes and transfer parameters.
- MetaDefender Security Gateway nodes: Collects and transfers customer data. Each node consists of a 1U server. One node services the BLUE zone (MetaDefender Security Gateway BLUE) and the other services the RED zone (MetaDefender Security Gateway RED).

## [MetaDefender Security Gateway Documentation](/docs/netwall/v5.13.2/netwall/netwall-intro#metadefender-security-gateway-documentation)

The users can consult this web page or, alternatively, they can download the manual in pdf format from the link below:

[NetWall USG-100 manual](https://api.developerhub.io/api/public/version/12418/pdf-download?k=af4471e1cf36b75496c29e3ecd05a717c9cbb5161fd4c58ffb298b20d7c75519) (SHA256: a3149b6812177138945b4f99ed3faf87584a45dbd8fbd52de704d37ee21f01a1).

[OPSWAT NetWall Unidirectional Security Gateway USG-100 Common Criteria Evaluated Configuration Guide](https://metascanbucket.s3.amazonaws.com/opswatnetwall/docs/OPSWAT%20NetWall%20Unidirectional%20Security%20Gateway%20USG-100%20Common%20Criteria%20Evaluated%20Configuration%20Guide%20v1.2.pdf) (SHA256: 3d7441526c6c814f04ed31e058dd4fc7bb01e31c82b44d7ac88df0b0fa07a4a9)

[OPSWAT NetWall USG-100 AGD documentation](https://metascanbucket.s3.amazonaws.com/opswatnetwall/docs/OPSWAT%20NetWall%20USG-100%20AGD%20documentation%20v1.4.pdf) (SHA256: 99bde97972805aee095d3adf35d4f3e3612774078122755e26a5d1ad3ffb126f)
