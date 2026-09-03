<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines -->

# Where can I find API documentation and guidelines?

This article applies to all supported versions of the NAC API, the current NAC Enforcer and the Web UI.

API documentation for the latest NAC features will be available via [This Webpage](https://docs.cloud.impulse.com).

Additional guidelines are covered below.

## [Device Enrollment](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#device-enrollment)

NAC supports the enrollment of **MAC addresses** for use in a **RADIUS based enforcement (RBE)** environment.

This feature supports two use cases, namely:

1. When administrators configure an initial role to which devices are assigned as soon as they first enter the system, even before NAC enforcement is applied.

- This serves as a work around for devices that require special set up or do not respond to RADIUS disconnects or VLAN switching.

2. When administrators set the RADIUS server to operate in **Allowlist** mode, where only permitted devices are granted access to the network.

- All other devices will be rejected during the RADIUS transaction, before reaching the NAC enforcement system.
- This setting overlaps with **RADIUS Configuration**, and whether or not an RBE enforcement device uses the MAC address bulk upload as an allowlist is configurable via the **NAC**
- **Dashboard>Configuration>Radius>Configuration** page, by toggling the **Use authorized devices as a whitelist** setting, as shown below.

## [RAML](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#raml)

The following is the RAML document that represents the current state of the API:

#%RAML 1.0
title: Device Enrollment
version: v1
baseUri: https://{safeconnect}/camel/enrollment/{version}
baseUriParameters:
safeconnect:
description: The URL or IP address of your SafeConnect manager, or the single SafeConnect appliance in a standalone configuration.
mediaType: application/json
description: |
API documentation for the SafeConnect Device Enrollment system.
Available since SafeConnect version 6.5.0
uses:
hal : https://bitbucket.org/impulsepoint/raml-docs/raw/master/raml/hal/hal.raml
types:
deviceEnrollment:
type: object
properties:
macAddress: string
role: string
description: string
deviceEnrollmentResource:
type: deviceEnrollment
properties:
_links: hal.selfLink
deviceEnrollmentPage:
type: object
description: A HAL deviceEnrollment page representation
properties:
_embedded: deviceEnrollmentResource[]
_links: hal.halPageLinks
page: hal.halPage
/device:
get:
description: Retrieve a page of enrollment records
is: [hal.paged]
responses:
200:
body:
application/hal+json:
type: deviceEnrollmentPage
example: |
{
"_embedded": {
"deviceEnrollments": [
{
"macAddress": "aabbccddeeff",
"role": "SC_Initial_Role",
"description": "<descriptive text>",
"_links": {
"self": {
"href": "http://127.0.0.1:8096/enrollment/v1/device/aabbccddeeff"
}
}
}
]
},
"_links": {
"self": {
"href": "http://127.0.0.1:8096/enrollment/v1/device"
}
},
"page": {
"size": 20,
"totalElements": 1,
"totalPages": 1,
"number": 0
}
}
post:
description: Save a new enrollment record
body:
application/json:
type: deviceEnrollment
example: |
{
"macAddress": "aabbccddeeff",
"role": "SC_Initial_Role",
"description": "<descriptive text>"
}
responses:
200:
description: New enrollment saved
400:
body:
type: string
description: Describes why the proposed new enrollment isn't valid
409:
body:
type: string
description: Describes the conflict with the proprosed new enrollment
500:
description: An unexpected server error occurred
delete:
description: Delete all enrollments.
responses:
200:
description: All enrollments deleted
500:
description: An unexpected server error occurred
/bulk:
post:
description: Upload a spreadsheet file (csv, xls, xlsx) with enrollment records
body:
multipart/form-data:
properties:
file:
description: The file to be uploaded
type: file
required: true
example: |
mac address,role,description
aabbccddeeff,SC_Initial_Role,<descriptive text>
000000000001,SC_Quarantine_Role,<another enrollment>
responses:
200:
description: New enrollments saved, and existing enrollments updated.
400:
description: Describes why the provided enrollments aren't valid.
500:
description: An unexpected server error occurred
/{macAddress}:
get:
description: Retrieve a specific enrollment record
responses:
200:
body:
application/hal+json:
type: deviceEnrollmentResource
example: |
{
"macAddress": "aabbccddeeff",
"role": "SC_Initial_Role",
"description": "<descriptive text>",
"_links": {
"self": {
"href": "http://127.0.0.1:8096/enrollment/v1/device/aabbccddeeff"
}
}
}
400:
description: If the macAddress path parameter isn't a valid MAC address
404:
description: If the macAddress path parameter doesn't have an enrollment record
put:
description: Update an existing enrollment.
body:
application/json:
type: deviceEnrollment
example: |
{
"macAddress": "aabbccddeeff",
"role": "SC_Initial_Role",
"description": "<descriptive text>"
}
responses:
200:
description: Update processed successfully. After the update, the device enrollment record
400:
description: The proposed update isn't valid
404:
description: The macAddress path parameter doesn't have an enrollment record
409:
description: The proposed update conflicts with another enrollment
500:
description: An unexpected server error occurred
delete:
description: Delete an existing enrollment
responses:
200:
description: Enrollment deleted successfully
400:
description: If the macAddress path parameter isn't a valid MAC address
404:
description: If the macAddress path parameter doesn't have an enrollment record
500:
description: An unexpected server error occurred
## [XML APIs](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#xml-apis)

### [Make An Account](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#make-an-account)

1. Log into the configuration interface with a **Username**/**Password** that has privileges to create user accounts. In the example below, we have created a profile called legacy.

2. Create a new user profile that includes the legacy API privilege. In the example below, the user details are:

- Username: **apiuser**
- Password:**A@p!i12#3**
- Profile: **legacy**

3. Click **Save** to apply your changes and create the user.

Pro Tip:

At this point, the new user can make requests against the **XML API**s. These requests are sent as **HTTP POST**s to [This API](https://auth.impulse.com:8443/impulse.api).

## [Policy group update](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#policy-group-update)

This API should be used to add or remove **Qualifiers** to/from **Policy Groups** in the system.

- This feature may be used to temporarily block or allow access to individual Clients.
- For example, another system may make automated requests to block a client for a violation of security practices.

### [XML structure](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#xml-structure)

1. Credentials:

- **<username>[username]</username>**

  - The username for the user created in the previous step. Do not include the **[]**.
- **<password>[password]</password>**

  - The password for the user created in the previous step. Do not include the **[]**.

2. **<groupName>[Group Name]</groupName>**

- The target group that you want the user added to or removed from.

  - Valid groups include:

    - Block Access
    - Open Access

3. Define only one of the following blocking criteria (leave the other criteria defined, with blank values):

- **<ip>[IP address]</ip>**

  - Enter the IP address of the desired target host.
- **<username>[Username]</username>**

  - Enter the username of the desired target host.
- **<macAddress>[MAC Address]</macAddress>**

  - Enter the MAC address of the desired target host.

4. Optional:

- **<note>[Enter user note]</note>**

  - The **REMARK** keyword followed by any text in the Block Access list will display whatever text is after the **REMARK** keyword to the user.

    - REMARK DMCA Violation #123

      - Will show "DMCA Violation #123" to the client.
- **<expiresInSeconds>[Expiration time]</expiresInSeconds>**

  - Enter the time for which a user will remain in the respective group. When the time is expired, the user is automatically removed from the group, and returned to their normal policy group.

    - Enter "86400" to expire in one day.
  - If no time is entered, the user will be in the desired group until removed manually.
- **<automaticallyManage>[true|false]</automaticallyManage>**

  - If omitted, it defaults to false.
  - Only used when adding qualifiers.

    - **True**

      - Any IP or MAC address qualifiers will be updated as network interfaces change. For example, if a device gets a new IP address through DHCP, the qualifier will update to match. This only applies to the groups “Block Access” and “Open Access”. If another group is used, this behaves the same as “false”.
    - **False**

      - Any IP or MAC address qualifiers will be constant, and will not change to reflect new host data. This is the default if the automatically Manage tag is omitted.

5. Deprecated:

- **<standardOutput>true</standardOutput>**

  - If present, this should be set to "true".
  - If false, formats the output for use in the XML API user interface. This user interface is deprecated.

### [Examples](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#examples)

To add a user with an IP address of 169.0.0.1 to the Block Access group:

<genericPolicyRequest>
<credentials>
<username>apiUsername</username>
<password>apiPassword</password>
</credentials>
<groupDefinitionRequest>
<groupName>Block Access</groupName>
<action>add</action>
<ip>169.0.0.1</ip>
<username/>
<macAddress/>
<note>REMARK - DMCA Violation</note>
<expiresInSeconds/>
<standardOutput>true</standardOutput>
</groupDefinitionRequest>
</genericPolicyRequest>

To remove a user with an IP address of 169.0.0.1 from the Block Access group:

<genericPolicyRequest>
<credentials>
<username>apiUsername</username>
<password>apiPassword</password>
</credentials>
<groupDefinitionRequest>
<groupName>Block Access</groupName>
<action>remove</action>
<ip>169.0.0.1</ip>
<username/>
<macAddress/>
<note>REMARK - Max test</note>
<expiresInSeconds/>
<standardOutput>true</standardOutput>
</groupDefinitionRequest>
</genericPolicyRequest>
### [Return Values](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#return-values)

Successful submissions return the **Success** keyword in the **result** tag. A successful addition to a group will return:

<groupDefResponse>
<result>Success</result>
<action>added</action>
<extra>169.0.0.1</extra>
</groupDefResponse>

A successful removal from a group will return:

<groupDefResponse>
<result>Success</result>
<action>removed</action>
<extra>169.0.0.1</extra>
</groupDefResponse>

Errors return the **Failure** keyword in the **result** tag. A failure due to bad credentials will return:

<apiResponse>
<result>Failure</result>
<action>login</action>
<extra>invalid credentials</extra>
</apiResponse>

A failure to create a duplicate will return:

<groupDefResponse>
<result>Failure</result>
<action>added</action>
<extra>entry already exists,not added again</extra>
</groupDefResponse>
## [Qualifier inquiry](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#qualifier-inquiry)

As of the MetaDefender IT Access 6.1 release, we have a new API to query.

- If a specific **IP**, **Username** or **MAC** address is set up in one of the **Policy Groups** in the system, this API will return the group it belongs to.
- This is useful for allowing other systems to determine which group a Client is in.

Define only one of the following inquiry criteria (leave the other criteria defined, with blank values):

- **<ip>[IP address]</ip>**

  - Enter the IP address of the desired target host.
- **<username>[Username]</username>**

  - Enter the username of the desired target host.
- **<macAddress>[MAC Address]</macAddress>**

  - Enter the MAC Address of the desired target host.

### [Request](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#request)

<qualifierRequest>
<credentials>
<username>testapi</username>
<password>testapi</password>
</credentials>
<qualifierDetails>
<ip/>
<principal/>
<macAddress>00022d85288c</macAddress>
<standardOutput>true</standardOutput>
</qualifierDetails>
</qualifierRequest>
### [Response](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#response)

A search result matching the input will return the following fields:

<qualifierInquiryResponse>
<result>Success</result>
<action>query</action>
<extra>
<ipAddress/>
<macAddress>00022d85288c</macAddress>
<principal/>
<groupLabel>Registered Devices With Policy Key</groupLabel>
</extra>
</qualifierInquiryResponse>

A search result with no matches will return the following:

<qualifierInquiryResponse>
<result>Failure</result>
<action>query</action>
<extra>no information found for the submitted qualifier</extra>
</qualifierInquiryResponse>
## [Guest profile API](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#guest-profile-api)

As of NAC version 6.5.16, the **Guest Profile API** provides access to **retrieve a list of all guest profiles**, as well as the ability to **enable/disable guest profiles by ID**.

- This functionality allows guest profiles to be temporarily disabled, and then enabled again later on.
- For example, a NAC administrator might disable guest profiles over a weekend, and then enable them again on Monday.
- There is no means to disable all guest profiles with a single call, so to disable multiple guest profiles, administrators will need to make separate calls for each profile.

### [Enabling and disabling guest profiles](/docs/manac/nac-v8.1.1/knowledge-base/where-can-i-find-api-documentation-and-guidelines#enabling-and-disabling-guest-profiles)

The following two cURL commands allow administrators with read/write privileges to **enable/disable guest profiles by ID**.

1. Get a list of all guest profiles using an endpoint [Here](https://portal.myweblogon.com:8443/apis/guestProfile).
2. Use the following command to obtain the **guest profile ID** that is necessary to **disable/enable a guest profile**.

- Replace **username** and **password** with the administrative user’s information in the corresponding fields.
- **portal.myweblogon**.com can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

curl GET on /apis/guestProfile
> curl -k --digest --user username:password https://portal.myweblogon.com:8443/apis/guestProfile

3. Enable/disable a guest profile by ID, with the following cURL command.

- To disable, change the portion of the URL that reads **true** to **false**.
- Replace the guest ID in the code block with the ID obtained from the cURL command, to be disabled/enabled.
- Replace **username** and **password** with the NAC administrator’s information in the corresponding fields.
- **portal.myweblogon**.com can be replaced with the IP address of the appliance or the custom hostname of the appliance, if applicable.

curl PUT on /apis/guestProfiles/\{id\}
# Enabled Guest Profile with ID of 42
> curl -k --digest --user username:password -X PUT https://portal.myweblogon.com:8443/apis/guestProfile/42?enabled=true

To enable or disable additional guest profiles, repeat the above process until all guest ID statuses are in their desired states.

Support:

If you have further inquiries, concerns or issues regarding **API Documentation And Guidelines**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
