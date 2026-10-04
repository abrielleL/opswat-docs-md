<!-- source: https://www.opswat.com/docs/mdndr/release-notes -->

# Release Notes

###

 v5.3.0

## MetaDefender NDR v5.3.0 — Release Notes

**Release Date:** September 29, 2026

### Overview

MetaDefender NDR v5.3.0 introduces six significant capability additions focused on licensing flexibility, regulatory compliance, multi-tenant deployment, security operations integration, and long-term data governance.

### Key Customer Benefits

#### Licensing & Entitlements Service

- Added a dedicated licensing and entitlements service that centralizes license validation, feature entitlement checks, and usage tracking.
- Provided a more reliable and auditable foundation for feature gating and subscription management across deployments.

#### Corsec FIPS Certification

- Completed FIPS 140-2/140-3 validation work with Corsec.
- Enabled deployment in federal, defense, and other regulated environments that require FIPS-validated cryptographic modules.

#### Multitenancy Phase 1

- Added the first phase of multitenancy support, allowing a single MetaDefender NDR deployment to logically separate data, configuration, and access across multiple tenants.
- Laid the groundwork for MSSPs and large enterprises that need to manage multiple business units or customers from a shared platform instance.

#### D3 Security SOAR Integration

- Added native integration with D3 Security's SOAR platform.
- Enabled automated alert forwarding, case creation, and orchestrated response workflows without custom middleware.

#### UI/UX Enhancements

- Delivered broad usability improvements across the hunting, dashboard, and administration interfaces.
- Reduced the number of clicks needed for routine analyst and administrator tasks.

#### Data Retention Management

- Added granular data retention policy configuration by data type.
- Gave organizations finer control over storage costs and compliance with internal or regulatory data-retention requirements.

### Upgrade Notes

- Customers in regulated environments should validate their deployment against the new FIPS-validated cryptographic modules after upgrade.
- Organizations planning multi-tenant deployments should review the Multitenancy Phase 1 documentation before enabling tenant separation.
- Customers using SOAR platforms should review the new D3 Security integration configuration guide to enable automated case creation.
- Administrators should review default data retention settings after upgrade, as new granular controls may change existing storage behavior.
- A browser refresh may be required after upgrade to load the latest UI assets.
