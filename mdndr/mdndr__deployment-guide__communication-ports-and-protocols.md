<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/communication-ports-and-protocols -->

# Communication Ports and Protocols

- **Client → Manager UI**

HTTPS (TCP 443) – Secure web access to the MetaDefender NDR Manager UI and API through the front-envoy HTTPS service. TLS 1.3 only.

- **Sensor ↔ Manager**

The sensor starts a secure outbound TLS 1.3 communication channel to the Manager (default TCP 443, configurable). The channel supports policy push, configuration sync, command execution, health checks, certificate lifecycle management, and real-time event stream from the Unix socket.

- The system mutually authenticates and encrypts all traffic end-to-end with TLS 1.3 and mTLS where applicable.

| Port | Protocol | Exposed to | Purpose |
| --- | --- | --- | --- |
| 443 | TCP | Users / UI / API clients | Main NDR UI and API access through front-envoy HTTPS |
| 8443 | TCP | Sensors | Sensor enrollment TLS endpoint on manager |
| 9443 | TCP | Sensors | Sensor mTLS API endpoint for work polling, configuration updates, bundle delivery, and certificate lifecycle management |
| 9094 | TCP | Sensors | External Kafka SSL/mTLS ingest for Suricata and sensor event stream |
| 4317 | TCP | Sensors | OTLP gRPC telemetry from the sensor-side OpenTelemetry agent to the platform OpenTelemetry collector443 |
