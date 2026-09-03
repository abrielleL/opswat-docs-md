<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-do-i-remediate-a-failed-result-when-attempting-to-install-a- -->

# How do I remediate a failed result when attempting to install a product or push SET product configuration to remote devices via an SSL Connection?

This article applies to all supported versions of MetaDefender products to be deployed on Windows, macOS or Linux systems, including:

- MetaDefender Core
- MetaDefender Kiosk
- MetaDefender Managed File Transfer
- MetaDefender ICAP Server
- MetaDefender Email Gateway Security
- MetaDefender Drive
- MetaDefender for Secure Storage
- MetaAccess NAC

Additionally, this article applies to OPSWAT Central Management V7.5+ releases deployed on Windows or Linux systems.

## [Remote install: connection failures](/docs/ocm/knowledgebase/how-do-i-remediate-a-failed-result-when-attempting-to-install-a-#remote-install-connection-failures)

When attempting to remote-install an OPSWAT product to your managed devices via OPSWAT Central Management and an SSL connection, the system may return an error stating that a **Connection cannot be established**.

This is more than likely the result of an **OpenSSH server** not being enabled on the target device/s. Users should review [This Article](https://docs.opswat.com/ocm/operating/remote-install-opswat-products) for detailed instructions on how to configure the target machine/s accordingly.

## [SET configuration: push failures](/docs/ocm/knowledgebase/how-do-i-remediate-a-failed-result-when-attempting-to-install-a-#set-configuration-push-failures)

Likewise, administrators may encounter a failed result when attempting to push SET configuration to product instances via OPSWAT Central Management Console over an SSL Connection.

In this case (and provided that an OpenSSH server is enabled on the target machine/s to allow it/them to communicate with OPSWAT Central Management), administrators can likely remediate the problem by ensuring that the **Certificate Name** is identical in both the OPSWAT Central Management Console and the product instance (such as in the MetaDefender Core) to which they are attempting to push the SET configuration.

Support:

For further queries, concerns or issues regarding **Unable To Remediate A Failure To Remote Install Products Or Push SET Product Configuration To Remote Devices Via An SSL Connection**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
