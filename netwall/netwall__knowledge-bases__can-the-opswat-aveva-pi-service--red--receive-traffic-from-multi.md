<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/can-the-opswat-aveva-pi-service--red--receive-traffic-from-multi -->

# Can the OPSWAT AVEVA PI Service (Red) receive traffic from multiple NetWalls at the same time?

This article applies to all NetWall releases.

Note:

This article applies for traffic that originates from the RED NetWall and goes to a destination source on the RED side. In this case, from RED NetWall to the AVEVA connector on RED.

At the moment, only one RED NetWall can be connected to an OPSWAT AVEVA PI Service for communication at any given time. If multiple NetWalls attempt to send traffic or communicate with a single OPSWAT AVEVA PI Service on the RED side, only one of the NetWalls will be able to establish a communication channel. The other NetWalls will fail establishing communication and will not be able to connect.

**Recommendation**

To have multiple RED NetWalls sending traffic to an OPSWAT AVEVA PI service on the RED, you will have to deploy multiple OPSWAT AVEVA PI services on separate machines (VMs or hardware). In this scenario, one RED NetWall will communication with one OSPWAT AVEVA PI Service.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
