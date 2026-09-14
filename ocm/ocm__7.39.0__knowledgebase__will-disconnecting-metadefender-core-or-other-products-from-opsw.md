<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/will-disconnecting-metadefender-core-or-other-products-from-opsw -->

# Will disconnecting MetaDefender Core or other products from OPSWAT Central Management v7 delete my configurations?

This article applies to OPSWAT Central Management v7 releases.

Disconnecting MetaDefender Core (MD Core) or other OPSWAT products from OPSWAT Central Management v7 **does not delete the existing configurations stored locally on the product.**

Below is a detailed explanation of what happens when a product is removed from OPSWAT Central Management v7:

### [**1. Are local configurations deleted?**](/docs/ocm/7.39.0/knowledgebase/will-disconnecting-metadefender-core-or-other-products-from-opsw#1-are-local-configurations-deleted)

**No. Local configurations remain unchanged.**

All settings that were previously configured directly on the device stay intact after disconnection. OPSWAT Central Management v7 does not delete, reset, or overwrite any local configuration data.

This includes cases where Central Management was used to configure a Core set. The Core set keeps the configuration it had at the moment the Core was unenrolled. Its settings remain independent from the Core once it is deleted or disconnected.

### [**2. What happens to configuration synchronization?**](/docs/ocm/7.39.0/knowledgebase/will-disconnecting-metadefender-core-or-other-products-from-opsw#2-what-happens-to-configuration-synchronization)

**Synchronization stops.** Once the product is removed from OPSWAT Central Management v7:

- The product will no longer receive policy updates or configuration changes from OPSWAT Central Management v7.
- OPSWAT Central Management v7 can no longer remotely modify or enforce configurations on that product.

### [**3. Management impact**](/docs/ocm/7.39.0/knowledgebase/will-disconnecting-metadefender-core-or-other-products-from-opsw#3-management-impact)

After disconnecting from OPSWAT Central Management v7:

- Centralized control is lost.
- Automated policy distribution stops.
- The product continues operating independently with its existing local settings.
- Consistent policy enforcement across multiple devices is no longer guaranteed.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
