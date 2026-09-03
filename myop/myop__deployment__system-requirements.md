<!-- source: https://www.opswat.com/docs/myop/deployment/system-requirements -->

# System Requirements

To deploy the My OPSWAT On-premises appliance, ensure that your system meets the minimum requirements listed below.

## [Hypervisor Requirements](/docs/myop/deployment/system-requirements#hypervisor-requirements)

My OPSWAT On-premises supports the following virtualization platforms:

- VMware

  - VMware vSphere 7.0, 8.0
  - VMware Workstation Player 17

## [Virtual Appliance Minimum Requirements](/docs/myop/deployment/system-requirements#virtual-appliance-minimum-requirements)

The virtual appliance is created with the following specifications:

- CPU: 8 cores.

  - The hypervisor system must support the AVX instruction set for the virtual CPU.
- Memory: 32 GB.
- Storage:

  - SSD storage is recommended.
  - Thick-provisioned disk size: 1 TB.
  - Thin-provisioned disk size: 10 GB initially, 1 TB maximum.

## [Networking and port requirements](/docs/myop/deployment/system-requirements#networking-and-port-requirements)

| Port | Protocol | Direction | Destination/Source | Use |
| --- | --- | --- | --- | --- |
| 443 | TCP | Inbound | Product instances | communications from Products to My OPSWAT |
| 443 | TCP | Outbound | OPSWAT hosting servers.  [More details](/docs/myop/knowledge-base/what-external-links-does-my-opswat-on-premises-server-connect-to) | for product/modules updates, if enabled |
| 123 | UDP | Outbound | NTP servers | time synchronization |
| <proxy port> | TCP | Outbound | [Configured proxy servers](/docs/myop/configuration/proxy) | send outbound traffics through proxy servers, if configured |
| <SMTP port> | TCP | Outbound | [A configured SMTP server](/docs/myop/configuration/email) | send emails, if configured |
| <Active Directory port> | TCP | Outbound | [Configured Active Directory Servers](/docs/myop/user-management/add-a-new-user-directory) | user authentications, if an account adds an Active Directory user directory |
| <IdP port> | TCP | Outbound | [Configured IdP Servers](/docs/myop/user-management/add-a-new-user-directory) | user authentications, if an account adds a SSO user directory |

Note that if you route traffic through proxy servers, there's no need to set up outbound rules for other outbound connections, except the proxy connections.

## [Browser Versions Supported](/docs/myop/deployment/system-requirements#browser-versions-supported)

Supported browsers for launching the My OPSWAT On-premises console are Chrome, Firefox, and Microsoft Edge on desktop (mobile view has not been supported yet, but in our roadmap). We recommend that you should use the most current version of the browser.

## [Screen Resolution](/docs/myop/deployment/system-requirements#screen-resolution)

We recommend that you use a screen resolution of 1300x768 or larger to properly display My OPSWAT On-premises web console interface.
