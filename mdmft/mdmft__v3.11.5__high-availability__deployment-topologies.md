<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/deployment-topologies -->

# Deployment Topologies

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

MetaDefender Managed File Transfer™ supports multiple deployment topologies, each designed for different levels of redundancy and infrastructure complexity. Choose the topology that best matches your organization's availability requirements, network architecture, and disaster recovery goals.

### [Simple Setup](/docs/mdmft/v3.11.5/high-availability/deployment-topologies#simple-setup)

The simplest HA deployment. A single MetaDefender MFT HA Controller™ manages two MetaDefender® MFT instances in an **active-passive** configuration.

Info

**When to use:** You need high availability for MetaDefender® MFT but can accept the MetaDefender MFT HA Controller™ itself as a single point of failure.

Warning

**Note:** If the MetaDefender MFT HA Controller™ becomes unavailable, automatic failover will not occur. Consider the [Redundant Controllers](/docs/mdmft/v3.11.5/high-availability/deployment-topologies#redundant-controllers) topology if controller-level redundancy is required.

You can find more information about the setup [here](/docs/mdmft/v3.11.5/high-availability/high-availability).

### [Redundant Controllers](/docs/mdmft/v3.11.5/high-availability/deployment-topologies#redundant-controllers)

This topology eliminates the MetaDefender MFT HA Controller™ as a single point of failure by deploying **three MetaDefender MFT HA Controller™** instances in a Raft consensus cluster. A **3rd-party load balancer** sits in front of the controllers and distributes incoming traffic across them.

Info

**When to use:** Environments where both the MetaDefender® MFT service and the HA control plane must be resilient to individual component failures.

You can find more information about the setup [here](/docs/mdmft/v3.11.5/high-availability/redundant-ha-controllers).

### [Two-Site Setup](/docs/mdmft/v3.11.5/high-availability/deployment-topologies#two-site-setup)

This topology extends high availability across **two separated sites** for disaster recovery.

A **3rd-party load balancer** directs user traffic to the appropriate site based on a **public-facing health endpoint** exposed by each MetaDefender® MFT instance.

In this context, a split-brain scenario can occur if a network failure isolates the Primary and Secondary sites. The MetaDefender MFT HA Controller™ may lose connectivity to the Primary MetaDefender® MFT and activate the Secondary MetaDefender® MFT, while the Primary may still be running and processing traffic. This can lead to both sites operating independently and accepting requests, resulting in inconsistent system state or data corruption.

Warning

**Note:** The Two-Site topology does **not** provide split-brain protection.

It is the customer's responsibility to assess this risk and implement additional safeguards to mitigate potential data corruption in the event of a network partition.

You can find more information about the setup [here](/docs/mdmft/v3.11.5/high-availability/two-site-setup).

## [Choosing a Topology](/docs/mdmft/v3.11.5/high-availability/deployment-topologies#choosing-a-topology)

| Feature | Simple Setup | Redundant Controllers | Two-Site Setup |
| --- | --- | --- | --- |
| Number of MetaDefender MFT HA Controller™ peers | 1 | 3 | 1 |
| Single Point of Failure | ⚠️Yes | ✅No | ✅No |
| Split-Brain Risk | ✅No | ✅No | ⚠️Yes |
| Failure Handling | Medium | Strong | Limited |
| Operational Complexity | Low | High | Medium |
