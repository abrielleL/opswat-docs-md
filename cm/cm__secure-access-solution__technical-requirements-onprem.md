<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/technical-requirements-onprem -->

# Technical Requirements

## [Virtual Enforcer System Requirements](https://www.opswat.com/docs/manac/installation/technical-requirements#virtual-enforcer-system-requirements)

### [VMWare vSphere](https://www.opswat.com/docs/manac/installation/technical-requirements#vmware-vsphere)

#### Small Standalone Appliance

| **Appliance Specifications** | **NAC-Edge VMWare Enforcer** |
| ---- | ---- |
| **VMWare Version** | ESXi 5.1 or newer |
| **Virtual Hardware Version** | Minimum version 8 |
| **CPU** | 16 vCPUs (2-3Ghz) |
| **Memory** | 32 GB Minimum |
| **Hard Drive Storage** | 100 GB Minimum |
| **Network Interface** | Gigabit NIC |

### Network Requirements

#### FQDN Resolution

The following FQDN must be resolved to the IP address of the NAC image before deployment:

| FQDN | Resolves To |
| ---- | ---- |
| portal.myweblogon.com | IP address of the NAC image |

**Note:** Ensure your DNS server (or local `hosts` file) is configured to resolve `portal.myweblogon.com` to the NAC image's assigned IP address prior to installation. Failure to configure this may result in portal access issues.
