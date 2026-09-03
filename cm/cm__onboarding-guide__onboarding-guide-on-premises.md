<!-- source: https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises -->

# Onboarding Guide (On-Premises)

This onboarding guide aims to help you get familiar with My OPSWAT Central Management platform, enroll MetaDefender products, navigate core functions, and manage your account with maximum efficiency.

- [Pre-Onboarding Setup](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#pre-onboarding-setup)
  - [Check System Requirements](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#check-system-requirements)
  - [Download Installation Package](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#download-installation-package)
  - [Install My OPSWAT Central Management](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#install-my-opswat-central-management)
  - [Setup Wizard](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#setup-wizard)
- [Getting Started](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#getting-started)
  - [Enroll Products](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#enroll-products)
  - [Navigate Core Functions](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#navigate-core-functions)
  - [Manage Your Account](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#manage-your-account)

## Pre-Onboarding Setup

Complete these steps to prepare your environment and install My OPSWAT Central Management.

### **Check System Requirements**

Verify that your server meets the minimum specifications to deploy My OPSWAT Central Management On-premises. Refer to the [System Requirement](https://www.opswat.com/docs/cm/deployment/system-requirements) guideline for more details.

### **Download Installation Package**

Once your server is ready, the next step is to obtain the My OPSWAT Central Management installation files.

- Log into the [My OPSWAT Portal](https://my.opswat.com).
- In the left-side menu, click **Product Downloads**.
- Search or scroll for **My OPSWAT Central Management** to open the product details page.
- Click **Download**, then select the specific system and version you need.

![](https://uploads.developerhub.io/prod/97qW/bzqwohxvsaealun2yug9bnc38ggcnbksebnola0c1o7g7andnc1xydrtb0ulyb48.png)

### **Install My OPSWAT Central Management**

Choose the procedure that matches your infrastructure:

- For Windows: Follow [MSI Installation - Standalone mode](https://www.opswat.com/docs/cm/deployment/msi-installation) guideline for detailed instructions.
- For Linux:  Follow [RPM Installation](https://www.opswat.com/docs/cm/deployment/rpm-installation) guideline for detailed instructions.
- For OVA: Follow [Virtual Appliance Deployment](https://www.opswat.com/docs/cm/deployment/virtual-appliance-deployment) guideline for detailed instruction.
- For AWS: Follow [Deployment with AWS](https://www.opswat.com/docs/cm/deployment/deployment-with-aws) guideline for detailed instruction.

### **Setup Wizard**

Once the installation is finished, the Setup Wizard will walk you through the final configuration steps to register your account and get your console live. Please follow the [Setup Wizard ](https://www.opswat.com/docs/cm/deployment/setup-wizard#setup-wizard-with-the-new-setup)guideline to complete the process.

![](https://uploads.developerhub.io/prod/97qW/gk5ixck84fu3w7201y84vn67ltm2eh367gs4ucse8ibl6vqk2zg35m7f6eqdfax1.png)

## Getting Started

Steps to execute once your environment is ready and your console is active.

### **Enroll Products**

Enrollment connects your distributed MetaDefender products to My OPSWAT Central Management console. Select the specific enrollment workflow for your product:

- [Enroll MetaDefender Kiosk](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk)
- [Enroll MetaDefender Endpoint](https://www.opswat.com/docs/cm/product-management/metadefender-endpoint)
- [Enroll other Products](https://www.opswat.com/docs/cm/product-management/other-products)

Once enrollment is complete, head over to the **Inventory** tab where you can view and manage all enrolled assets.

### **Navigate Core Functions**

This section outlines the core functions available to help you view, monitor, and manage your environment effectively.

#### **Dashboard**

Gain near real-time insights into your security posture through specialized dashboards. Instead of digging through logs, you get a clear, intuitive visual of what’s happening across your infrastructure.

![](https://uploads.developerhub.io/prod/97qW/fwi98n2um4fm9osd8t0rsgdv1buv9ezbjynrun00r495fmsqu5f5ea6qoam898h6.png)

- [Peripheral Media Protection Dashboard:](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection) Monitors the security lifecycle of removable media across your Kiosk, Media Firewall, and Endpoint network to prevent physical-entry threats.
- Endpoint Security Dashboard: Monitor device posture checks, track OS update status, and identify non-compliant devices.
- [Hardware Supply Chain Dashboard:](https://www.opswat.com/docs/cm/product-management/hardware-supply-chain) Secure your hardware lifecycle by identifying vulnerable hosts and tracking supply chain integrity across your MetaDefender Drive deployments.
- [File Security Protection Dashboard](https://www.opswat.com/docs/cm/product-management/file-security-protection): Centralizes statistics and data from your MetaDefender Core and MetaDefender ICAP, ensuring file-processing security measures are performing effectively.
- Industrial FirewalI Dashboard: Centralize the configuration and management of MetaDefender Industrial Firewall deployments across OT environments.

#### **Inventory**

The **Inventory** serves as the centralized warehouse for every service, device, and application in your environment. Use this function to view real-time health status, track event logs, and organize assets into Groups for streamlined management.

Refer to the [Inventory](https://www.opswat.com/docs/cm/product-management/inventory) guideline for a full walkthrough of every filter, view, and action available.

![Inventory delivers both high‑level visibility and detailed drilldowns across connected services and devices.](https://uploads.developerhub.io/prod/97qW/xvuch37vg657va194fw5of2u37gz8mnhkqdk0fr2ujcvwhv4iljszfzehl81fp2r.png)

#### **Policies**

The Policies function allows you to define and enforce security standards and push them out to all your devices at once. It ensures every instance is following the same security rules without manual effort.

Refer to the [Policies Management](https://www.opswat.com/docs/cm/product-management/overview-policy-management) guideline for detailed configuration steps.

![](https://uploads.developerhub.io/prod/97qW/h2v9ag81kl36ys8yk900mdbgd2scxgatgy0yiginrh43avx0g6d1kaxmmel2g32w.png)

#### **Settings**

Fine-tune your platform-wide configurations by navigating to the **Settings** tab.

Refer to the [Global Settings](https://www.opswat.com/docs/cm/configurations/global-settings) guideline for more details on the settings you can customize to tailor your account to your needs.

![](https://uploads.developerhub.io/prod/97qW/nf9tfnoh4c76jckix6pvtxodoefe2tvfga0f03d3jmgm7v5j47pq77vu6pgq64kh.png)

### **Manage Your Account**

Keep your platform running efficiently with these administrative workflows.

#### **Users & Roles**

Provision console users and define granular access levels.

- To provision users who will access the My OPSWAT Central Management console, refer to the [Provision Users](https://www.opswat.com/docs/cm/user-management/provision-users#invite-a-console-user) guideline.
- To create a customized level of access for console users, follow the [Role Management](https://www.opswat.com/docs/cm/user-management/role-management) guideline.

![](https://uploads.developerhub.io/prod/97qW/byduhdtayek4edey3zxuqiv6wwta47dy8x484a5vkfe6mvlhem1bprvxx8bi58z6.png)

#### **Server Configuration**

Refer to the [Server Configuration](https://www.opswat.com/docs/cm/configurations/server) guideline for detailed instructions on how to configure server settings.

#### **Product Updates**

Use the [Product Updates](https://www.opswat.com/docs/cm/configurations/product-updates) guideline to learn how to manage product updates.
