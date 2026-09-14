<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/upgrade-a-mft-cluster -->

# Upgrade MFT Cluster

Summarize Page    Connect to Cursor Connect to VS Code
## [Upgrade Steps](/docs/mdmft/v3.11.4/high-availability/upgrade-a-mft-cluster#upgrade-steps)

1. On the MetaDefender MFT HA Controller™ machine stop the Windows Service. This prevents the controller from directing traffic or interfering during node upgrades.

2. Upgrade the **active** node: On the currently active node, run the new version of the installer. More information about upgrading can be found [here](/docs/mdmft/v3.11.4/installation/updating-and-upgrading).
3. Wait for the installation to complete successfully.
4. Stop the application services on the active node: After the installer finishes, stop all product services (Windows services). You can find more details about how to stop the product services [here](/docs/mdmft/v3.11.4/high-availability/install-mft-nodes#stop-the-first-node).
5. Upgrade the **passive** node: Go to the passive node machine and run the same installer.
6. After the installation completed stop all product services.
7. Upgrade the MetaDefender MFT HA Controller™ with it's own installer.
8. Start the `Node Manager` service on each MetaDefender® MFT node (active and passive).

Info

The MetaDefender MFT HA Controller™ periodically sends health checks to each node, including verifying that all components are running compatible versions. If the versions match, it proceeds to select which node becomes active and which remains passive.

9. Verify that the HA cluster has been upgraded by visiting the MetaDefender MFT HA Controller™’s web interface (at its configured address).
10. As the final recommended step, trigger a manual failover after the upgrade to verify that all nodes are operating correctly. You can find more information about manual failover [here](/docs/mdmft/v3.11.4/high-availability/failover-scenarios#manually-triggered-failover).
