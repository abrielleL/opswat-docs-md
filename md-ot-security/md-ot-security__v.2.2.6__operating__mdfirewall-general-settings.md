<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/mdfirewall-general-settings -->

# General Settings

The **General Settings** is accessible under **Settings → General Settings**

General Settings page contains the information and configurations that help other networks or devices communicate with MetaDefender Industrial Firewall & IPS.

In the **Settings** menu, click **General Settings**, you can change the values:

- **Timezone:** Show timezone of the appliance. The MetaDefender Industrial Firewall & IPS timezone is synchronized with MetaDefender OT Security.
- **Hostname:** Label specified for the device. This name is used in events and logs.
- **SSH Port: (used for troubleshooting by OPSWAT)** Secure Shell (SSH) is a cryptographic network protocol that lets network services operate securely over an unsecured network. The standard TCP port is 22.
- **SLMP Learn Port:** Port where Seamless Message Protocol is learned. The usual default SLMP port is 1025.
- **DICOM Learn Port:** Port where DICOM is learned. The usual default DICOM port is 104.
- **Session Timeout:** Number of minutes a session can stay open
- **Login Message:** Text that shows after a user logs on the appliance.
- **Fail Open:** Bypass function on the appliance that allows network traffic to keep passing through even if the appliance fails. It should always be **Enabled**, but if it is **Disabled** it signals possible problems. It is not editable.
- **ICMP Block:** ICMP traffic is blocked by default. You can Disable the block or Enable it.
- **IPv6 Block:** Usually, IPv6 traffic is not found in an industrial environment, so by default all IPv6 traffic is blocked. You can Disable this block or Enable it again.
- **Randomize Server Response Header:** Security option that helps to hide your server information. It can be **Enabled** or **Disabled**.
- **Dongle Constraint:** By default, you need a USB dongle to log in. You can turn this option on or off.
- **Learning UDP Protocol:** Support learning the unsupported UDP protocol. Default is disable.

Click the **Save** button to save your changes. User have to reboot MetaDefender Industrial Firewall & IPS to apply the changes.
