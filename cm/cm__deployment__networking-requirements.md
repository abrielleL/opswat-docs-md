<!-- source: https://www.opswat.com/docs/cm/deployment/networking-requirements -->

# Networking Requirements

To ensure proper communication between product instances and the My OPSWAT Central Management (CM10), the following **domain names (URLs) and ports** must be allowed through your **firewall** or **proxy**.

## Outbound Connections (from Customer Network to CM10 server)

| Purpose | Protocol | Port | Domains |
| ---- | ---- | ---- | ---- |
| Product instances connect to CM10 | HTTPs | 443 | product.my.**<tenant ID>**.opswat.com *Ex: product.my.us.opswat.com* |
| Product updates | HTTPs | 443 | please refer [Product Updates Domains](https://www.opswat.com/docs/cm/knowledge-base/product-updates-domains) |
| Administrators can access CM10 console | HTTPs | 443 | my.opswat.com my.**<tenant ID>**.opswat.com *.opswatgears.com *Ex: my.us.opswat.com* |
| MetaDefender Endpoint communication | HTTPs | 443 | gears.opswat.com (if endpoints connect to United States tenant) gears-eu.opswat.com (if endpoints connect to Europe tenant) |
| MetaDefender Cloud (if MetaDefender Endpoint scans files with MetaDefender Cloud) | HTTPs | 443 | api.metadefender.com |
| CDN | HTTPs | 443 | opswat-gears-cloud.s3-us-west-2.amazonaws.com opswat-gears-cloud-clients.s3-us-west-2.amazonaws.com opswat-gears-fetch-log.s3.amazonaws.com softwareopswat-a.akamaihd.net |

## My OPSWAT Central Management Tenants

| Tenant Location | Tenant ID |
| ---- | ---- |
| United States | us |
| Europe | eu |
