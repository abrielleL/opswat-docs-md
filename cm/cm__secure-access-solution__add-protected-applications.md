<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications -->

# Add Protected Applications

> **Info**
>
> This feature requires a premium My OPSWAT Central Management License.

This section guides you through a workflow to protect your applications with SDP method. For testing purposes, OPSWAT hosts a demo application at [demo.sdp.opswat.com](http://demo.sdp.opswat.com)

- [Add Protected Application](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications#add-protected-application)
  - [Secure IT Access Method](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications#secure-it-access-method)
  - [idP Method](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications#idp-method)
- [User Assignment](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications#user-assignment)
- [Gateways](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications#gateways)

## Before You Begin

You will need to ensure that **Enable Secure Access** is checked off. This can be found in **Secure Access > Protected Apps**.

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Add Protected Application

Click **Add Protected Application**, then choose your preferred method.

![](https://uploads.developerhub.io/prod/97qW/hn5yo3aryoxa1k168792frvowj5sx6z7p0kfswb0qockf0dza08a9095g84nhuet.png)

### Secure IT Access Method

Select** Secure IT Access Method** to begin.

![](https://uploads.developerhub.io/prod/97qW/9voxvzivsjvtyyjqgdarjdlluc9gjxa7n9qfj08d976hw7v319qq8jgu9oi3829s.png)

| Configuration | Details |
| ---- | ---- |
| **Application Name** | This name will be shown to your end-users |
| **Access Mode** | - **Disable**: the system will always allow an authorized users to access the application without processing access rules on your account - **Monitor**: the system will process access rules but will always allow an authorized users to access the application without processing access rules on your account - **Enforce**: the system will process access rules to decide if the system grants an authorized users access to the application |
| **Application Type** | Select **Web Application** or **SSH, RDP, or Other** - For **SSH, RDP, or Other** types of applications, My OPSWAT Central Management allows administrators to add up to 1,000 addresses to the protected application. For more information on bulk uploading addresses, please refer to [Bulk Upload](https://www.opswat.com/docs/cm/secure-access-solution/bulk-upload) |
| **Addresses** (for** SSH, RDP, or Other**) | Each address can be an IPv4 or IPv6 address, range or CIDR block, or a domain: - **IPv4**: `10.20.0.50`, `10.20.0.1-10.20.0.254` or `10.20.0.0/24` - **IPv6**: `2001:db8:20::50`, `2001:db8:20::1-2001:db8:20::ff` or `2001:db8:20::/64` - **Domain**: `erp.example.com` An application can list IPv4 and IPv6 addresses together |
| **Application URL **(for **Web Application**) | Where the application is hosted |
| **Ports** | Ports the application is running |
| **Allow ICMP Traffic** | Check **Allow ICMP Traffic** if you allow devices send ICMP traffic to the application |
| **Visible to Users**  | Check **Visible to Users** if you want to users to see the applications listed in the SDP section of the OPSWAT Client. Hidden applications will still be accessible to users according to your access rules |

Note: For commonly used applications, please refer to [Common Used Applications](https://www.opswat.com/docs/cm/secure-access-solution/common-used-applications) guideline.

### idP Method

To protect applications with the IdP Method, you can refer [Add Protected Applications with IdP Method.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)

## User Assignment

- Assign who can access to this application. This step can be skipped and do later. Refer [Assign Users/Groups to a Protected Application](https://www.opswat.com/docs/cm/secure-access-solution/assign-users-groups-to-a-protected-application) for more details.
- Click the arrow icon to add to the selected Users/Groups lists to grant end-users/IdP groups access to the applications.
- Click **Assign.**

## Gateways

- You may be asked to set up a SDP Gateway if you have not set up SDP Gateway, please refer [Set Up Gateways](https://www.opswat.com/docs/cm/secure-access-solution/set-up-gateways) for more details.
- Configure your firewall/proxy to lock the application down so only SDP Gateways can reach your application. Allow each gateway's IPv4 address for IPv4 applications and its IPv6 address for IPv6 applications. Both are shown in the Gateway Configuration Tool under **[F7] Network Info**.

  Note A gateway reaches an application over the same IP version as the application's address. To protect IPv6 applications, assign them to gateways that have IPv6 configured.

- Assign what gateways can access to this application. This step can be skipped and do later.
- Click the arrow icon to add the selected gateway(s) to the access list for applications.
- Click **Assign.**

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
