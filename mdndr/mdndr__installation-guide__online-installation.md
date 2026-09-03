<!-- source: https://www.opswat.com/docs/mdndr/installation-guide/online-installation -->

# Online Installation

> **Prepare your host system /VM**

> Before installation, make sure that your target system meets the technical requirements. A person with basic Linux skills must do the installation.

> **Warning**

> This page only applies to product installation with a **stable internet connection!**

## [Installation](/docs/mdndr/installation-guide/online-installation#installation)

### [**Step #1 - Download and unpack the product installer:**](/docs/mdndr/installation-guide/online-installation#step-1---download-and-unpack-the-product-installer)

Download the release archive from <https://my.opswat.com/portal/products>. Save it to a convenient location, for example your home folder.

The release archive is password protected. Use 7-Zip to unpack it:

> Use the **password** that you received from OPSWAT support!

> Adjust the x.y.z **version numbers** to match the downloaded filename.

7za x -aoa -p"PASSWORD" MetaDefender_NDR_vx.y.z-Standalone.zip
### [Step #2 - Move to the installation folder:](/docs/mdndr/installation-guide/online-installation#step-2---move-to-the-installation-folder)

cd ndr-installer
### [Step #3 - Run the install shell script](/docs/mdndr/installation-guide/online-installation#step-3---run-the-install-shell-script)

This operation can take up to 20-30 minutes. The time depends on available network bandwidth.

sudo ./install.sh

The first installation step is EULA acceptance. Type **ACCEPT** to start the installation.

### [**Step #4 - Access the NDR web server**](/docs/mdndr/installation-guide/online-installation#step-4---access-the-ndr-web-server)

Go to ([https://localhost:443](https://localhost/)). Set up the initial Admin user.

> username: admin

> password: admin123

### [Step #5 - Add your activation key](/docs/mdndr/installation-guide/online-installation#step-5---add-your-activation-key)

> Use the Activation Key that you received from your OPSWAT Sales Representative. Follow the instructions on the License Activation page.

Simple steps for Online activation:

Go to *Admin panel > Settings > Integrations > License Management*. Click *Activate All*. Then **enter your license key**!

---

## [Manager/sensor installation and adoption (v5)](/docs/mdndr/installation-guide/online-installation#managersensor-installation-and-adoption-v5)

MetaDefender NDR v5 deploys from a bootable ISO that runs a **First-Boot Guided Installer**. The installer supports three deployment roles. You can deploy a Manager and one or more Sensors independently.

### [Prerequisites](/docs/mdndr/installation-guide/online-installation#prerequisites)

| Resource | All-in-One | Manager Only | Sensor Only |

| --- | --- | --- | --- |

| CPU | 8+ cores (4 min) | 4+ cores | 2+ cores |

| RAM | 32 GB recommended (8 GB min) | 16 GB recommended (8 GB min) | 4 GB min |

| Disk | 150 GB | 150 GB | 50 GB |

| NICs | 2+ (1 mgmt, 1+ capture) | 1 (mgmt) | 1 mgmt + 1+ capture |

> For Sensor enrollment to a remote Manager: HTTPS port **8443** must be open from sensor to Manager IP.

### [Obtain and boot the ISO](/docs/mdndr/installation-guide/online-installation#obtain-and-boot-the-iso)

1. Download the NDR v5 ISO from the [OPSWAT Customer Portal](https://my.opswat.com/portal/products) or your designated artifact repository.
2. Flash to USB. On Linux/macOS, use `dd`. On Windows, use [Rufus](https://rufus.ie) in **DD Image** mode.
3. As an alternative, attach the ISO as a virtual CD-ROM in your hypervisor.
4. Boot the target server/VM from the ISO.
5. When the **NDR boot menu** appears, select **Install NDR Platform**.
6. Press Enter.
7. Wait until the automated Oracle Linux 9 OS installation completes (~10–20 minutes).
8. Let the system reboot automatically.

### [First-boot guided installer](/docs/mdndr/installation-guide/online-installation#first-boot-guided-installer)

After reboot, the **NDR First-Boot Guided Installer** starts automatically on the console. If you connect over SSH before setup completes, run:

sudo ndr-firstboot

**Step 1:** Accept the EULA. Enter `ACCEPT`.

**Step 2:** Select a deployment role:

- **1) All-in-One** — Full NDR management platform with a local Suricata sensor on this host
- **2) Manager** — Management platform only; you enroll sensors separately
- **3) Sensor** — Network capture sensor that connects to an existing Manager

#### [All-in-One role prompts](/docs/mdndr/installation-guide/online-installation#all-in-one-role-prompts)

| Prompt | Example | Notes |

| --- | --- | --- |

| Management interface | `eth0` | Interface for operator UI/API access |

| Capture interface(s) | `eth1,eth2` | Comma-separated interfaces |

| HOME_NET | `192.168.0.0/16` | Internal network CIDR(s) |

| Sensor name | `aio-sensor-01` | Friendly display name in the UI |

#### [Manager only role](/docs/mdndr/installation-guide/online-installation#manager-only-role)

The installer prompts only for the **management network interface**. Use the NDR Web UI after installation for all further configuration.

#### [Sensor only role — enrollment prompts](/docs/mdndr/installation-guide/online-installation#sensor-only-role--enrollment-prompts)

| Prompt | Example | Notes |

| --- | --- | --- |

| Manager URL | `https://192.168.1.10:8443` | Manager enrollment API endpoint |

| Enrollment token | `eyJ...` | Generated from Manager UI |

| Capture interface(s) | `eth1` | Interface(s) for traffic capture |

| HOME_NET | `192.168.0.0/16` | Internal network CIDR(s) |

| Sensor name | `sensor-datacenter-01` | Friendly display name |

### [Generate a sensor enrollment token](/docs/mdndr/installation-guide/online-installation#generate-a-sensor-enrollment-token)

Before you enroll a new sensor, generate an enrollment token from the Manager:

1. Log in to the Manager Web UI.
2. Go to **Admin panel → Sensors → Add Sensor**.
3. Copy the generated enrollment token (`eyJ...`).
4. When prompted, supply this token to the Sensor First-Boot Installer.

The sensor establishes a mutual TLS-authenticated channel to the Manager after successful enrollment. It appears in the **Sensors** list as **Online**.

### [Post-installation access](/docs/mdndr/installation-guide/online-installation#post-installation-access)

| Service | URL / Endpoint |

| --- | --- |

| NDR Web UI | `https://<ip>:443` |

| SSH | `ssh admin@<ip>` |

| Sensor status | `sudo systemctl status ndr-adapter.service ndr-sensord.service` |

### [Airgapped deployments](/docs/mdndr/installation-guide/online-installation#airgapped-deployments)

The NDR ISO is fully self-contained. All container images are pre-loaded. The installation and normal operation require **no internet access**. For DNS-restricted environments, configure `/etc/hosts` or a local DNS resolver. This lets the system resolve the management hostname before sensor enrollment.

---

## [OVA installation for MetaDefender NDR v5](/docs/mdndr/installation-guide/online-installation#ova-installation-for-metadefender-ndr-v5)

MetaDefender NDR v5 installs from a **bootable ISO image**. No pre-built OVA is available for import. This section tells you how to create and configure a virtual machine. It also tells you how to attach the NDR v5 ISO and run the First-Boot Guided Installer in a hypervisor.

> OPSWAT distributes MetaDefender NDR v5 as a **bootable ISO** (not a pre-packaged OVA/OVF). Create the VM yourself with the specs below. Then install from the ISO exactly as you would on bare metal.

> VM-based deployments support **1 Gbps sensors and below only**. Higher throughput tiers (10 Gb, 20 Gb, 40 Gb, 100 Gb) require dedicated bare-metal appliances with hardware-level tuning (SR-IOV, pinned CPUs, hugepages, RAID NVMe). Do not run a high-throughput sensor in a VM.

---

> Enable CPU virtualization extensions (**Intel VT-x / AMD-V**) in BIOS/UEFI. For nested virtualization (VM-inside-VM), make sure that the hypervisor exposes these extensions to the guest.

### [Supported hypervisors](/docs/mdndr/installation-guide/online-installation#supported-hypervisors)

| Hypervisor | Recommended Adapter | Notes |

| --- | --- | --- |

| VMware ESXi 7.0+ | VMXNET3 | Recommended for production |

| VMware Workstation / Fusion (Intel) | VMXNET3 or E1000e | Lab/demo use |

| KVM / Proxmox VE | VirtIO | Best open-source option |

| VirtualBox | Paravirtualized / Intel PRO/1000 | Lab use only |

---

> VMware Fusion on **Apple Silicon (ARM/M-series)** is not supported. MetaDefender NDR v5 requires x86_64 architecture.

### [VM size requirements](/docs/mdndr/installation-guide/online-installation#vm-size-requirements)

#### [Sensor virtual machine (1 Gbps)](/docs/mdndr/installation-guide/online-installation#sensor-virtual-machine-1-gbps)

| Resource | Minimum | Recommended |

| --- | --- | --- |

| vCPU | 24 cores | 32 cores |

| RAM | 256 GB | 256 GB |

| Storage | 7.68 TB | 7.68 TB NVMe |

| Management NIC | 1 GbE | 1 GbE (static IP) |

| Capture NIC(s) | 1 GbE+ | 1+ dedicated capture interfaces |

> Configure capture NIC(s) in **promiscuous mode** so the VM can see all traffic on the monitored segment. In VMware, set the vSwitch/portgroup to **Promiscuous Mode: Accept**. In Proxmox/KVM, set the bridge up without ARP filter.

#### [Manager VM](/docs/mdndr/installation-guide/online-installation#manager-vm)

| SKU | Sensors Managed | vCPU Cores | RAM | Storage |

| --- | --- | --- | --- | --- |

| Manager STD | Up to 25 sensors | 32–64 | 512 GB | 19.2 TB NVMe (RAID 10) |

| Manager XL | 100–500 sensors | 96–192 | 1–4 TB | 76.8+ TB NVMe (RAID 10) |

---

> Elasticsearch and ClickHouse use Manager storage for event retention. 19.2 TB (Manager STD) supports approximately 90 days of full event retention at typical enterprise traffic volumes. Add storage or nodes if you need longer retention.

### [Attach the ISO](/docs/mdndr/installation-guide/online-installation#attach-the-iso)

**VMware ESXi / vCenter:**

1. Upload the NDR v5 ISO to your datastore.
2. Edit VM Settings → **CD/DVD Drive** → Datastore ISO File → select the ISO.
3. Select **Connect at Power On**.

**VMware Workstation / Fusion:**

1. VM Settings → **CD/DVD** → Use ISO Image File → browse to the NDR v5 ISO.

**Proxmox VE:**

1. Upload the ISO to **local (pve) → ISO Images**.
2. VM → Hardware → **Add → CD/DVD Drive** → select the ISO from storage.
3. Set the boot order to boot from the CD drive first.

**KVM / virt-manager:**

1. Add Hardware → **Storage** → Select custom storage → ISO file.
2. Set boot device to CD-ROM in the Boot Options tab.

---

### [Install from the ISO](/docs/mdndr/installation-guide/online-installation#install-from-the-iso)

1. Power on the VM.
2. When the **NDR boot menu** appears, select **Install NDR Platform**.
3. Press Enter.
4. > To install with FIPS 140-2 cryptographic enforcement (required for US federal or regulated environments), select **Install NDR Platform (FIPS Mode)** instead.

   > You **cannot enable FIPS mode after installation** — you must re-image to switch.
5. Wait until the automated Oracle Linux 9 OS installation completes (~10–20 minutes).
6. Let the VM reboot automatically.
7. After reboot, use the **NDR First-Boot Guided Installer** on the console (tty1).
8. Follow the prompts from the **Manager/Sensor Installation and Adoption (v5)** section above to complete your deployment.

---

### [Post-install: detach the ISO](/docs/mdndr/installation-guide/online-installation#post-install-detach-the-iso)

After installation, detach the ISO from the VM's CD/DVD drive. This prevents boot from it on the next restart.

> After a successful install, the VM boots directly from disk and the ISO is no longer needed. It is harmless but unnecessary to leave the ISO attached.
