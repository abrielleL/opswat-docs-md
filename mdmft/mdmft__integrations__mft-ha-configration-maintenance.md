<!-- source: https://www.opswat.com/docs/mdmft/integrations/mft-ha-configration-maintenance -->

# Configuration and Maintenance

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### [Configuration](/docs/mdmft/integrations/mft-ha-configration-maintenance#configuration)

1. Install and configure MetaDefender Managed File Transfer with Microsoft SQL Server Database.
2. Install Neverfail Continuity Engine.
3. Configure Neverfail Continuity Engine.

4. Add MetaDefender Managed File Transfer to Neverfail Continuity Engine as a Service and add folders via the provided script.
5. Stop Neverfail Continuity Engine using the "Stop Protected Applications" option.

6. Clone the full virtual machine.
7. After cloning, reconfigure the Neverfail Continuity Engine on the cloned system as Secondary/Passive.

8. Start Neverfail Continuity Engine on the First/Active Server.

### [Use Cases](/docs/mdmft/integrations/mft-ha-configration-maintenance#use-cases)

Info

The following are examples of how Neverfail Continuity Engine can react to various events, depending on its configuration:

1. MetaDefender Managed File Transfer service stops -> Neverfail Continuity Engine automatically starts the service.
2. Service Network goes down on the active server due to a network switch error -> Neverfail Continuity Engine switches from the active server to the passive server.
3. Host Windows system shuts down or crashes -> Neverfail Continuity Engine switches the active server to the passive server.
4. Manual switch from the active system to the passive node -> done before performing any operating system updates/maintenance.

### [Maintenance](/docs/mdmft/integrations/mft-ha-configration-maintenance#maintenance)

#### [How to Update MetaDefender Managed File Transfer in a High Available Configuration](/docs/mdmft/integrations/mft-ha-configration-maintenance#how-to-update-metadefender-managed-file-transfer-in-a-high-available-configuration)

1. Create a full system backup from both the active and passive systems.
2. Stop Neverfail Continuity Engine on both the active and passive servers, but keep MetaDefender Managed File Transfer running.
3. Update MetaDefender Managed File Transfer on the first server (previously active server) as outlined in the <how to update MFT> guide.
4. Stop MetaDefender Managed File Transfer services on the first server.
5. Start MetaDefender Managed File Transfer services on the second server (previously the passive server).
6. Update MetaDefender Managed File Transfer on second server following the [Upgrading MetaDefender Managed File Transfer](/docs/mdmft/installation/updating-and-upgrading) guide.
7. Stop MetaDefender Managed File Transfer services on second server.
8. Start Neverfail Continuity Engine on the first server (previously the active server).
9. Start Neverfail Continuity Engine on the second server (previously the passive server).
