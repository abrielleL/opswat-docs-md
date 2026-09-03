<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/ldap-ad-authentication -->

# LDAP/AD Authentication

Authentication sources are used to determine valid user credentials and collect group memberships. Configuring an LDAP sources is required if there is a need to assign RADIUS attributes, such as VLAN assignment, outside of the NAC Policy engine. If the RADIUS server is integrated with AD for EAP-PEAP authentication, a separate LDAP connection must still be defined for this functionality to work. This requirement is present as the Direct Active Directory integration is not able to perform the level of group lookups required for this functionality.

## Steps by Steps configuration

### Create Authentication Sources

Refer to [Authentication Sources Setup ](https://www.opswat.com/docs/cm/secure-access-solution/authentication-sources-setup)for more details.

### Setup Rules for Web Authentication

On **RADIUS NAC** > **Rule**, define a Rules for authentication as below:

![](https://uploads.developerhub.io/prod/97qW/aep0xm9kn8bpp0vng9c85vmht16pw6emt9z8gq3qa0yydxdph184uylh6gev33gz.png)

### Select Web Authentication Sources

1. Navigate to **RADIUS NAC** > **RADIUS Configuration** > Select your **Edge** type
2. Select **Web Authentication Sources**
3. On **AD/LDAP Server Connections**, select **Guest User Database**
4. Select an **Authentication Source** (multiple sources can be selected)
5. Click on **Save**

![](https://uploads.developerhub.io/prod/97qW/u1kj87aqa6zg1qaze7ok63pmsm7jh280qt5pou8ftpt9fiyx6wcsqigzwu2yfgqh.png)
