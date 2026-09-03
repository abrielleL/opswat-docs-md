<!-- source: https://www.opswat.com/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat- -->

# What are differences between OCMv7 vs My OPSWAT?

### [Why are My OPSWAT On-premises better than OCMv7?](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#why-are-my-opswat-on-premises-better-than-ocmv7)

- Improve the quality and clarity of reports and dashboards to emphasize what a user should pay attention: Security risk, Inventory, product-specific dashboards
- Optimized/ standardized communications between managed products and My OPSWAT for easy deploying the entire OPSWAT solution.
- Seamless and secure user provisions with Local users, Active Directory integration, and Single Sign-On integration
- Individual license & Volume license activation
- Flexible/ faster deployment with virtual appliance option for on-premises deployments
- Provide a SaaS-based product management solution that enables customers to seamlessly integrate their instances and start immediately.
- Seamless upgrade process: either Auto-upgrade itself via Internet at desired schedule or manually upgrading.
- Integration: RESTful APIs allows seamless data retrieval from My OPSWAT to your data center, enabling data visualization across various systems within your organization.
- Enhance the user interface and user experience so that users can focus on their operation

### [Deployment Options](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#deployment-options)

|  | OCMv7 | My OPSWAT |
| --- | --- | --- |
| On-premises | Windows (msi)  Linux (Ubuntu 18, 20, 22; Red Hat Enterprise Linux 7) | Virtual appliance (ova: VMware Player, WMware) |
| SaaS |  | my.opswat.com |
| IaaS (Bring Your Own Cloud) |  | AWS AMI |

### [Features parity with OCMv7](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#features-parity-with-ocmv7)

#### [Product Management](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#product-management)

| Product | Inventory |  | Dashboard & Reporting |  | Configuration |  | Auto Update |  |  |  | License Management |  | Product Update |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  | OCMv7 | My OPSWAT | OCMv7 | My OPSWAT | OCMv7 | My OPSWAT | OCMv7 | My OPSWAT |  |  | OCMv7 | My OPSWAT | OCMv7 | My OPSWAT |
| MetaDefender Kiosk Linux (L-Series) | Y | Y | Y | Y | Y | Y | Modules Firmware | Modules Firmware |  |  | Volume license | Volume license | Y | Y |
| MetaDefender Kiosk Windows (K-Series) | Y | Y | Y | Y | Y | Y | N | Firmware |  |  | Individual | Individual/ Volume license | N/A | N/A |
| MetaDefender Core | Y | Y | Y | Y | Y | Y | Modules | Modules |  |  | Individual | Individual/ Volume license | N/A | N/A |
| MetaDefender File Transfer (Vault) | Y | Y | N | Y | Y | Y |  |  |  |  | Individual |  | N/A | N/A |
| MetaDefender ICAP Server | Y | Y |  |  | Y | Y |  |  |  |  | Individual |  | N/A | N/A |
| MetaDefender Email Gateway Security | Y | Y |  |  | Y | Y |  |  |  |  | Individual |  | N/A | N/A |
| MetaDefender for Secure Storage | Y | Y |  |  | N | Y |  |  |  |  |  |  | N/A | N/A |
| MetaDefende Software Supply Chain |  | Y |  |  |  |  |  |  |  |  |  |  |  |  |
| MetaDefender Drive | Y | Y | Only scan session report |  | Y |  |  |  |  |  |  |  |  |  |
| MetaDefender Media Firewall |  | Y |  | Y |  |  |  | N/A |  |  |  | N/A |  | Y |
| MetaDefender Sandbox |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Bilateral Security Gateway Red |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Bilateral Security Gateway Blue |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Optical Diode Red |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Optical Diode Blue |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender NetWall Threat Protection Red |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender NetWall Threat Protection Blue |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Unidirectional Security Gateway Red |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Unidirectional Security Gateway Blue |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender OT Security |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |
| MetaDefender Industrial Firewall & IPS |  | Y |  |  |  |  | N/A | N/A |  |  |  |  | N/A | N/A |

#### [User Management](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#user-management)

|  | OCMv7 | My OPSWAT |
| --- | --- | --- |
| **User Provision** |  |  |
| Local Users | Y | Y |
| Active Directory | Y | Y |
| Single Sign-On (SAML 2.0) | Y  only IdP-Initiated  no single logout | Y  both IdP-Initiated and SP-Initiated  single logout  allow map IdP groups to My OPSWAT with different roles |
| **User Roles** |  |  |
| built-in roles | - Administrator - View-Only - Operator | - Administrator - View-Only |
| Custom roles | N | Y |
| **Miscellaneous** |  |  |
| Export users/groups | N | Y |
| User session timeout | Y | Y |
| PIN requirement for changes | Y  always enable | Y  configurable |
| User Profile | Y | Y |

#### [Reports & Notifications](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#reports--notifications)

|  | OCMv7 | My OPSWAT |
| --- | --- | --- |
| Inventory Dashboard | Y | Y  (with a better dashboard) |
| Security Risks Dashboard |  | Y |
| MetaDefender Kiosk Summary | Y | Y |

#### [Public APIs](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#public-apis)

My OPSWAT provides [RESTful APIs](https://docs.opswat.com/product-management/developer-guide) that allow seamless data retrieval from your My OPSWAT to your data center, enabling data visualization across various systems within your organization. More details can be found at <documentation link>

OCMv7 doesn’t support this.

#### [Other Features](/docs/myop/knowledge-base/what-are-differences-between-ocmv7-vs-my-opswat-#other-features)

|  | OCMv7 | My OPSWAT |
| --- | --- | --- |
| Proxy | Y | Y |
| Email | Y  Basic authentication | Y  Basic authentication  Secret key authentication |
| Secure connection | Y | Y |
| Certificates management | Y | Y |
| Trust certificates management |  | Y |
| Auto-upgrade |  | Y |
| Audit log | Y | Y |
| Import/Export | Y | Y |
| Data Retention |  | Y |
| **Tools** |  |  |
| - Challenge Response Code Generator for MD Endpoint (OMVA) |  | Y |
| **Customization** |  |  |
| - message on Login page | Y |  |
