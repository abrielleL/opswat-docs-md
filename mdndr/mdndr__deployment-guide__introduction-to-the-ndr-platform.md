<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/introduction-to-the-ndr-platform -->

# Introduction to the NDR Platform

The NDR platform is a modern, Suricata-powered Network Detection and Response solution. It has two tightly integrated components:

- **Sensor** — A high-performance, passive (IDS) appliance/VM. It uses AF_PACKET for native packet capture, deep protocol decode, file extraction, JA3/JA4 fingerprint, and multi-layer analysis. Sensors log **all** events to a local Unix socket. Events include alerts, flows, protocol logs, netflow, fileinfo, and stats. This gives zero-copy, low-latency forward to the Manager.
- **Manager** — The centralized control plane. It provides policy orchestration, configuration management, advanced analytics, visualization, reports, audit, and update distribution. The Manager consumes events from the Sensor's Unix socket through a lightweight adapter. It enriches them and routes them through the real time analytic engine.

**Event flow (highlights Unix socket log):**
