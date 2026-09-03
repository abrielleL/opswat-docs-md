<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/which-snmp-versions-are-supported-by-netwall-products--how-to-co -->

# Which SNMP versions are supported by NetWall products? How to configure OID?

This article applies to all MetaDefender NetWall products including Optical Diode, USG/BSG, Diode X, etc.

Supported SNMP Versions:

Currently, NetWall supports the following SNMP versions:

- SNMP v1
- SNMP v2c

**Monitoring OIDs and MIBs**

Depending on the type of metric being monitored, different MIBs should be used.

Disk Monitoring: For disk-related metrics such as disk usage and storage statistics, use the UCD MIB.

Bandwidth Monitoring: For monitoring network interfaces and bandwidth usage, use MIB-2.

MIB-2 includes standard network interface counters such as:

- Interface traffic statistics
- Incoming and outgoing bandwidth
- Interface status

**OPSWAT MIB**

These OIDs are not part of standard MIB libraries and may vary depending on the product version.

If you require the OIDs defined in the OPSWAT MIB for monitoring or integration purposes, please contact OPSWAT Support.

In Summary

SNMP v1 and v2c are supported by NetWall. For monitoring:

- Use **U**CD MIB for disk and system resource metrics.
- Use MIB-2 for network bandwidth and interface statistics.
- Use the OPSWAT MIB for additional NetWall-specific metrics (available through OPSWAT Support).

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
