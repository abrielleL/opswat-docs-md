<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/operating/guest-manager-guide -->

# Guest Manager Guide

Overview

The purpose of this document is to provide the end user with an overview and basic familiarity with the NAC Guest Manager. The NAC Guest Manager provides a way to provision guest user accounts. Guest user credentials can be created from this page and are stored within NAC, preventing the need to use additional LDAP resources. This document will only cover help desk provisioning model of guest users. The self-provisioning model of guest access is covered in detail in a separate document.

Access to the features of the NAC Guest Manager will vary depending on the read or write permissions granted to the end user from the User Management section of the NAC Configuration Manager.

## [Introduction](/docs/manac/nac-v8.1.1/operating/guest-manager-guide#introduction)

To access the Guest Manager, navigate to [https://portal.myweblogon.com:8443/manage/#/guests/users](https://auth.impulse.com:8443/manage/#/guests/users). “[portal.myweblogon.com](http://auth.impulse.com/)” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

Users with “read” access to the Guest Manager will be able to view everything in the Guest Manager. The list of accounts can be sorted by clicking on the column titles.

## [Accounts Tab](/docs/manac/nac-v8.1.1/operating/guest-manager-guide#accounts-tab)

Clicking on "Add" in the top right corner of the page will open a form to create a new guest user.

When creating guest users, the only required fields are the “Username” and “Password” fields. Everything else is optional based on the business needs.

The password can be entered manually or by clicking on the key icon inside the “Password” field. This icon will automatically create a randomized password. Clicking the eye icon will toggle whether the password is seen in plain text or hidden as bullets.

Clicking Advanced shows more options. These fields are automatically filled with the default settings for the Guest User Profile. These are configured in the Guest Self-Provisioning section of the Configuration Manager

Once a user account is created, it will appear in the user list in the Accounts tab. When guest accounts expire, the system will remove the account and copy the details to the History tab.

Clicking on "Actions" in the top right corner of the page will show a drop down of actions which can be taken on a guest user entry. These are grayed out (as shown below) unless a user is selected from the list. When any option is clicked, a popup appears to verify this is the wanted operation.

| Operation | Description |
| --- | --- |
| Purge | Clears the guest user record. |
| Expire | Treats the guest user as if it were new on the network. |
| Activate | Activates an Inactive guest user enrollment. |
| Resend Notification | Resends both text and email notifications. |
| Print Login Info | Opens a new tab in browser containing the username and QR codes of the guest user. |
| Bulk Upload | Used to upload a large number of guest user entries which would be inconvenient to input one at a time. From the popup, a template can be downloaded, filled with the required information for every new entry and uploaded. |

## [History Tab](/docs/manac/nac-v8.1.1/operating/guest-manager-guide#history-tab)

The history page shows the transaction history of all guest accounts. The list can be sorted by clicking on the column titles.
