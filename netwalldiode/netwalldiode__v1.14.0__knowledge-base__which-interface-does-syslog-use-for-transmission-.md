<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/which-interface-does-syslog-use-for-transmission- -->

# Which Interface Does Syslog Use for Transmission?

This article applies to all MetaDefender NetWall devices.

Syslog streams in MetaDefender network devices (such as USG NetWall) are designed to use the data interface for transmission.

However, the actual interface used depends on the routing configuration of the device.

If the Syslog server is reachable through both the management (MGMT) and data interfaces, the device will select the interface based on the system routing table. This means that the interface associated with the route to the Syslog server’s network will be used, regardless of whether it’s the MGMT or data interface.

#### [**Example Scenario**](/docs/netwalldiode/v1.14.0/knowledge-base/which-interface-does-syslog-use-for-transmission-#example-scenario)

Syslog Server: 40.40.40.40

In this example, the Syslog server is located on a network (40.40.40.x) that is not directly reachable from either the MGMT or data subnets.

Since the device has a default gateway configured on the MGMT interface (20.20.20.1), it will use that interface to reach the Syslog server. As a result, Syslog traffic will go through the MGMT interface even though the Syslog process is logically associated with the data interface.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
