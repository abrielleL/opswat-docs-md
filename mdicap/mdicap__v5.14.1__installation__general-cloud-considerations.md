<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/general-cloud-considerations -->

# General Cloud Considerations

When deploying to any Cloud Service Provider (CSP), consider these general recommendations:

## [Roles/Permissions](/docs/mdicap/v5.14.1/installation/general-cloud-considerations#rolespermissions)

The Principle of Least Privilege (PoLP) is a foundational cybersecurity concept. It entails granting users, applications, and systems only the minimum access necessary to perform their tasks.

This approach minimizes the potential attack surface, mitigates risks associated with insider threats, and helps prevent privilege creep. When deploying OPSWAT products, **OPSWAT recommends** adhering to this principle.

Regarding access to applications or API endpoints, generate **strong passwords** for UI access.

Store the **API keys** required to access the API endpoints of the various products in a secure secrets manager.

## [VPC/Networking](/docs/mdicap/v5.14.1/installation/general-cloud-considerations#vpcnetworking)

OPSWAT recommends following networking best practices when deploying products:

- Multi-AZ Deployment

  - Distribute resources across multiple Availability Zones (AZs) to enhance fault tolerance and availability. OPSWAT products are designed to run in different AZs simultaneously.
- Security Groups

  - These act as virtual firewalls to control inbound and outbound traffic. Follow the system requirements for each OPSWAT product to open the necessary ports.
- IP Address Planning

  - Allocate CIDR blocks thoughtfully to avoid overlaps, especially when integrating with on-premises networks.
- Subnet Segmentation

  - Use distinct subnets to separate public-facing resources (MDSS UI) from private resources (MDSS PostgreSql database server).
