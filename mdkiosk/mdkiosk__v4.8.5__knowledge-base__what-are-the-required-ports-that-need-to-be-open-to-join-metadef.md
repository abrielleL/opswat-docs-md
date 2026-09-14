<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef -->

# What are the required ports that need to be open to join MetaDefender Hardened image to the domain?

Version Check:

- This article applies to all MetaDefender Kiosk Versions deployed using the OPSWAT Hardened image.
## [**Overview**](/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef#overview)

This article outlines the network ports and protocols required for successfully joining our OPSWAT Windows Hardened Kiosk to an Active Directory (AD) domain. Proper connectivity to domain controllers (DCs) over these ports is essential for authentication, directory services, and group policy processing.

---

## [**Required Ports and Protocols:**](/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef#required-ports-and-protocols)

| Service | Protocol | Port | **Purpose** |
| --- | --- | --- | --- |
| DNS | TCP/UDP | 53 | Name resolution for domain controllers |
| Kerberos | TCP/UDP | 88 | Authentication with AD |
| RPC Endpoint Mapper | TCP | 135 | Required to locate RPC services |
| NetBIOS Name Service | UDP | 137 | Legacy environments |
| NetBIOS Datagram | UDP | 138 | Legacy environments |
| NetBIOS Session | TCP | 139 | Legacy support (may still be required) |
| LDAP | TCP/UDP | 389 | Directory queries and authentication |
| SMB/CIFS | TCP | 445 | File sharing and SYSVOL/NETLOGON access |
| Kerberos kpasswd | TCP/UDP | 464 |  |
| RPC Dynamic Ports | TCP | 49152–65535 | Used for AD services, group policy, and replication |

**Optional (depending on config):**

| Service | Protocol | Port | **Purpose** |
| --- | --- | --- | --- |
| LDAPS | TCP | 636 | Secure LDAP (if enforced) |
| Global Catalog | TCP | 3268 | AD forest-wide searches |
| Global Catalog SSL | TCP | 3269 | Secure GC access |
| NTP (time sync) | UDP | 123 | Time synchronization (Kerberos dependency) |

---

## [**Important Notes**](/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef#important-notes)

- The Hardened Image **blocks all inbound connections by default**, but the domain join traffic is primarily outbound from the kiosk to the DC, so it should work as long as there's no network firewall blocking those ports between the kiosk and the DC.
- To access firewall settings on the Hardened Image, you'll need to go through the **MMC snap-in** (`mmc` → Add Snap-in → Windows Defender Firewall), since `gpedit.msc` shortcuts are restricted.
- Domain-join state is **not preserved across Hardened Image upgrades** — you'll need to re-join after each image upgrade.

---

## [**Validation Steps**](/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef#validation-steps)

After opening the required ports, validate connectivity:

| **Test** | **Command** |
| --- | --- |
| **Test DNS Resolution** | **nslookup** <YOUR_DOMAIN.LOCAL> |
| **Test Domain Controller Discovery** | **nltest /dsgetdc**:<YOUR_DOMAIN.LOCAL> |
| **Test Port Connectivity (PowerShell)** | **Test-NetConnection** -<COMPUTER_NAME> <DC_NAME> -Port 389 |

---

## [**Common Issues**](/docs/mdkiosk/v4.8.5/knowledge-base/what-are-the-required-ports-that-need-to-be-open-to-join-metadef#common-issues)

| Issue | Cause | Resolution |
| --- | --- | --- |
| "Domain not found" | DNS misconfiguration | Point client DNS to domain controller |
| "Access denied" | Kerberos failure | Verify time sync (NTP) |
| Join hangs or times out | Firewall blocking RPC | Open port 135 and dynamic RPC range |
| Group policy not applied | SMB blocked | Ensure port 445 is open |

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
