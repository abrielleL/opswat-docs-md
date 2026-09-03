<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configure-eap-ttls -->

# Configure EAP-TTLS

## Introduction

This document describes how to set up Windows Group Policy to allow domain machines to automatically perform 802.1x EAP-TTLS authentication against RADIUS NAC.

## Create RADIUS Clients

1. Log into the **MY OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS NAC**
3. Click on **Edge** Type
4. Click on **RADIUS Clients** tab
5. Click **Add RADIUS Clients** button
   - Provide a name for the Radius Client
   - Select a specific Vendor
   - Enter a **Secret key**
   - Click on **Add**

![](https://uploads.developerhub.io/prod/97qW/2fjnzs4q2590fk8xq035f1n13ivxejhq95ypuy21bu3kjtkfalt3koraa6qoe41m.png)

CIDR Ranges could also be input as:

![](https://uploads.developerhub.io/prod/97qW/2z8cmzpdfdhbgwqo3ev507a8b3hqfwh07b52t9fltl7stc4nmi6yovqlonnae4dv.png)

## Integrate with AD/LDAP

To configure an Authentication Source, refer to [Authentication Sources Setup](https://www.opswat.com/docs/cm/secure-access-solution/authentication-sources-setup).

## Enable EAP-TTLS Authentication

1. Log into the **MY OPSWAT Central Management** console as an administrator
2. Navigate to **RADIUS NAC**
3. Click on the item with **Edge** type
4. Click on **Authentication Methods** tab
5. Click on **Enable Authentication Methods** toggle button

![](https://uploads.developerhub.io/prod/97qW/7cm51ijpg38ph0kfizu20ws27yf0jbppu9e9vufjbootzrnnxxmlxit0fau6elz5.png)

5. Select EAP-TTLS
6. Click on **Add** button and select an LDAP connection

![](https://uploads.developerhub.io/prod/97qW/pwhkupneagev796jrx8vb8ho8oy1yd34fdzvsoobf83l6xjytun5fwhzeawjbjyq.png)

7. One or multiple connection can be selected

![](https://uploads.developerhub.io/prod/97qW/vgr7ehlmx0f82ffe13h0fvpf32v0zpywprwhwck2ilu331fu89bmch21hkkv439c.png)

![](https://uploads.developerhub.io/prod/97qW/mjya0hskycqjwjc3kniqd3yx0ofhi5xkg1ojfbf9ta23pbbgm4qw6as23ig71pl6.png)

8. Click on Save button

## Appy the configuration

Click on **Apply** button to publish the configuration

![](https://uploads.developerhub.io/prod/97qW/unxq0qq2zn2s8eph06slutzyi8fi5og93sy2fwcvq8vler27d4s67lh0r5r5thh4.png)
