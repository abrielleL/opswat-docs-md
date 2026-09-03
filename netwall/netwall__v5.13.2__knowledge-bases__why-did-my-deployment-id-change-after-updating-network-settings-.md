<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/knowledge-bases/why-did-my-deployment-id-change-after-updating-network-settings- -->

# Why Did My Deployment ID Change After Updating Network Settings?

This article applies to all NetWall products running versions earlier than USG/BSG 5.12, Optical Diode 1.12, TG 1.8.0 (older OS), and TG 2.3.0 (RHEL-based OS).

Under certain conditions, changes to system network settings can cause the Deployment ID to change unexpectedly. The Deployment ID is influenced by the following system attributes:

1. Host name
2. Default gateway interface

Any change to either of these can result in a new Deployment ID being generated as the system is treated as a new deployment. Note that changing the Management IP solely does not affect the existing Deployment ID.

This behavior is expected in older software versions.

With new versions of NetWalls below, changing the default gateway should not impact the deployment ID.

| Product | Version |
| --- | --- |
| USG / BSG | 5.12 |
| Optical Diode | 1.12 |
| TG (older OS) | 1.8.0 |
| TG (RHEL-based OS) | 2.3.0 |

Systems running versions prior to this update may still experience Deployment ID changes when the default gateway interface or host name is modified.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
