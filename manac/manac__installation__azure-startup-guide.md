<!-- source: https://www.opswat.com/docs/manac/installation/azure-startup-guide -->

# Azure Startup Guide

Includes Installation Instructions for loading NAC into your Azure environment.

## [Overview](/docs/manac/installation/azure-startup-guide#overview)

This document is intended to be used as a guide to install a Virtual Machine (VM) version of the NAC Policy Enforcer appliance within an Azure virtual environment. You should be familiar with the Azure Management Portal prior to attempting this task. If technical support is required during the installation, please use the contact information below for assistance.

NAC is deployed to an Azure environment via a template that includes all components needed for complete functionality in an Azure. At deployment, you will receive an email from OPSWAT with a link to Azure to deploy the VM in your environment, and an Access Token needed to complete delivery. Once you have received this email, you may begin with installation below.

OPSWAT Customer Support: <https://opswat.com/support/>

## [Installation](/docs/manac/installation/azure-startup-guide#installation)

Info

The OPSWAT Enforcer VM image requires a **Standard_A5** Azure Instance. This configuration allows for up to 25,000 concurrent connections.

To deploy the new VM in your Azure environment, click the Deploy to Azure button in the email you received from OPSWAT. This will take you to a form in the Azure platform to create the environment.

Fill in all required information including your Access Token that was included in your email. Once the information is filled in, click purchase.

- Subscription

  - You may use your own subscription. Charges will occur per the Azure pricing model.
- Resource Group

  - Resource groups provide a way to monitor, control access, provision and manage billing for collections of assets that are required to run an application, or used by a client or company department.
  - Microsoft Documentation: <https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview>
- Location

  - Choose a regional Azure Datacenter to meet your requirements
- Storage Account Name

  - An Azure storage account provides a unique namespace to store and access your Azure Storage data objects. All objects in a storage account are billed together as a group. By default, the data in your account is available only to you, the account owner.
  - Microsoft Documentation: <https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account>
- DNS for Public IP

  - Used for communication with the Internet, including Azure public-facing services.
  - Microsoft Documentation: <https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-ip-addresses-overview-arm>

After the deployment is finished you should see your environment.

## [Email Configuration](/docs/manac/installation/azure-startup-guide#email-configuration)

Azure Reference: <https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/>

The supported way to send e-mails to external domains from Azure compute resources is via a SMTP relay (otherwise known as a SMTP smart host). The Azure compute resource sends the e-mail to the SMTP relay and then the SMTP relay provider delivers the e-mail to the external domain. Microsoft Exchange Online Protection is one provider of a SMTP relay, but there are several 3rd party providers as well. We list some pointers to SMTP relay services below, but it is not a complete list. Please note that you need to setup an account with the SMTP relay provider first and then configure your Azure server or application to send outbound e-mail via the SMTP relay.
