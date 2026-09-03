<!-- source: https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux -->

# Getting Started with Kiosk Linux

[**My OPSWAT**](https://docs.opswat.com/my/get-started)

My OPSWAT is a unified portal that enables stakeholders: customers, partners, and community users to engage, communicate and do business with OPSWAT.

A My OPSWAT account is necessary to ensure you have the ability to:

- be informed and receive the latest Kiosk updates
- keep communication open with OPSWAT regarding any product questions or requests
- potentially manage Kiosks from your user organization's user account

[**My OPSWAT**](https://docs.opswat.com/product-management/get-started) **/** [**Central Management**](https://docs.opswat.com/ocm/quick-start) **product management**

This is the management server that allows Administrators to manage all deployed Kiosks.

Deployment can be done with an on-premise installation or utilize My OPSWAT to manage Kiosks from the cloud.

The management server allows the ability manage multiple aspects of Kiosk:

- Activate/deactivate a **Volume License**
- Configure Kiosks, either individually or within specified groups
- Provide Kiosk upgrade package hosting
- View detailed session reports
- Dashboard view of aggregated data [session result counts, average scan times, system health] of all Kiosks

[**Kiosk**](https://docs.opswat.com/mdkiosk-linux/setup/product-overview)

This is the hardware appliance unit that users will use to scan their portable media, receive results of their scan, and can transfer media to a secondary destination.

Volume License

The Volume License is the licensing mechanism to allow Kiosk to connect to My OPSWAT or OPSWAT Central Management.

If a Volume License has not been obtained, reach out to [OPSWAT Support](https://www.opswat.com/support) to request a Volume License and provide the Deployment ID of the management server in use.

---

## [Setup Checklist](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#setup-checklist)

1. [Setup a My OPSWAT account](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#setup-a-my-opswat-account)
2. [Setup a management server product](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#setup-a-management-server): [My OPSWAT](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#my-opswat) / [OPSWAT Central Management](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#opswat-central-management)

   1. Obtain and activate a Volume License in the management server
3. [Connect Kiosk to the management server](https://docs.opswat.com/mdkiosk-linux/setup/getting-started-with-kiosk-linux#connect-kiosk-to-the-management-server)

Info

Items 1 & 2 are highly recommended to be done before the Kiosk arrives.

Item 3 can only be done once the Kiosk is received.

---

## [Setup a My OPSWAT account](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#setup-a-my-opswat-account)

Pre-Requisite

Email address to use for signing up.

Goal for successful setup

Successfully login to the [My OPSWAT Portal](https://docs.opswat.com/my/home).

Having a My OPSWAT account is essential to obtain the resources prior to setting up the Kiosk once it arrives and to have access to support when necessary.

Follow the [My OPSWAT guide](https://docs.opswat.com/my/get-started/getting-started) to create your account.

---

## [Setup a management server](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#setup-a-management-server)

Pre-Requisite

Ensure that your My OPSWAT account is created and you can login to the Portal.

Goal for successful setup

Management server is operational and Volume License is activated.

A management server is required to license, configure, and manage Kiosk instances.

There are multiple management products to choose from based on the deployment environment of your organization:

#### [My OPSWAT](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#my-opswat)

My OPSWAT requires no installation and is accessible at [my.opswat.com](https://my.opswat.com/).

- [Activate the Volume License](https://docs.opswat.com/product-management/operating/MD-Kiosk-L-Series-License)

  - If a Volume License has not been obtained, reach out to [OPSWAT Support](https://www.opswat.com/support) to request a Volume License and provide the Deployment ID from `My Products > Settings > License` page
  - Activation is successful when under the `MetaDefender Kiosk L-Series Activation` section, the `Limit` column shows the expected amount of Kiosk instances purchased and the Expires date is set to a time in the future.

- Take note of the [Registration Code](https://docs.opswat.com/product-management/configuration#registration-code)

  - **Server URL** is simply `my.opswat.com`
  - These items are used for connecting a Kiosk to My OPSWAT

Refer to the [My OPSWAT product operation guide](https://docs.opswat.com/product-management/operating/product-dashboard) for more details on how to manage a Kiosk.

#### [OPSWAT Central Management](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#opswat-central-management)

Central Management can be installed on-premise and deployed within your local network.

- [Install](https://docs.opswat.com/ocm/quick-start/installation)

  - Follow the installation guide to install and run through the configuration wizard to perform the basic setup
- [Activate the Volume License](https://docs.opswat.com/ocm/integrations/managing-the-metadefender-kiosk-linux-volume-license)

  - If a Volume License has not been obtained, reach out to [OPSWAT Support](https://www.opswat.com/support) to request a Volume License and provide the Deployment ID from the [License menu](https://docs.opswat.com/ocm/installation/checking-opswat-central-management-license#license-menu)
  - Activation is successful when the `Limit` column shows the expected amount of Kiosk instances purchased and the expiration date is shown.
- Take note of the [Server URL](https://docs.opswat.com/ocm/configuration/setting-up-domain) and Registration Code

  - The Reg Code can be found in `Settings > Global Settings > Account > Registration Code`
  - These items are used for connecting a Kiosk to Central Management

Refer to [Central Management's user guide](https://docs.opswat.com/ocm/integrations/metadefender-kiosk-linux) for more details on how to manage a Kiosk.

---

## [Connect Kiosk to the management server](/docs/mdkiosk-linux/v5.7.4/setup/getting-started-with-kiosk-linux#connect-kiosk-to-the-management-server)

Pre-Requisite

Ensure that the management server & Volume License are activated and that the environment where Kiosk(s) are deployed will be able to connect to the management server.

Goal for successful setup

Kiosk is no longer in Evaluation Mode and can accept media to scan.

Kiosk will start in Evaluation Mode when powered on for the first time.

**Details of Evaluation Mode**

- No management connection

  - No settings can be modified
  - No updates are downloaded
  - No reports are generated or stored
- Only AV engines are used for scanning
- `Scan` and `Scan and Copy to USB` workflows are available for selection when starting a session
- Trial period is set for `120 days`

To unlock the full feature set of Kiosk, connect it to the management server previously setup.

On the Insert Media prompt page in Evaluation Mode, click the `Connect to OCM` button to begin the setup process to connect Kiosk.

Connect to OCM

Info

Once Kiosk is out of Evaluation Mode, it cannot be reverted back to it

Kiosk connection setup begins with choosing the default on-screen language:

Select a language

The Onboarding screen will show next.

Connecting to a management server can be done with two different methods:

- [Ethernet / Wi-Fi Mode](https://docs.opswat.com/mdkiosk-linux/setup/management-via-ethernet---wi-fi-mode) - if the Kiosk will have a direct internet connection to the My OPSWAT / Central Management server
- [Island Mode](https://docs.opswat.com/mdkiosk-linux/setup/management---island-mode) - if the Kiosk will not have any network connection to Central Management

  - Requires at least one Kiosk connected to OPSWAT Central Management through Ethernet / Wi-Fi Mode
