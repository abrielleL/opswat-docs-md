<!-- source: https://www.opswat.com/docs/md-ot-security/knowledge-base/troubleshoots---common-issues -->

# Troubleshoots - Common issues

#### [System time drift - Stuck at installing a component (Enterprise Manager, Site Bundle, Network Sensor) on the ESXi host](/docs/md-ot-security/knowledge-base/troubleshoots---common-issues#system-time-drift---stuck-at-installing-a-component-enterprise-manager-site-bundle-network-sensor-on-the-esxi-host)

System time drift can lead to fail the installation of MDOTS components. The signal to recognize it is that the installation process is hanging out too long and stop at the screen below.

When the user is stuck at this step, please make sure the current time of the ESXi host is correct.

If Users do not have NTP server, users must set the time correctly with the current UTC time or Local time.

#### [IP address duplication - Unstable connection between MDOTS Components](/docs/md-ot-security/knowledge-base/troubleshoots---common-issues#ip-address-duplication---unstable-connection-between-mdots-components)

The unstable connection between MDOTS Components often happens when the IP address of one of them is duplicated with another device in the same network subnet
