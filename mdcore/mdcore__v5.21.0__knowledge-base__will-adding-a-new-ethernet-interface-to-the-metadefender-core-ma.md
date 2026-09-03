<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/will-adding-a-new-ethernet-interface-to-the-metadefender-core-ma -->

# Will adding a new Ethernet Interface to the MetaDefender Core machine impact its functionality?

This applies to all versions before **MetaDefender Core** **5.17.0**

**v5.17.0** introduces support for teamed NIC (Network Interface Card) configurations, preserving Deployment ID and maintaining stable license activation when network adapters are changed or switched within the team.

Adding an additional **Ethernet interface** to a system running MetaDefender Core does not negatively affect the product’s operational capabilities. When properly configured, MetaDefender Core can operate seamlessly across multiple network interfaces.

MetaDefender Core supports serving both its **REST API** and **Web UI** on multiple IP addresses. This behavior is governed by the `restaddress` registry configuration parameter. Administrators may choose to:

- Allow MetaDefender Core to listen on all available IP addresses, or
- Restrict MetaDefender Core to a specific IP address if required.

For detailed configuration instructions, refer to the MetaDefender Core Configuration documentation.

[**→ MetaDefender Configuration**](https://www.opswat.com/docs/mdcore/configuration/metadefender-configuration#windows)

While adding a secondary Ethernet interface is safe, administrators must use caution when modifying the **primary NIC**—specifically its **MAC address**. The MAC address of the initially configured primary network interface is tied to the system’s **Deployment ID**.

Changing the primary NIC’s MAC address will cause MetaDefender Core to update its Deployment ID. This triggers a license validation event.

[**→ Does the Deployment ID change at any time?**](https://www.opswat.com/docs/mdcore/knowledge-base/does-the-deployment-id-change-at-any-time-)

If a Deployment ID change occurs, MetaDefender Core automatically recognizes the modification and prompts for license reactivation. Activation based on the updated Deployment ID ensures continuous service availability.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
