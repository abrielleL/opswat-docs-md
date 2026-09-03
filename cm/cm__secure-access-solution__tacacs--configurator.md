<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/tacacs--configurator -->

# TACACS+ Configurator

## 1. Overview

TACACS+_NG integrates with LDAP through several connected components. The core service **tac_plus-ng** handles AAA requests from network devices and listens on **TCP port 49**. It relies on the **MAVIS framework** which mediates between TACACS+ and external identity sources via the MAVIS LDAP module (`mavis_tacplus_ldap.pl`), which binds to the AD/LDAP server and validates credentials.

---

## 2. Prerequisites

| Item | Details |
| ---- | ---- |
| k0s cluster | Running, `k0s kubectl get nodes` returns Ready |
| Helm | Installed, `helm version` works |
| Existing release | `nac-appliance` deployed in namespace `cloudnac` |
| Release package | `tacacs-ng-release.tar` obtained from OPSWAT and copied to the VM |
| Disk space | At least 1 GB free in `/home/nac/` |

---

## 3. Deployment Steps

### Step 1 — Copy the release package to the customer VM

Obtain `tacacs-ng-release.tar` from OPSWAT (via secure file share, USB, or any available transfer method) and place it at `/home/nac/` on the customer VM.

If you have SCP access to the VM:

```bash
scp tacacs-ng-release.tar nac@<customer-vm-ip>:/home/nac/
```

> **Info**
>
> The release package contains: `tacacs-nglatest.tar` (Docker image), `tacplus-ng.cfg` (config template), and `addtacacsng.sh` (deploy script).

---

### Step 2 — Extract the release package

On the customer VM:

```bash
cd /home/nac
tar -xvf tacacs-ng-release.tar
mkdir -p nac-images tacacs/etc
mv -f tacacs-ng-release/tacacs-ng_latest.tar nac-images/
mv -f tacacs-ng-release/tac_plus-ng.cfg tacacs/etc/
mv -f tacacs-ng-release/add_tacacs_ng.sh .
chmod +x add_tacacs_ng.sh
```

---

### Step 3 — Edit the config file for the customer environment

Open `/home/nac/tacacs/etc/tac_plus-ng.cfg` and update the following values to match the customer's AD/LDAP environment:

| Field | Description |
| ---- | ---- |
| `LDAP_HOSTS` | Customer AD/LDAP server IP and port, e.g. `192.168.1.10:389` |
| `LDAP_BASE` | Base DN, e.g. `dc=company,dc=local` |
| `LDAP_USER` | Bind account, e.g. `Administrator@company.local` |
| `LDAP_PASSWD` | Bind account password |
| `key` (in `host world` block) | Shared secret — must match what is configured on the network device |

```bash
nano /home/nac/tacacs/etc/tac_plus-ng.cfg
```

> **Info**
>
> ⚠️ Do not skip this step. Running the script before editing the config will deploy tacacs-ng with placeholder LDAP values that will not authenticate any users.

The full default `tac_plus-ng.cfg` template:

```bash
#!/usr/local/sbin/tac_plus-ng
id = spawnd {
    listen = { port = 49 }
    spawn = { instances min = 1 instances max = 10 }
    background = no
}

id = tac_plus-ng {
    log authzlog { destination = /var/log/tac_plus-ng/authz.log }
    log authclog { destination = /var/log/tac_plus-ng/authc.log }
    log acctlog { destination = /var/log/tac_plus-ng/acct.log }
    accounting log = acctlog
    authentication log = authclog
    authorization log = authzlog

    mavis module = groups {
        groups filter = /^(NetworkAdmins|NetworkOperator)$/
    }

    mavis module = external {
        setenv LDAP_SERVER_TYPE = "microsoft"
        setenv LDAP_HOSTS = "192.168.99.101:389"
        setenv LDAP_BASE = "dc=mgmlab,dc=local"
        setenv LDAP_USER = "Administrator@mgmlab.local"
        setenv LDAP_PASSWD = "Fvl123456!"
        setenv TACACS_GROUP_PREFIX = ""
        setenv UNLIMIT_AD_GROUP_MEMBERSHIP = 1
        setenv REQUIRE_TACACS_GROUP_PREFIX = 0
        exec = /usr/local/lib/mavis/mavis_tacplus_ldap.pl
    }

    login backend = mavis
    user backend = mavis
    pap backend = mavis

    host world {
        address = 0.0.0.0/0, ::/0
        welcome banner = "*** Welcome to NAC Appliance TACACS+ ***\n"
        enable 15 = clear SECRETENABLEPASSWORD
        anonymous-enable = deny
        key = "HelloMetaAccess"
    }

    profile admins {
        script {
            if (service == shell) {
                if (cmd == "") { set priv-lvl = 15 permit }
                permit
            }
        }
    }

    profile operators {
        script {
            if (service == shell) {
                if (cmd == "") { set priv-lvl = 1 permit return }
                if (cmd =~ /^enable/) { permit return }
                if (cmd =~ /^config/) { deny return }
                if (cmd =~ /^show/) { permit return }
                deny
            }
        }
    }

    group admins
    group operators

    ruleset {
        rule {
            script {
                if (memberof =~ /NetworkAdmins/) { profile = admins permit return }
                if (memberof =~ /NetworkOperator/) { profile = operators permit return }
                deny
            }
        }
    }
}
```

---

### Step 4 — Run the deployment script

```bash
sudo /home/nac/add_tacacs_ng.sh
```

The script performs these actions automatically:

| Action | Details |
| ---- | ---- |
| Verify prerequisites | helm, k0s, chart path |
| Import image | `k0s ctr image import tacacs-ng_latest.tar` |
| Patch values.yaml | Inserts `tacacsNg:` block using `sed` (idempotent) |
| Create host dirs | `/home/nac/tacacs/etc/` and `/home/nac/tacacs/log/tac_plus-ng` |
| Detect host IP | Via `ip route` / `ip addr` |
| `helm upgrade` | Upgrades the existing release to add tacacs-ng |
| Verify pod | Waits up to 120 s for the pod to be Ready |

Deployment logs are written to: `/etc/nac-appliance/onboarding/logs/tacacs-ng.log`

---

### Step 5 — Verify the deployment

```bash
# Pod status
k0s kubectl get pods -n cloudnac -l app.kubernetes.io/component=tacacs-ng

# Service — should show externalIP and port TCP/49
k0s kubectl describe svc nac-appliance-tacacs-ng -n cloudnac

# Container logs
k0s kubectl logs -n cloudnac -l app.kubernetes.io/component=tacacs-ng -f

# TCP/49 connectivity test
nc -zv <customer-vm-ip> 49
```

Expected pod output:

```plaintext
NAME                                    READY   STATUS    RESTARTS   AGE
nac-appliance-tacacs-ng-<hash>          1/1     Running   0          1m
```

---

## 4. Configure Network Devices

### 4.1 Palo-Alto

**Device > Server Profiles > TACACS+** → Add new profile:

| Field | Value |
| ---- | ---- |
| Profile Name | NAC-TACACS |
| Server IP | `<customer-vm-ip>` |
| Port | 49 |
| Shared Secret | must match `key` in `tac_plus-ng.cfg` |
| Timeout | 10s |

Then: **Device > Setup > Management > Authentication Settings** → select the profile.

Role mapping: **Device > Admin Roles** → `priv-lvl=15` = superuser, `priv-lvl=1` = read-only.

### 4.2 Fortigate

**System > Authentication > TACACS+ Servers** → Create New:

| Field | Value |
| ---- | ---- |
| Name | NAC-TACACS |
| Server IP | `<customer-vm-ip>` |
| Port | 49 |
| Key | must match `key` in `tac_plus-ng.cfg` |
| Authentication type | PAP |

Then: **System > Administrators** → create/edit admin → Authentication: **TACACS+** → select profile.

### 4.3 Cisco

```plaintext
aaa new-model
aaa authentication login default group tacacs+ local
aaa authentication enable default group tacacs+
aaa authorization exec default group tacacs+ local
aaa authorization commands 1 default group tacacs+ local
aaa authorization commands 15 default group tacacs+ local
aaa accounting exec default start-stop group tacacs+
aaa accounting commands 1 default start-stop group tacacs+
aaa accounting commands 15 default start-stop group tacacs+

tacacs server NAC-TACACS
    address ipv4 <customer-vm-ip>
    key <shared-secret>
```

---

## 5. AD Group Setup

| AD Group | TACACS+ Profile | Privilege Level | Permissions |
| ---- | ---- | ---- | ---- |
| `NetworkAdmins` | admins | 15 | Full access — enable + config mode on all devices |
| `NetworkOperator` | operators | 1 | Show commands only — config commands denied |

---

## 6. Rollback

```bash
# Roll back entire Helm release to previous revision
helm rollback nac-appliance -n cloudnac

# Or just disable tacacs-ng without full rollback
sed -i '/^tacacsNg:/,/^[^ ]/{s/enabled: true/enabled: false/}' \
    /home/nac/nac-edge-helm/values.yaml

helm upgrade nac-appliance /home/nac/nac-edge-helm \
    --values /home/nac/nac-edge-helm/values.yaml \
    --set global.hostIP="${HOST_IP_ADDRESS}" \
    --namespace cloudnac --timeout 5m
```

---

## 7. Device Onboarding Templates (Customer Devices)

This section provides TACACS+ configuration templates for all network device families identified for onboarding. Replace `<TACACS_SERVER_IP>` with the NAC Appliance host IP and `<SHARED_SECRET>` with the `key` value in `tac_plus-ng.cfg`.

### Supported Device Summary

| Vendor | Devices | Firmware | TACACS+ Support |
| ---- | ---- | ---- | ---- |
| Arista | 7538, 7050SX3-48C8C, 7050SX3-48YC8C, 720DT-24S-M-S-2, 7280CR3-32D4, 7280SR3E-40YC6-M, 7508N | 4.34.3M | ✅ Full |
| Juniper | EX-4100, MX10003, MX204, MX240, MX-304, QFX10002, QFX10008, QFX5120, SRX5400, SRX5800, PTX-10001, SRX1500, SRX380-POE-AC | 22.4R3-S6.5 | ✅ Full |
| Palo Alto | PA-5430, PA-5450 | 11.1.13 | ✅ Full |
| Fortinet | FG-901G, FG-7081F | 7.4.9 | ✅ Full |
| F5 BIG-IP | r10600, r5600, r5800 | 17.5.1.4 | ✅ Full (VSA required) |
| Trellix NSM | Sensor 9600, NSM Manager | 11.1.x | ❌ No TACACS+ — use LDAP/AD |

---

### 7.1 Arista EOS (4.34.3M)

Applies to all Arista models listed above. Run these commands in global config mode.

```plaintext
! TACACS+ server
tacacs-server host <TACACS_SERVER_IP> key 7 <SHARED_SECRET>
tacacs-server timeout 10

! AAA server group
aaa group server tacacs+ NAC-TACACS
    server <TACACS_SERVER_IP>

! Authentication
aaa authentication login default group NAC-TACACS local
aaa authentication enable default group NAC-TACACS local

! Authorization
aaa authorization exec default group NAC-TACACS local
aaa authorization commands all default group NAC-TACACS local

! Accounting
aaa accounting exec default start-stop group NAC-TACACS
aaa accounting commands all default start-stop group NAC-TACACS
aaa accounting system default start-stop group NAC-TACACS
```

> **Info**
>
> Arista EOS maps `priv-lvl=15` to full privilege and `priv-lvl=1` to restricted mode natively — no additional role configuration required when `tac_plus-ng.cfg` sets `priv-lvl` correctly.

---

### 7.2 Juniper Junos (22.4R3-S6.5)

Applies to all Juniper models listed above (EX, MX, QFX, SRX, PTX series).

```plaintext
# TACACS+ server
set system tacplus-server <TACACS_SERVER_IP> secret "<SHARED_SECRET>"
set system tacplus-server <TACACS_SERVER_IP> timeout 10
set system tacplus-server <TACACS_SERVER_IP> single-connection

# Authentication order: TACACS+ first, fall back to local
set system authentication-order [ tacplus password ]

# Login classes for role mapping
set system login class TACACS-ADMIN permissions all
set system login class TACACS-ADMIN allow-commands ".*"
set system login class TACACS-ADMIN deny-commands ""

set system login class TACACS-OPERATOR permissions [ view view-configuration ]
set system login class TACACS-OPERATOR allow-commands "(show|ping|traceroute|help|exit|quit)"
set system login class TACACS-OPERATOR deny-commands "(request|set|delete|run|clear)"

# Wildcard remote user — required for TACACS+ logins
set system login user remote full-name "TACACS Remote User"
set system login user remote class TACACS-OPERATOR
```

> **Info**
>
> Junos note: The `remote` user class acts as the default. For `NetworkAdmins`, configure `tac_plus-ng.cfg` to return `service=junos-exec { local-user-name = TACACS-ADMIN }` as a per-device authorization attribute, which overrides the default class at login time.

---

### 7.3 Palo Alto PAN-OS (11.1.13)

Applies to PA-5430 and PA-5450.

**CLI (set commands):**

```plaintext
set shared server-profile tacacs TACACS-NAC server <TACACS_SERVER_IP> port 49
set shared server-profile tacacs TACACS-NAC server <TACACS_SERVER_IP> secret <SHARED_SECRET>
set shared server-profile tacacs TACACS-NAC use-single-connection yes
set shared server-profile tacacs TACACS-NAC timeout 10

set shared authentication-profile TACACS-AUTH protocol TACACS+
set shared authentication-profile TACACS-AUTH server-profile TACACS-NAC
set shared authentication-profile TACACS-AUTH allow-list all

set deviceconfig system authentication-profile TACACS-AUTH
```

**GUI path:** Device > Server Profiles > TACACS+ → create profile → Device > Authentication Profile → link profile → Device > Setup > Management > Authentication Settings → select profile.

**Admin Role mapping:**

| priv-lvl from TACACS+ | PAN-OS Role |
| ---- | ---- |
| 15 | Superuser (full access) |
| 1 | Device Reader (read-only) |

---

### 7.4 Fortinet FortiOS (7.4.9)

Applies to FG-901G and FG-7081F.

```plaintext
# TACACS+ server definition
config user tacacs+
    edit "TACACS-NAC"
        set server <TACACS_SERVER_IP>
        set key <SHARED_SECRET>
        set authen-type pap
        set port 49
end

# Admin access profiles
config system accprofile
    edit "TACACS-FULL-ACCESS"
        set secfabgrp read-write
        set ftviewgrp read-write
        set authgrp read-write
        set sysgrp read-write
        set netgrp read-write
        set loggrp read-write
        set routegrp read-write
        set fwgrp read-write
        set vpngrp read-write
        set utmgrp read-write
    edit "TACACS-READ-ONLY"
        set secfabgrp read
        set ftviewgrp read
        set authgrp read
        set sysgrp read
        set netgrp read
        set loggrp read
        set routegrp read
        set fwgrp read
        set vpngrp read
        set utmgrp read
end

# User group linked to TACACS+ server
config user group
    edit "TACACS-ADMINS"
        set member "TACACS-NAC"
end

# Wildcard admin using TACACS+ auth
config system admin
    edit "tacacs_admin"
        set remote-auth enable
        set accprofile "TACACS-FULL-ACCESS"
        set wildcard enable
        set remote-group "TACACS-ADMINS"
end
```

> **Info**
>
> For read-only users, create a separate wildcard admin entry pointing to `TACACS-READ-ONLY` profile and map it to a different TACACS+ group (`NetworkOperator`).

---

### 7.5 F5 BIG-IP TMOS (17.5.1.4)

Applies to r10600, r5600, r5800 (configured at the BIG-IP tenant/TMOS level, not the rSeries chassis).

**TMSH commands:**

```plaintext
# Configure TACACS+
tmsh modify auth tacacs system-auth {
    secret <SHARED_SECRET>
    servers add { <TACACS_SERVER_IP> }
    service ppp
    protocol ip
}

# Set auth source
tmsh modify auth source { type tacacs }

# Remote role mapping via VSA
tmsh modify auth remote-role {
    role-info add {
        TACACS-ADMIN {
            attribute "F5-LTM-User-Info-1=admin"
            console tmsh
            line-order 10
            role administrator
            user-partition All
        }
        TACACS-OPERATOR {
            attribute "F5-LTM-User-Info-1=operator"
            console tmsh
            line-order 20
            role operator
            user-partition Common
        }
    }
}

# Default fallback for unmatched remote users
tmsh modify auth remote-user {
    default-role operator
    default-partition Common
}

tmsh save sys config
```

> **Info**
>
> F5 VSA requirement: F5 uses the `F5-LTM-User-Info-1` Vendor Specific Attribute for role assignment. Add a device-specific host block in `tac_plus-ng.cfg` for F5 management IPs, returning this VSA in the authorization response:

>

> **Info**
>
> host f5-devices {>         address = <F5-management-subnet>/24>         key = "<SHARED_SECRET>">         service = ppp {>             protocol = ip {>                 F5-LTM-User-Info-1 = admin>             }>         }>     }

**F5 Devices in scope:**

| Model | Hostname | Firmware |
| ---- | ---- | ---- |
| r10600 | DC2-B78-L4LB01, DC2-A88-L4LB02 | 17.5.1.4 |
| r5600 | DC2-B81-SSL-VPNGW01, DC2-A91-SSL-VPNGW02 | 17.5.1.4 |
| r5600 | DC2-B79-LB-WAF01, DC2-A89-LB-WAF02 | 17.5.1.4 |
| r5800 | DC2-B80-ADOS01, DC2-A90-ADOS02 | 17.5.1.4 |

---

### 7.6 Trellix Network Security (NSM + Sensors)

Applies to: Sensor DC2-IPS02-A90 (v11.1.5.139), Manager DC2-NSM01-B80 (v11.1.7.136.2)

> **Info**
>
> ❌ Trellix Network Security Platform does not support TACACS+. Administrative authentication on Trellix NSM supports:> > - Local user accounts (built-in)> - LDAP / Active Directory integration> - RADIUS (select versions only)

>

> **Info**
>
> Recommended approach: Configure Trellix NSM to authenticate via Active Directory / LDAP directly — the same AD that backs TACACS+ for all other devices. This achieves unified identity management without requiring TACACS+ support from Trellix.

---
