<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/clearing-orphaned-deployment-ids-after-network-configuration-cha -->

# Clearing Orphaned Deployment IDs After Network Configuration Changes

**Check Your Version:**

This article applies to MetaDefender Optical Diode (all license types)

**Symptom**

After changing the management IP address on a Optical Diode unit:

1. If the new management IP is assigned to a **different** NIC/interface than the original, a new deployment ID is generated, and a new YML license file must be generated.

   - Example: original Management IP was on Interface1, new Management IP is on Interface2.
2. If the management IP or default gateway changes but remains on the **same** NIC/interface, the existing deployment ID and license remain valid, no new YML file needs to be generated.

In the **first case**, the original deployment ID remains tied to its license slot and cannot be reused without being explicitly cleared.

Reference: <https://www.opswat.com/docs/netwalldiode/knowledge-base/how-to-configure-separate-data-and-management-interfaces-on-meta#change-the-default-route>

**Impact**

Each orphaned deployment ID continues to consume a unit from the license pool. If not cleared, customers with limited license quantities will be unable to activate replacement or additional units.

**Self-Service Deactivation**

Deployment IDs can be deactivated via the OPSWAT deactivation API:

curl -X GET "https://activation.dl.opswat.com/deactivation?key=<activation-key>&deployment=<deployment-id>"

A 200 Ok response with result: ok confirms successful deactivation.

**Contact OPSWAT Support**

If self-service deactivation is not possible, please contact OPSWAT Support and provide:

- License key
- Deployment ID(s) to be cleared (one per diode unit)
- Confirmation that the associated YML file is no longer in use

**Notes**

Clearing deployment IDs does not delete the license; it only frees the consumed activation slots.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

MetaDefender
