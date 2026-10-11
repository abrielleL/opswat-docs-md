<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-exclude-opswat-folder-from-anti-virus-windows-defender- -->

# How to Exclude the OPSWAT Folder from Windows Defender?

> **Please Note**
>
> This article applies to MetaDefender Storage Security deployed on Windows systems.

When using MetaDefender Storage Security deployed on Windows systems, it is important exclude the OPSWAT directory from **all**  existing Anti-Malware software programs on the machine. Failure to  exclude the OPSWAT directory can lead to performance degradation under high load, as the  Anti-Malware software will also scan files that are streamed from the storage integration to MetaDefender Core, and may also slow down communication between certain components of the product.

Some common Anti-Malware software to perform these exclusions on are, including but not  limited to: Windows Defender, McAfee, Norton, Bitdefender, Malwarebytes, SentinelOne.

### How to exclude on Windows Defender

Ensure you have **administrator privileges** before adding exclusions.

1. Navigate to “Windows Security” > “Virus & threat protection”

![](https://uploads.developerhub.io/prod/k8zL/q2gcq2lseoyo6472gzklax56zamgbnh4gv0x4tcox3qae6mwn53s452pvnkmgmqy.png)

2. Under “Virus & threat protection settings” click “Manage settings”

![](https://uploads.developerhub.io/prod/k8zL/emabm940au2ulv1xceyn7317ii2u0b1hykdcuqp01eo9ga8aj6fnaokqudd00k3j.png)

3. Scroll down to “Exclusions” and click “Add or remove exclusions”

![](https://uploads.developerhub.io/prod/k8zL/2o02g346ei1mkrar699m7xcmcddvr7s3xsg6d443k3rpwogkhzodpxpc1n70nq5m.png)

3. Add the “OPSWAT” folder. By default it is located in the installation directory: `C:\Program Files\OPSWAT` .
4. Add the “Temp” folder located at `C:\Users\<user>\AppData\Local\Temp`.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
