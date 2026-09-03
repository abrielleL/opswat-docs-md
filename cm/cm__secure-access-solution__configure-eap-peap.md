<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configure-eap-peap -->

# Configure EAP-PEAP

## Introduction

This document describes how to set up EAP-PEAP (Protected Extensible Authentication Protocol). This setup is essential for organizations seeking to enhance their network security while enabling seamless user access.

To configure EAP-PEAP authentication, follow these steps:

## Prepare the Network Infrastructure

Ensure that your wireless access points (APs) and switches are compatible with EAP-PEAP.

## Create RADIUS Clients

1. Log into the **My OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS NAC**
3. Click on a specific **Edge** type
4. Click on **RADIUS Clients** tab
5. Click **Add RADIUS Clients** button
   - Provide a name for the Radius Client
   - Select a specific Vendor
   - Enter a **Secret key**
   - Click on **Add**

![](https://uploads.developerhub.io/prod/97qW/xia66bw4bl8e7vvjk60ggyfkpn8c1g7y0m47atpzrt1i3ppiwwyuhvni74u8w44c.png)

## Enable EAP-PEAP Authentication

1. Log into the **My OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS** **NAC**
3. Click on the **Edge** Type
4. Click on **Authentication Methods** tab
5. Click on **Enable Authentication Methods** toggle button

![](https://uploads.developerhub.io/prod/97qW/c8sexjctq7b73sre837hk2x1iu9u5u2afisstt7szz2qjuhtp6e0ntc0fona328e.png)

5. Select **EAP-PEAP**
6. Input your Active Directory credentials in order to join the domain:

- Domain: The full domain of your Active Directory environment (examples: com, [sub.domain.net](http://sub.domain.net/), domain.local).
- Workgroup: This is the workgroup name of your domain
- Active Directory Domain Controller: The FQDN of the domain controller that NAC will authenticate against
- NetBIOS Name**:** This is the name NAC will use as the machine name when it registers itself in Active Directory
- Username: The username of a Domain Admin or other user with rights to join devices to the domain (Least Privilege account could be used)
- Password: The password corresponding to the given username
- Confirm Password: The password corresponding to the given username

![](https://uploads.developerhub.io/prod/97qW/wt9acdgiqo2fhk2arycua2sgfvsti9h5rhf6c3x9e1xkqt92uqhohu0v8ejxx7rr.png)

7. Save changes.

## Apply the configuration

![](https://uploads.developerhub.io/prod/97qW/g2w7oxznbscxignzi1enurk1dg850tc83ehwzz3tzyz3fuux93yvazq5bqiacmya.png)

Click on the **Apply** button at the upper right corner of the screen.
