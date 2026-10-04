<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/how-to-setup-firewall-rules-for-pi-database-replication---pi-to- -->

# How to setup Firewall Rules for PI Database Replication & PI-to-PI Transfers?

This article captures the minimum firewall rules required when PI traffic traverses an OPSWAT NetWall for either Pi Replication & Pi-to-Pi Transfer

If you change the configurable Config port on either side, update your rules accordingly.

**Additional PI Server Rule**

Both Red and Blue Flankers connect to their respective on-prem PI Data Archive servers on TCP 5450 (OSIsoft default). Make sure this path is already allowed; see OSIsoft port matrix for other optional endpoints.

**Rule-Creation Checklist**

1. **Outbound from NetWall RED**

   1. Allow TCP **60001** and **60002** to the Red Flanker IP.
2. **Outbound from NetWall BLUE**

   1. Allow TCP **60001** (replication) or **60000** (PI-to-PI) to the Blue Flanker IP.
3. **Inbound to NetWall BLUE**

   1. Allow TCP **61097** (replication) or **61096** (PI-to-PI) **from** the Blue Flanker IP **to** NetWall BLUE.
   2. This is the only rule in which the Flanker initiates the session.
4. **Confirm PI Server Access**

   1. Permit each Flanker to reach its local PI Data Archive on **TCP 5450** (and any other PI services you use).

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
