<!-- source: https://www.opswat.com/docs/mdndr/archived-release-notes -->

# Archived Release Notes

###

 v5.1.0
## Release Notes for v5.1.0

### Overview

This release improves the NDR platform experience across detection coverage, hunting workflows, policy and signature management, update reliability, and operational hardening. The focus is on making investigations faster, presenting richer alert context, improving policy workflows, and reducing operational friction during platform updates.

### Key Customer Benefits

#### Improved Hunting and Investigation

- Added configurable table views for hunting and dashboard workflows, including column selection, column ordering, resizing, auto-sizing, and persisted user preferences.
- Added advanced search capabilities for hunting workflows, including support for nested objects and collections.
- Improved alert and event detail views with clearer field labels, better behavioral and ML alert visibility, and sensor name context where available.
- Improved dashboard recent-alert pagination and table behavior for larger result sets.

#### Stronger Signature and Policy Workflows

- Restored reliable loading for the signature policy page so the signature catalog is visible and searchable from the UI.
- Improved default policy seeding and pagination behavior for large signature sets.
- Added policy templates, single-draft/discard workflow improvements, and policy role-based access controls.
- Improved support for raw rule compilation and policy assignment operations.
- Added ATT&CK coverage metadata to help customers better understand detection coverage.

#### Expanded Detection and Alert Context

- Added and refined behavioral, ML, DNS, DGA, port-scan, connection-spray, and tunneling detection outputs.
- Improved alert naming and signature attribution for ML and behavioral detections.
- Added richer detection metadata such as destination ports, feature attribution, and protocol context where available.
- Reduced false positives from internal platform, sensor, TLS, DNS, broadcast, and HOME_NET noise.
- Improved alert documents so enrichments and ontology-backed fields are more consistent across detection types.

#### Better Analytics and Search

- Improved search behavior for sessions, flows, files, alerts, and text fields.
- Added separate indexing improvements for core hunting data types.
- Improved dashboard and hunting aggregates, including hourly top-alert-by-signature support.
- Improved time-range handling for analytics queries.
- Added more consistent, ontology-aligned detection fields across analytics APIs.

#### Enrichment Improvements

- Improved C2, GeoIP, InSights, and MetaDefender enrichment behavior.
- Added service-level proxy support for enrichment providers in environments that require outbound proxy control.
- Improved MetaDefender concurrency handling with hot-reload support for scan limits.
- Expanded GeoIP enrichment eligibility and moved GeoIP processing to a more data-driven model.

### Platform Update and Operations Improvements

- Added platform auto-update provider support.
- Hardened manual update workflows and host-side update execution.
- Improved package validation, policy-rule staging, and update provider handling.
- Improved platform update coordination from the manager.
- Improved large-rule handling and timeout behavior during sensor policy/rule delivery.
- Improved production security controls around Kafka transport, update execution, and release exposure.

### Security and Reliability Hardening

- Removed sensitive authentication logging.
- Improved audit filtering and correlation reads.
- Improved licensing integration and runtime behavior.
- Applied dependency and runtime hardening across platform services.
- Improved release scanning coverage and remediation of known dependency findings.

### Upgrade Notes

- Customers should expect UI changes in hunting, dashboard, policy, and signature workflows.
- Browser refresh may be required after upgrade to load the latest UI assets.
- Customers using outbound proxies should review enrichment and update-provider proxy settings after upgrade.
- Customers with large signature or policy deployments should benefit from improved pagination, rule handling, and timeout behavior.
- Customers using sensor interface changes should validate that the sensor is capturing on the expected interface after configuration changes.
