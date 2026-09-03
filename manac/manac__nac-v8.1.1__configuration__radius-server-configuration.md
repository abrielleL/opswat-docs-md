<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/radius-server-configuration -->

# RADIUS Server Configuration

## [Overview](/docs/manac/nac-v8.1.1/configuration/radius-server-configuration#overview)

The following guide covers steps to configure NAC as a RADIUS server. By configuring NAC as a RADIUS server, multiple options become available to the environment:

- A RADIUS authentication server with the ability to support the following authentication types:

  - MAC authentication
  - EAP-PEAP (Direct Active Directory Authentication)
- Ability to conditionally proxy RADIUS server requests to any number of upstream RADIUS servers.
- Ability to assign a specific set of RADIUS attributes on association. The specific attributes available will depend on the vendor that is chosen and can include:

  - VLAN assignments
  - Vendor specific profiles or roles
  - ACL names
- Ability to perform enforcement actions using just the RADIUS NAS device.

## [NAC Installation](/docs/manac/nac-v8.1.1/configuration/radius-server-configuration#nac-installation)

If you have not configured your NAC appliance with an IP address and confirmed access to the proactive Impulse Management Services, please contact Support at [opswat.com/support](https://opswat.com/support/)

Step 1: [NAC RADIUS Server Authentication Mode Configuration](/docs/manac/nac-v8.1.1/configuration/radius-server-authentication-mode-configuration)

Step 2: [NAC RADIUS Clients Configuration](/docs/manac/nac-v8.1.1/configuration/radius-clients-configuration)

Step 3: [NAC RADIUS Network Environment Configuration](/docs/manac/nac-v8.1.1/configuration/radius-network-environment-configuration)

Step 4: [NAC Roles for use with RADIUS](/docs/manac/nac-v8.1.1/configuration/roles-for-use-with-radius)

Troubleshooting: [NAC RADIUS Troubleshooting](/docs/manac/nac-v8.1.1/configuration/radius-logs-for-troubleshooting)
