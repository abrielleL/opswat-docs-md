<!-- source: https://www.opswat.com/docs/mdmft/high-availability/two-site-setup -->

# Two-Site Setup

Summarize Page    Connect to Cursor Connect to VS Code

The Two-Site topology is designed for geographically distributed deployments where traffic is routed externally and failover occurs across sites.

## [Overview](/docs/mdmft/high-availability/two-site-setup#overview)

In this topology, MetaDefender® MFT instances are deployed across two sites:

- **Primary Site (Active)** – handles all client traffic under normal operation
- **Secondary Site (Passive)** – remains on standby until failover is triggered

Client traffic is routed through a **third-party load balancer**, which directs requests based on a public health endpoint.

## [MetaDefender MFT HA Controller™ Behavior](/docs/mdmft/high-availability/two-site-setup#ha_controller_product_name_short-behavior)

A key difference in this topology compared to other deployments is the role of the HA Controller.

The MetaDefender MFT HA Controller™ **does not act as a reverse proxy**. Instead, it functions as a **state manager and failover switch**.

- It continuously monitors the health of the MetaDefender® MFT nodes
- It does not handle or route client traffic
- It determines which node should be active

If the MetaDefender MFT HA Controller™ detects that the active (Primary) MetaDefender® MFT node is unavailable:

- It promotes the Secondary MetaDefender® MFT node to active
- The system transitions to serving traffic from the Secondary site

This design separates:

- **Traffic routing (external load balancer)**
- **Failover decision logic (MetaDefender MFT HA Controller™)**

## [Traffic Flow](/docs/mdmft/high-availability/two-site-setup#traffic-flow)

Clients connect to the system via a **third-party Load Balancer**

1. The Load Balancer routes traffic to the currently active MetaDefender MFT HA Controller™ instance
2. Routing decisions are based on a **public** [**Health Endpoint**](/docs/mdmft/high-availability/two-site-load-balancer-setup#health-endpoint)
3. The MetaDefender MFT HA Controller™ independently monitors node health and controls activation state

## [Failover Behavior](/docs/mdmft/high-availability/two-site-setup#failover-behavior)

Failover is triggered when:

- The MetaDefender MFT HA Controller™ loses connectivity to the active MetaDefender® MFT node
- Or the node fails health checks

In such cases:

- The Secondary node is activated
- The Load Balancer begins routing traffic to the Secondary site

## [When to Use This Topology](/docs/mdmft/high-availability/two-site-setup#when-to-use-this-topology)

This topology is best suited for:

- Geo-distributed environments
- Disaster recovery scenarios
- Deployments requiring external traffic control

It is **not recommended** for environments requiring strict consistency guarantees without additional safeguards.

### [Limitations and Risks](/docs/mdmft/high-availability/two-site-setup#limitations-and-risks)

#### [Split-Brain Scenario](/docs/mdmft/high-availability/two-site-setup#split-brain-scenario)

A split-brain condition occurs when a distributed system is divided into multiple isolated parts due to a network failure, and each part assumes it is the active system. As a result, multiple nodes may operate independently and accept requests without coordination, leading to inconsistent data and system state.

In the Two-Site topology, this situation can occur if the MetaDefender MFT HA Controller™ loses network connectivity to the Primary Site. In such a case:

- The MetaDefender MFT HA Controller™ assumes the Primary MetaDefender® MFT is unavailable
- It activates the Secondary MetaDefender® MFT

However, the Primary MetaDefender® MFT may still be running and processing requests.

This results in both MetaDefender® MFT nodes operating simultaneously and independently. In addition to handling client requests, each MetaDefender® MFT instance may also execute background processing tasks such as file processing, malware scanning, email notifications, syslog generation, and other internal workflows.

Because these operations are not coordinated between sites, concurrent execution can lead to:

- Race conditions
- Data inconsistency
- Data corruption
- Duplicate or conflicting background processing actions

Resolving such situations may require manual intervention and can result in data loss.

Warning

The Two-Site topology does not provide split-brain protection. It is the customer's responsibility to assess this risk and implement additional safeguards to prevent or mitigate split-brain scenarios.
