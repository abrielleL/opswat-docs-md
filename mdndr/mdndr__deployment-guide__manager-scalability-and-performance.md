<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/manager-scalability-and-performance -->

# Manager Scalability and Performance

The Manager scales from small deployments (1–25 Sensors) to large enterprise deployments (100–200 Sensors).

- **Event ingestion**: All Sensors log to local Unix socket → Sensor adapter → message queue.
- **Stream analytics**: The analytics engine consumes the message queue and performs real-time behavioral analysis.
- **Storage layer**: Hot data uses full text indexed storage (recent events, fast search). Warm/cold data uses columnar database storage (long-term retention, cost-optimized analytics).
- **Manager size**:

| Manager Type | Sensors supported | CPU Cores | RAM | Storage (RAID 10 NVMe) |
| --- | --- | --- | --- | --- |
| Manager STD | Up to 25 | 32–64 | 512 GB | 19.2 TB |
| Manager XL | 100–500 | 96–192 | 1–4 TB | 76.8+ TB |

- Add Manager nodes for horizontal scale.
