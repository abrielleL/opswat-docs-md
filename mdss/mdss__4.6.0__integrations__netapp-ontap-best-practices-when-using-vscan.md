<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/netapp-ontap-best-practices-when-using-vscan -->

# Vscan | Best practices

### Privileged User

- Restrict privileged users to virus-scanning operations. Normal users should be discouraged from using privileged user credentials. This restriction can be achieved by turning off login rights for privileged users on Active Directory.
- Privileged users are not required to be part of any user group that has a large number of rights in the domain, such as the administrators group or the backup operators group
- Privileged users must be validated only by the storage system so that they are allowed to create Vscanner connections and access files for virus scanning.

### Vscanner

- Use the computers running Vscanners only for virus-scanning purposes. To discourage general use, disable the Windows terminal services and other remote access provisions on these machines and grant the right to install new software on these machines only to administrators.
- Dedicate Vscanners to virus scanning and do not use them for other operations, such as backups. You might decide to run the Vscanner as a virtual machine (VM). If this is the case, ensure that the resources allocated to the VM are not shared and are sufficient to perform virus scanning.
- Provide adequate CPU, memory, and disk capacity to the Vscanner to avoid resource bottlenecks. Most Vscanners are designed to use multiple CPU core servers and to distribute the load across the CPUs.
- For remote sites and branch offices, NetApp recommends using a local Vscanner rather than a remote Vscanner because the former is a perfect candidate for high latency. If cost is a factor, use a laptop or PC (as a Vscanner) for moderate virus protection.

### Vscanner Networking

- Connect the NetApp storage system and the Vscanner by using at least a 1GbE network.
- For an environment with multiple Vscanners, connect all servers that have similar high-performing network connections. Connecting the Vscanners improves performance by allowing load sharing.
- NetApp recommends using a dedicated network with a private VLAN for the connection from the SVM to the Vscanner so that the scan traffic is not affected by other client network traffic. Create a separate NIC that is dedicated to the antivirus VLAN on the Vscanner and to the data LIF on the SVM. This step simplifies administration and troubleshooting if network issues arise.
- The AV traffic should be segregated using a private network. The AV server should be configured to communicate with domain controller (DC) and clustered Data ONTAP in one of the following ways:
  - The DC should communicate to the AV servers through the private network that is used to segregate the traffic.
  - The DC and AV server should communicate through a different network (not the private network mentioned previously), which is not the same as the CIFS client network. Private Network is optional.
- For Kerberos authentication to work for the AV communication, create a DNS entry for the private LIFs and a service principal name on the DC corresponding to the DNS entry created for the private LIF. Use this name when adding a LIF to the Antivirus Connector. The DNS should be able to return a unique name for each private LIF.

### Node Failover

If the LIF for Vscan traffic is configured on a different port than the LIF for client traffic, the Vscan LIF might fail over to another node in case of a port failure. The change will make the Vscanner not reachable from the new node and the scan notifications for file operations on the node will fail.

> **Info**
>
> For more details about this type of storage please read [the official ONTAP Documentation](https://docs.netapp.com/us-en/ontap/)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
