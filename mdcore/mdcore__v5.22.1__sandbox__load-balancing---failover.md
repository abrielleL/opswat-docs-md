<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/sandbox/load-balancing---failover -->

# Load Balancing / Failover

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

Only available in Remote Adaptive Sandbox version 2.4.0 and higher.

## [Enable Load Balancing](/docs/mdcore/v5.22.1/sandbox/load-balancing---failover#enable-load-balancing)

Load balancing / Failover can be enabled in **Inventory -> Modules -> Adaptive Sandbox -> Enable load balancing/failover**

## [Round Robin](/docs/mdcore/v5.22.1/sandbox/load-balancing---failover#round-robin)

The Round Robin strategy can be used to add 1-2 extra Standalone Sandbox instances, for better scanning performance in high demand scenarios

Round Robin will cycle through the servers trying to distribute the load between them (Server 1 -> Server 2 -> Server 3 -> Repeat)

**Failover**

The Failover strategy can be used to register a second Standalone Instance for backup in case of High Availability setups.

The failover server will only be used when the first server is unresponsive.
