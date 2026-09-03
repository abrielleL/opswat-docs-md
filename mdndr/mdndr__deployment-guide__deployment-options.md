<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/deployment-options -->

# Deployment Options

A sensor is passive. It receives a copy of the network traffic through a mirror. Choose the mirror method that matches your environment.

### [On-premise](/docs/mdndr/deployment-guide/deployment-options#on-premise)

- **Network TAP (best practice)**: Passive, fail-safe full-duplex mirror. Use optical/copper TAPs (Ixia, Keysight, or Gigamon) on critical links. The sensor receives traffic on one or more capture interfaces.
- **Switch SPAN port (last resort)**: Configure port mirror (Cisco `monitor session`, Arista `mirror session`, Juniper `port-mirror`). Use ERSPAN for remote sources.
- Sensors operate in passive IDS mode by default.

### [Virtualized (VMware VCF)](/docs/mdndr/deployment-guide/deployment-options#virtualized-vmware-vcf)

- Deploy a virtual sensor (vSensor) in the same cluster to see east-west traffic.
- Use an NSX port-mirror profile or a vSphere Distributed Switch (VDS) port-mirror session.
- A physical SPAN alone misses host-local traffic between two virtual machines.
- For the full procedure, see Strategic sensor placement.

### [Cloud deployments](/docs/mdndr/deployment-guide/deployment-options#cloud-deployments)

- **AWS**: VPC Traffic Mirroring (filter by ENI, subnet, or VPC) sends traffic to the sensor's ENI.
- **Azure**: Virtual Network TAP or Network Watcher packet capture routes traffic to Sensor VM.
- **GCP**: Packet Mirror policies target instance groups or specific VMs.
- Sensors run as VMs in the same VPC/VNet. You can deploy the Manager in the same cloud or on-premise (hybrid).
- The platform supports multi-region and multi-account setups through transit gateways or peer connections.
