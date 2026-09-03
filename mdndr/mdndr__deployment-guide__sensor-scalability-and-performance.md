<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/sensor-scalability-and-performance -->

# Sensor Scalability and Performance

Sensors support 0% packet loss at sustained load + bursts. They use AF_PACKET v3, CPU affinity, large ring buffers, and multi-queue NICs.

**Recommended hardware tiers for appliances (0% packet loss, 100k+ signatures, full protocol log + Unix socket output):**

| Throughput | CPU Cores | RAM | Storage (RAID 10 NVMe) | NIC Example |
| --- | --- | --- | --- | --- |
| 100 Mb | 8–16 | 128 GB | 3.84 TB | 2×1 GbE LOM |
| 1 Gb | 24–32 | 256 GB | 7.68 TB | Broadcom 57414 25 GbE |
| 10 Gb | 48–64 | 512 GB | 19.2 TB | NVIDIA ConnectX-6 100 GbE |
| 20 Gb | 86–96 | 1 TB | 38.4 TB | Broadcom 57508 100 GbE |
| 40 Gb | 96–128 | 2 TB | 51.2 TB | Broadcom 57508 Dual 100 GbE |
| 100 Gb | 128–192 | 4 TB | 76.8 TB | NVIDIA ConnectX-6 100 GbE |

All tiers use BOSS-N2 boot storage (RAID 1) for OS separation. All tiers use AF_PACKET tuning (`block-size`, `ring-size`, `cluster-type: cluster_flow`).
