<!-- source: https://www.opswat.com/docs/manac/installation/remote-access-requirements -->

# Remote Access Requirements

The Access Requirements below are used to facilitate installation, testing, training, support, monitoring, backups and upgrades of your NAC Appliance(s).

- Allow outbound ssh (port 22) to below resources from host x.x.x.x (NAC Appliance Private IP):

  - FQDN: **nac-ca1.opswat.com**

    - IP Address: 52.1.227.222/32
  - FQDN: **nac-ca2.opswat.com**

    - IP Address: 52.4.162.8/32
  - FQDN: **nac-downloads.opswat.com**

    - IP Address: 34.192.23.191/32
- Allow outbound https (port 443) to below resources from host x.x.x.x (NAC Appliance Private IP):

  - FQDN: **gears.opswat.com**
- Allow outbound HTTP/HTTPS (port 80 and 443) to below resources from host x.x.x.x (NAC Appliance Private IP):
- - Service Name: Amazon Web Services (Appliance Configuration Backups)
  - Resources:

    - 52.92.16.0/20
    - 52.216.0.0/15
    - 54.231.0.0/17
- Allow outbound for following services from host x.x.x.x (NAC Appliance Private IP):

  - Services: HTTPS, DNS, NTP

Warning

Allowing outbound TCP/22 connection from the NAC virtual appliance to 52.1.227.222 and 52.4.162.8 will permit it to establish reverse SSH tunnels that allow OPSWAT to gain remote SSH access to your appliance. While OPSWAT will only use this access with regard to an active support case or project (e.g. initial implementation or upgrades), you may wish to remove our *ability* to access your appliance outside these time frames for security reasons. To do this, simply block outbound TCP/22 connections from your appliance’s private IP in your network’s firewall.

**NOTE** - If you opt to block outbound TCP/22 connections from your NAC, it may take up to 1 hour for your NAC to re-establish a reverse SSH tunnel to our remote access servers once these connections are allowed again (e.g. when requesting remote support).

If any questions arise please contact your OPSWAT Deployment Engineer or OPSWAT Support.
