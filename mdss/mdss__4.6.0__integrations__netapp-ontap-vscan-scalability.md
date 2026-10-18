<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/netapp-ontap-vscan-scalability -->

# Vscan | Scalability

Our recommendation is to start with the basic use case, monitor the performance and, depending your business needs, scale the system accordingly.

| Description | Use case | Solution |
| ---- | ---- | ---- |
| Small scale deployments with one SMB share | 0 - 20,000 files per hour* 1 x SMB share | 1 x Vscan Server |
| Small scale deployments with multiple SMB shares | 0 - 20,000 files per hour* 2 or more SMB shares | 1. Connect multiple SMB shares to the same OPSWAT-ONTAP-Connector 2. Connect each SMB share to a separate MDSS instance. You will need a Vscan Server for each MDSS instance |
| Medium to Large scale deployments | 20,000 + files per hour * | 1. Configure multiple Vscan Servers to support your SMB share. 2. Split your data in multiple SMB shares each one being connected to a separate Vscan Server having separate MDSS instances. |

*** The data presented in the table was derived from our [sizing guide](https://www.opswat.com/docs/mdss/getting-started/sizing-guide). These results are intended as guidelines rather than precise performance guarantees due to the multitude of variables that can impact performance, such as file types, network configurations, and hardware specifications. For critical throughput requirements, OPSWAT recommends conducting site-specific benchmarks prior to deploying a production solution.

How to connect multiple SMB shares to the same OPSWAT-ONTAP-Connector

1. Add your SMB share to MetaDefender Storage Security following [this article](https://www.opswat.com/docs/mdss/integrations/netapp-ontap-how-to-enable-vscan)
2. Copy your `StorageClientId`and `SharePath`for your new storage

![](https://uploads.developerhub.io/prod/k8zL/lukf345mungsrgo7mnau2mwjzkmyhfy3ehifye47fpc22ya4rpo3kqetlagoa4lh.png)

3. Navigate to `C:\ProgramData\OPSWAT-ONTAP-Connector\config.ini`
4. Open the file in text editor (requires admin privileges) and modify the number of storage units: `StorageUnits=2`
5. Add details about the second storage unit:

```bash
[Storage Unit 2]
ClientId={StorageClientId}
SharePath={SharePath}
```

6. Restart the service with name`opswat-ontap-connector` in order changes to take effect

### How to configure multiple Vscan Servers

1. You need to have a new Windows Server machine and another AD user (privileged user). For each scan server you will need to have a separate Windows Server machine because **only one ONTAP Connector can be installed on the same Windows Server machine**
2. From ONTAP CLI, add the new IP of the Vscan Server and the new privileged user to scanner pool

```bash
vserver vscan scanner-pool modify -vserver {your-vserver} -scanner-pool {scanner-pool-name} -hostnames {list-of-host-names} -privileged-users {list-of-privileged-users}
```

```bash
vserver vscan scanner-pool modify -vserver opswat-vserver -scanner-pool opswat-scanner-pool -hostnames 10.30.160.180,10.30.160.181 -privileged-users TestAD\privilegeduser1,TESTAD\privilegeduser2
```

For more information about `vserver vscan scanner-pool modify` command, please read [this article](https://docs.netapp.com/us-en/ontap-cli-96//vserver-vscan-scanner-pool-modify.html)

3. Install ONTAP AV Connector and OPSWAT ONTAP Connector on the new Windows Server machine. Follow [this guidance](https://www.opswat.com/docs/mdss/integrations/netapp-ontap-how-to-enable-vscan). To install OPSWAT ONTAP Connector, please copy the zip from first Vscan Server and install from there.
4. Navigate to `C:\ProgramData\OPSWAT-ONTAP-Connector\config.ini` , open it in a text editor with admin privileges
5. Modify the IP of the MetaDefender Storage Security from `127.0.0.1`  with the IP of the first Vscan Server, where your MDSS instance is installed (**Note**: Please be aware that the IP displayed or assigned may differ if a proxy or VPN is being used. To ensure accurate IP information, verify if any proxy or VPN is active)
6. Restart service with name `opswat-ontap-connector` in order changes to take effect
7. Now you should have two scanning servers connected to the same SMB share and same MDSS instance.
8. If you want to add more scan servers, please repeat the process.

> **Info**
>
> When multiple scan servers are utilized, files are distributed to the scan servers using a round-robin method.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
