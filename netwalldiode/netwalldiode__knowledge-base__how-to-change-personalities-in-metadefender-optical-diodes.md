<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes -->

# How to change personalities in Metadefender Optical Diodes

This article applies all deployments of Metadefender Optical Diode

### [Summary](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#summary)

The **OD-101** and **OD-102** personalities on MetaDefender Optical Diode appliances are interchangeable. You can switch between the two personalities on the same hardware as long as **both Optical Diode appliances are running the exact same software version**.

### [What Are OD-101 and OD-102 Personalities?](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#what-are-od-101-and-od-102-personalities)

| Personality | Description | Key Characteristics |
| --- | --- | --- |
| **OD-101** | Common Criteria EAL4+ certified personality | EAL4+ certified mode High Availability **disabled** |
| **OD-102** | High Availability (HA) personality | HA support **enabled** Not EAL4+ certified |

### [Condition for Successful Interchange](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#condition-for-successful-interchange)

The personalities can be freely interchanged and will work together correctly only when both diodes are on the same MetaDefender Optical Diode version (for example, both running version 1.13.1).

This ensures full compatibility of the personality file, license, and configuration between the two units.

### [When Would You Interchange Personalities?](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#when-would-you-interchange-personalities)

- Convert a unit from EAL4+ certified mode (OD-101) to HA-capable mode (OD-102) when redundancy becomes a requirement.
- Switch from HA mode back to certified mode (OD-101) when Common Criteria EAL4+ compliance or audit needs change.
- Repurpose spare appliances between different projects without hardware replacement.

### [How to Interchange the Personality](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#how-to-interchange-the-personality)

1. Confirm that both MetaDefender Optical Diode appliances are updated to the **identical software version**.
2. Log in to [My OPSWAT Portal - One-stop Hub for Customers and Partners](http://myopswat.com/) and download the desired personality file (OD-101 or OD-102) that matches the current software version.
3. On the Optical Diode web interface, go to the **License / Personality** section.
4. Upload the new personality file.
5. Apply the change and reboot the appliance when prompted.
6. Verify the active personality on the **System Status** or **About** page.

### [Important Notes & Limitations](/docs/netwalldiode/knowledge-base/how-to-change-personalities-in-metadefender-optical-diodes#important-notes--limitations)

- After switching to **OD-102**, you can configure a High Availability pair.
- After switching to **OD-101**, the appliance operates in EAL4+ certified mode and HA functionality is disabled.
- Both units in an HA pair must use the **same personality** and the **same software version**.
- Changing personalities does **not** require an RMA or hardware replacement.
- Always back up the current configuration before performing a personality change.

This flexibility allows you to adapt the same physical MetaDefender Optical Diode appliances to evolving operational or compliance requirements without additional hardware purchases.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
