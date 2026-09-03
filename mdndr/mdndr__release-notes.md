<!-- source: https://www.opswat.com/docs/mdndr/release-notes -->

# Release Notes

###

 Release Notes - v5.2.0

## MetaDefender NDR v5.2.0 — Release Notes

**Release Date:** July 31, 2026

### Overview

MetaDefender NDR v5.2.0 introduces six significant capability additions focused on enterprise integration, operational visibility, and deployment flexibility — particularly for air-gapped environments and organizations with mature identity and security operations infrastructure.

### What’s New

#### Manual Threat Intelligence & Software Updates via UI

Operators can now upload threat intelligence feeds and software update packages directly through the administration interface. This eliminates dependency on automated pipelines and external connectivity, enabling organizations in air-gapped, classified, or network-restricted environments to maintain current detection coverage and software versions without external access.

#### Multi-Sensor Behavioral Analytics

Behavioral analytics now support multi-sensor configuration, enabling a single MetaDefender NDR deployment to correlate detections and orchestrate response across distributed sensor infrastructure. Security teams gain centralized visibility and coordinated detection across multiple network segments from a single control plane.

#### OpenTelemetry Observability Integration

MetaDefender NDR now natively exports metrics, traces, and logs in OpenTelemetry format, compatible with any OTel-compliant observability backend (Prometheus, Grafana, Datadog, Splunk Observability, and others). This provides standardized operational telemetry without custom integrations or proprietary agents.

#### Expanded Policy Administration

Policy administration has been significantly expanded to support fleet-wide policy management. Security teams can now define, version, and distribute detection and response policies across all deployed sensors from a single administrative interface, simplifying governance in large or multi-site deployments.

#### Enterprise Identity Integration (SAML 2.0 / Microsoft Entra ID / Okta)

MetaDefender NDR now supports single sign-on and identity federation via SAML 2.0, Microsoft Entra ID (Azure AD), and Okta. This enables seamless integration with enterprise IAM workflows, centralizes access control, and eliminates the need for local credential management for administrative users.

#### SIEM Integration via Syslog

Out-of-the-box syslog forwarding enables NDR alerts and event
