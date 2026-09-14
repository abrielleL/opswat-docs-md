<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention -->

# Threat Prevention (OPSWAT Industrial Firewall)

First, users need to select a sensor from the list at the top-right corner.

The list of OPSWAT Industrial Firewall contains all the information about OPSWAT Industrial Firewall in the system.

## [1. Mange the OPSWAT Industrial Firewall](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#1-mange-the-opswat-industrial-firewall)

### [Add OPSWAT Industrial Firewall](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#add-opswat-industrial-firewall)

Can add the OPSWAT Industrial Firewall by add manually or populate:

- Add manually: clicking on the Add IFW at the top right corner then input name and IP address

- Add manually: clicking on the Add IFW at the top right corner then input name and IP address

- Populate: clicking on the Populate IFW at the top right corner then the MetaDefender OT Security will auto detect all OPSWAT Industrial Firewall in the system.

### [Change Stage](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#change-stage)

**Stage:** Idle/Learn/Monitor/Protect

Can change stage for each the OPSWAT Industrial Firewall by clicking on three dot of specific device → Change Stage → Select Stage → Confirm

### [Remove](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#remove)

Can remove the OPSWAT Industrial Firewall by clicking on three dot of specific device → Remove → Confirm

## [2. OPSWAT Industrial Firewall list](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#2--opswat-industrial-firewall-list)

**Each OPSWAT Industrial Firewall contains the following fields:**

- **Name**: The name of OPSWAT Industrial Firewall
- **IPv4 Address:** the IPv4 address of OPSWAT Industrial Firewall
- **IP of protected PLCs:** the IPv4 address of PLCs that are protected in the system.
- **Firmware Version**
- **Mode:** Transparent
- **Stage:** Idle/Learn/Monitor/Protect
- **License Status:** No License/Licensed
- **Connectivity Status:** Disconnected/Connected (whether MetaDefender OT Security can connect the OPSWAT Industrial Firewall device or not)
- **Disk Space Status**
- **Memory Status**

### [Sorting](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#sorting)

We support filtering on the list of OPSWAT Industrial Firewall:

- The user can ***clicking for one field then select sort type***, and the result list will be updated according to the value(s) you entered.

## [3. Protected PLCs](/docs/md-ot-security/v.3.4.0/threat-prevention/threat-prevention#3-protected-plcs)

When OPSWAT Industrial Firewall is in **Monitor Stage**, if having some unauthorized connection want to connect to 1 of PLCs that are protected by this OPSWAT Industrial Firewall.

The alert will trigger and ask user to block this connection or not. If user select Unexpected, the popup will display as below and ask user Block this connection with OPSWAT Industrial Firewall. When confirming, the OPSWAT Industrial Firewall will automatically change to **Protect Stage**.
