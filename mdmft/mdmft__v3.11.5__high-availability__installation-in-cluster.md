<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/installation-in-cluster -->

# Installation

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This document provides step-by-step instructions for installing the MetaDefender MFT HA Controller™ in a clustered environment, where each controller is deployed on a separate machine for high availability and load balancing.

## [Terminology](/docs/mdmft/v3.11.5/high-availability/installation-in-cluster#terminology)

- **Peer**: An instance of the MetaDefender MFT HA Controller™, deployed as a node in the cluster. Each peer participates in high availability and cluster management.
- **Node**: A machine, on which MetaDefender® MFT runs, and this is behind one or more MetaDefender MFT HA Controller™ . MetaDefender® MFT nodes can operate in an active-passive manner.

---

## [Prerequisites](/docs/mdmft/v3.11.5/high-availability/installation-in-cluster#prerequisites)

Before starting, ensure the following:

- You have access to the installer.
- You have 3 machines for the MetaDefender MFT HA Controller™ cluster deployment.
- Each machine meets the required CPU, memory, disk, and OS prerequisites (see the [Requirements](/docs/mdmft/v3.11.5/high-availability/requirements) for details)
- All machines are connected via a reliable network and can communicate with each other (ensure required ports are open).
- You have administrative privileges on each machine.
- Each peer can connect to the active and passive nodes where MetaDefender® MFT is installed, and required ports are accessible between all peers and nodes.

## [Step 1: Prepare each peer](/docs/mdmft/v3.11.5/high-availability/installation-in-cluster#step-1-prepare-each-peer)

- **Download the Installer**: On every peer intended for the cluster, download the MetaDefender MFT HA Controller™ installer package from My OPSWAT™
- Confirm that each peer satisfies all prerequisites listed above.

## [Step 2. Run the installer](/docs/mdmft/v3.11.5/high-availability/installation-in-cluster#step-2-run-the-installer)

- Execute the installer on every peer according to the instructions in the [Install HA Controller](/docs/mdmft/v3.11.5/high-availability/install-ha-controller) page.
- Complete the installation process as prompted.

## [Step 3. Configure the peers](/docs/mdmft/v3.11.5/high-availability/installation-in-cluster#step-3-configure-the-peers)

- Once installation is complete on all peers, proceed with cluster configuration by following the steps in the [Configuration](/docs/mdmft/v3.11.5/high-availability/configuration) section.

---

Info

Do not attempt to configure cluster settings until installation is completed on all peers. Configuration instructions are provided separately.
