<!-- source: https://www.opswat.com/docs/cm/deployment/virtual-appliance-deployment -->

# Virtual Appliance Deployment

### Before you begin

- Before you begin the installation, ensure that your On-premise environment meets the [System Requirements](https://www.opswat.com/docs/cm/deployment/system-requirements)
- Access to the hypervisor (vSphere/ESXi 7.0 U3, 8.0, VirtualBox )
- Network information: IP, subnet, gateway, DNS (for static IP)
- NTP connectivity for time synchronization
- SSH key (recommended) or temporary password for secure login
- Security best practices:
  - Change all default passwords immediately after the first login
  - Prefer SSH key authentication; only enable password authentication temporarily if strictly needed, and disable it afterwards
  - Restrict SSH access to admin networks via ACLs/firewalls

### OVA deployment

1. Download the My OPSWAT Central Management On-Prem Virtual Appliance [OVA] from[ My OPSWAT](https://my.opswat.com/portal/home/myopswat-central-management).
2. Import/Deploy the OVA into [virtualization systems](https://www.opswat.com/docs/cm/deployment/system-requirements#virtual-appliance-ova).
3. VMware ESXi/vSphere: Select “Deploy OVF Template”, point to the OVA file, follow the wizard, and choose the appropriate datastore, network, storage, and the guest operating system is Red Hat Enterprise Linux 9 (64-bit) or a more recent version.
4. Assign VM resources: CPU, RAM, and disk size according to the recommendations.
5. Connect the VM NIC to the appropriate management network; ensure Internet egress (if required) and access to necessary internal services.
6. Enable hypervisor time synchronization (if available) to assist with initial time sync.

![](https://uploads.developerhub.io/prod/97qW/lrbafxrx7bn9ligw0971cx9bksgv97bu2kdh4yie5exccbzkwi827khssvasv19f.png)

### First boot and login

1. Power on the VM and open the console from the hypervisor, wait for 4-5 minutes as the system initializes.
2. Log in using the default account provided with the OVA (ocm/ocm123).
3. Give the VM a static IP address. This form will default to the IP address assigned by DHCP, but you can set it to whatever makes sense for your environment.

Immediately after logging in, change the administrator password and configure SSH key‑based access to harden security.

### Initial setup (initialization)

Run the following steps in order. Commands require sudo privileges.

```bash
# 1) Elevate privileges when necessary
sudo -s
# 2) Change the current account password
passwd
# 3) (Optional) Temporarily enable SSH password login
# Recommendation: use SSH keys. Only enable this temporarily if needed.
sed -i 's/^#\?PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config.d/50-cloud-init.conf
systemctl reload sshd
# 4) Check disk capacity
lsblk
df -h
# 5) Check and sync time
chronyc tracking || timedatectl status
timedatectl set-ntp true
# 6) Initialize filesystem and relabel SELinux (answer "yes" when asked to relabel)
/opt/mocm/lib/init-filesystem.sh
# 7) Reboot the VM and wait for 4-5 minutes as the system start up
reboot
```

During `init-filesystem.sh`, the system may ask to confirm SELinux relabel. Answer “yes” to ensure correct security labels before application services start.

### Starting services (start targets)

After the VM reboots and you log in again:

```bash
# Start application targets/services
sudo systemctl start mocm-infra.target
sudo systemctl start mocm-all.target
sudo systemctl enable mocm-all.target

# Verify status
systemctl status mocm-all.target --no-pager
journalctl -u mocm-all.target -b --no-pager | tail -n 200
```

### Post‑installation checks

- Services: Confirm `systemctl status mocm-all.target` for main targets/services shows `active`.
- Network: Ping gateway/DNS, test name resolution, and verify connectivity to required internal/external endpoints.
- Time: `chronyc tracking` or `timedatectl` should show stable NTP sync.
- Disk: Use `df -h` to confirm expected capacity and mount points.

### Access the User Interface

Once all services are up and running, you can access the [Setup wizard](https://www.opswat.com/docs/cm/deployment/setup-wizard) via your web browser:

- **URL:** `<server_ip>:9000/loading`

*(Replace <server_ip> with the actual IP address of your mocm server.)*
