<!-- source: https://www.opswat.com/docs/mdmft/integrations/mft-ha -->

# High Availability

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Info

MetaDefender Managed File Transfer™ uses a third-party solution, *Neverfail Continuity Engine*, to enable Active-Passive High Availability between two MetaDefender Managed File Transfer™ instances.

Neverfail Continuity Engine is a dependable software solution. It ensures uninterrupted operation of critical applications through advanced monitoring and failover capabilities, thereby enhancing business resilience against downtime and data loss.

### [Limitations](/docs/mdmft/integrations/mft-ha#limitations)

- The Neverfail High Availability setup supports only a 2-node system in an Active/Passive configuration.
- Virtual Machines cannot be in an Active Directory and must operate in Standalone mode.
- This solution does not cover high availability for *LocalDB* or *Microsoft SQL Server (RemoteDB)*.

### [Prerequisites](/docs/mdmft/integrations/mft-ha#prerequisites)

- **Remote MSSQL server:** A separate Microsoft SQL server must be accessible by the virtual machines.
- **Dedicated heartbeat network:** Neverfail requires a separate network for the heartbeat and data transfer channel.
- **Static IP:** All network interfaces must have static IP addresses.
- **Permission to clone:** Access and permission to clone the virtual machine.
- **Open network ports:** Open Windows Firewall ports for Neverfail Continuity Engine: 57348 , 52267.
