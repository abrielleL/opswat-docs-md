<!-- source: https://www.opswat.com/docs/metadefender-ot-access/2.3.0/knowledge-base/secure-ot-access---on-prem-iso-installation -->

# MetaDefender OT Access - On-Prem ISO Installation

## [Prerequisites](/docs/metadefender-ot-access/2.3.0/knowledge-base/secure-ot-access---on-prem-iso-installation#prerequisites)

- Secure OT Access ISO
- License file
- USB pen
- Cable: serial port to laptop

BashCopylsblk (note partition)
dd if=/dev/zero of=/dev/((partition)) bs=1M count=1000
sudo poweroff
#### [ISO Installation](/docs/metadefender-ot-access/2.3.0/knowledge-base/secure-ot-access---on-prem-iso-installation#iso-installation)

Steps to install Secure OT Access:

1. Make a bootable USB pen with a MetaDefender OT Access ISO (NAS_US:/builds/development/singlekey6/appliance/otfuse), we recommend rufus software to do so. MetaDefender OT Access ISOs can be downloaded from my.opswat.com.
2. Turn on MetaDefender OT Access appliance with the pen and connected through serial port.
3. When CLI is up, after inserting user and password, type _devicebuilder and select the Secure OT Access SKU option corresponding with your hardware or your VM, then accept when requested.
4. Type halt, and wait until it shuts down (NOT reboot).
5. Remove pen and serial port, connect Secure OT Access to your network through port 0 *(In case using Virtual Machine, please disconnect the ISO)* and turn it on again.
6. Access to 10.10.10.10:8443 using a browser connected to the same network and include license.
7. Configure Management IP in Network settings and reboot appliance.
8. Configure Service IP in Network settings.
9. Secure OT Access Management console should be ready in the IP you just configured, in port 443.
