<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/installation-options -->

# Installation Options

### [Bare metal](/docs/mdndr/deployment-guide/installation-options#bare-metal)

Deploy directly on dedicated physical servers for maximum performance and lowest latency.

- **Sensor**: Multi-core Intel Xeon 6 Performance series, 128 GB–4 TB RAM, BOSS-N2 boot RAID 1 (OS separation), high-speed NICs, large ring buffers, and RSS.
- **Manager**: Similar CPU/RAM but optimized for storage (RAID 10 NVMe).
- Installation process: Official ISO → automated Ansible playbooks (`ndr-sensor-install`, `ndr-manager-install`). They configure AF_PACKET threads, CPU affinity, hugepages, and systemd services. Post-install tune scripts validate 0% packet loss.

### [Virtualized deployment](/docs/mdndr/deployment-guide/installation-options#virtualized-deployment)

Supported hypervisors: VMware ESXi 8.x (SR-IOV strongly recommended), KVM/libvirt, Microsoft Hyper-V, Nutanix AHV.

- Sensor VM: Dedicated passthrough or SR-IOV NICs, pinned CPUs, NUMA alignment, 1 GB hugepages, and AF_PACKET in `cluster_flow` mode.
- Manager VM: Standard vCPU/memory.
- Performance is identical to bare metal when tuning is correct.

### [Turnkey appliances](/docs/mdndr/deployment-guide/installation-options#turnkey-appliances)

Pre-built 1U/2U Dell PowerEdge servers include factory-optimized BIOS, firmware, drivers, and BOSS-N2 boot storage.

- Available performance tiers: 100Mb, 1Gb, 10Gb, 20Gb, 40Gb, 100Gb (detailed in Section 5).
- Factory image includes Suricata 8.0, Manager or Sensor software, and all performance tuning.
- This is the simplest deployment path for customers who require guaranteed 0% packet loss.
