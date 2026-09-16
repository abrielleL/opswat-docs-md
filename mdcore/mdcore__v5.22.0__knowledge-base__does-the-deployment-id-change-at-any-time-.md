<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/does-the-deployment-id-change-at-any-time- -->

# Does the Deployment ID change at any time?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

### [**New in v5.17.0:**](/docs/mdcore/v5.22.0/knowledge-base/does-the-deployment-id-change-at-any-time-#new-in-v5170)

Starting from **MetaDefender Core v5.17.0**, the product now supports **teamed NIC (Network Interface Card) configurations** without causing Deployment ID changes. This enhancement ensures that license activation remains stable even when network adapters within the team are changed or switched. With this improvement:

- Deployment ID will remain consistent across NIC team reconfigurations.
- Service interruptions due to MAC address changes in teamed NIC setups are eliminated.

For more information, please refer to [Release notes - MetaDefender Core](https://www.opswat.com/docs/mdcore/release-notes#new-features-improvements-and-enhancements)

### [**For users running versions prior to v5.17.0, please refer to the following instructions:**](/docs/mdcore/v5.22.0/knowledge-base/does-the-deployment-id-change-at-any-time-#for-users-running-versions-prior-to-v5170-please-refer-to-the-following-instructions)

License holders should be aware that changes or updates to the hardware or network components of the system on which MetaDefender Core is installed could result in changes to the Deployment ID.

Pro Tip:

To check whether your Deployment ID has changed, go to your **MetaDefender Core Management Console>Settings>License** tab, where your package ID, activation key, deployment ID and license expiry date are all listed.

Error

In some cases, if MetaDefender Core is deployed on a server using **teamed NIC**, the deployment ID may change due to changing physical (MAC) address of the server’s network adapter.

**Cause**: NIC teaming, also known as Load Balancing/Failover (LBFO) or NIC bonding, allows you to combine multiple physical network adapters into a single logical network card

When using teamed NIC, because the primary team member (primary NIC) might change in a non-deterministic manner (e.g. at each boot, NIC disable/enable action, or other reconfiguration activities), the primary team member might change, and the MAC address of the team might vary.

- Since MetaDefender Core’s deployment ID is based partly on the MAC address of the network adapter, varying MAC address also leads to deployment ID changes and deactivation of license - causing service interruptions.

Example of a teamed NIC:

BashCopyEthernet adapter Team:
Connection-specific DNS Suffix . :
Description . . . . . . . . . . . : Microsoft Network Adapter Multiplexor Driver
Physical Address. . . . . . . . . : XX-XX-XX-XX-XX-XX

- `Microsoft Network Adapter Multiplexor Driver` is a kernel mode driver to team up with multiple network adapters to provide one unified device to utilize the entire network bandwidth and load balancing among underlying adapters.

**Solution**: To avoid MetaDefender Core service interruption due to changing deployment ID, please perform the necessary steps to ensure the teamed NIC’s physical address remain the same after reboot.

- One way to achieve this is by configuring **a static MAC address** for the teamed NIC.

Please Note:

Operating system upgrades, license upgrades, license renewals and other factors unrelated to system hardware and network components should not affect your Deployment ID.

However, in the unlikely event that you notice an unexplained change to your Deployment ID, please contact support as instructed below.

Support:

If you require further assistance with your **Licensing or Deployment ID**, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
