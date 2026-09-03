<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/captive-portal-configuration -->

# Captive Portal Configuration

## What is the Captive Portal?

The **captive portal** is a web page that MetaDefender NAC shows to a device before it is granted full access to your network. When a device connects but is not yet authenticated or not compliant, your network equipment redirects its web traffic to NAC Edge, which displays a **remediation page** — for example, a sign-in page, an agent-install prompt, or a block message. After the user completes the required action, the device is re-evaluated and given its intended level of access.

The captive portal works together with three other parts of RADIUS NAC:

- **Access Profiles** define the limited network access a device has while it is on the captive portal.
- **Rules** decide which devices are sent to the captive portal and which remediation page they see.
- **Remediation pages** are the actual pages the user sees (Block, MDE required, Guest, SSO, SSO and Guest). See [Rules — Showing a Remediation Page](rules#showing-a-remediation-page-new).

## How It Works

1. A device connects to the network and authenticates through RADIUS NAC.
2. The device is evaluated against your **Rules** (top to bottom). The first rule that matches and assigns a **Captive Portal** access profile places the device on the captive portal.
3. Your network vendor (switch, controller, or router) redirects the device's web traffic to **NAC Edge**.
4. NAC Edge shows the **remediation page** selected by that rule's **Show remediation page** action. If no page is set, the **Block** page is shown by default.
5. The user completes the required action — installs the agent, signs in as a guest, authenticates with SSO, and so on.
6. NAC re-evaluates the device and applies the access profile from the rule it now matches.

## Prerequisites

Before configuring the captive portal, make sure you have:

- A configured and connected **NAC Edge** — note its IP address; you will need it for the redirect configuration.
- An **Access Profile** you can assign to captive-portal devices (created in **RADIUS NAC → Configuration → Access Profiles**).
- A network vendor that supports either **DNAT redirect** (for example, Aruba) or **VLAN redirect** (for example, Cisco).
- For VLAN-based redirect: a **Layer 3 router or switch with ACL (Access Control List) and Policy Routing capabilities** is required.

## Step 1: Create a Captive Portal Access Profile

1. Go to **RADIUS NAC → Configuration → Access Profiles**.
2. Create an Access Profile to be used for the captive portal.

## Step 2: Create a Rule that Assigns the Captive Portal Profile

1. Go to **RADIUS NAC → Rules** and click **Add New Rule** (see [Rules](rules) for full details on conditions and actions).
2. Under **Apply these actions**, **Assign** the Captive Portal access profile you created in Step 1.
3. Add a **Show remediation page** action and select the page users should see (see [Step 4](#step-4-choose-the-remediation-page-users-see)).
4. Click **Apply** to save.

## Step 3: Configure Redirect on Your Network Vendor

How you redirect captive-portal traffic to NAC Edge depends on whether your vendor supports DNAT or VLAN redirect.

### Option A — DNAT-supported vendors (example: Aruba)

1. Create an Access Profile for the captive portal in the **Access Profiles** tab (Step 1).
2. In the **Aruba** dropdown, set the `Aruba-User-Role` attribute to your redirect role — for example, `ORG_B_2084RDR`.

3. Go to the **Rules** tab, add a rule, and assign it to the Captive Portal profile created above (Step 2).

4. On the network vendor console (Aruba in this example), create an **ACL** (Access Control List) to forward traffic to NAC Edge.

### Option B — VLAN-supported vendors (example: Cisco)

1. Create an Access Profile for the captive portal in the **Access Profiles** tab (Step 1).
2. In the **Cisco** dropdown, set the `Tunnel-Private-Group-Id` attribute to your quarantine VLAN ID — for example, `1776`.

3. **Configure the redirect for the VLAN.**

> **Pre-condition**
>
> A Layer 3 router or switch with ACL (Access Control List) and Policy Routing capabilities is required.

Apply an ACL and policy route-map on the router so that captive-portal (quarantine) traffic is forwarded to NAC Edge, while essential services (DNS, DHCP) are allowed through directly:

```bash
ip access-list extended Non_Redirect        # create IP access list (extended)
 permit udp any any eq domain               # allow DNS
 permit udp any any eq bootps               # allow DHCP
route-map CloudNac_Quarantine deny 10       # create route map
 match ip address Non_Redirect
route-map CloudNac_Quarantine permit 20
 set ip next-hop 10.40.177.85               # IP address of NAC Edge
interface GigabitEthernet0/0.1796
 description Wireless Quarantine Subnet
 encapsulation dot1Q 1796
 ip address 10.40.179.65 255.255.255.240
 ip helper-address 10.40.177.94             # DHCP server outside of this VLAN
 no ip route-cache
 ip policy route-map CloudNac_Quarantine    # apply route map CloudNac_Quarantine
```

**Values to change for your environment:**

- `10.40.177.85` — the IP address of your **NAC Edge** (`set ip next-hop`).
- `1796` (the VLAN ID in `encapsulation dot1Q` and the sub-interface) — your **quarantine VLAN**. This must match the `Tunnel-Private-Group-Id` value you set on the vendor in Step 3B.2.
- `10.40.179.65 255.255.255.240` — the gateway IP and mask for the quarantine VLAN.
- `10.40.177.94` — your **DHCP server** address (`ip helper-address`).
- `GigabitEthernet0/0.1796` — the sub-interface name for your quarantine VLAN; adjust to match your hardware.

> **Info**
>
> The `Non_Redirect` ACL permits DNS (`domain`) and DHCP (`bootps`) so quarantined devices can still resolve names and obtain an address. The route map denies redirect for that traffic (`deny 10`) and forwards everything else to NAC Edge (`permit 20` → `set ip next-hop`).

## Step 4: Choose the Remediation Page Users See

The captive portal displays a **remediation page** to the user. You choose which page in the matching rule's **Show remediation page** action (see [Rules — Showing a Remediation Page](rules#showing-a-remediation-page-new)).

Available pages:

- **Block** — a hard stop that reads "You are not allowed on this network." Shown automatically if no page is set.
- **MDE required** — prompts the user to install the MetaDefender Endpoint agent.
- **Guest**, **SSO**, and **SSO and Guest** — sign-in options for guest and/or single sign-on.

> **Info**
>
> If a device is placed on the captive portal and no matching rule sets a remediation page, the **Block** page is shown by default.

## Verify the Configuration

1. Using a test device, connect to the network.
2. Confirm the browser is redirected to the **expected** remediation page. For example, if the agent is not installed and the rule shows the **MDE required** page, the user is prompted to install the agent.

3. In **RADIUS NAC → Sessions**, confirm the device shows **Applied Access Profile = Captive Portal** and the **Applied Rule** you expect.

4. Complete the required action (install the agent, sign in, and so on), then confirm the device is re-evaluated and receives its intended access.

> **Note**
>
> Apple devices can use **DHCP option 114** on a Windows DHCP server for NAC integration with the Apple Captive Network Assistant (CNA).

## Troubleshooting

**Device is not redirected to the captive portal**

- Verify the matching rule assigns the Captive Portal access profile, and that no earlier rule matches first — rule order matters.
- Check the redirect configuration on your vendor (DNAT role, or VLAN plus policy route map).
- Confirm the `set ip next-hop` address matches your NAC Edge IP.

**The wrong page is shown, or the Block page always appears**

- Check the rule's **Show remediation page** action. If it isn't set, the Block page is shown by default.
- Make sure the rule you expect is the first one that matches.

**A quarantined device can't get an IP address or resolve DNS**

- Ensure the `Non_Redirect` ACL permits DHCP (`bootps`) and DNS (`domain`), and that `ip helper-address` points to your DHCP server.

**An Apple device doesn't open the portal automatically**

- Use DHCP option 114 (see the note above) so the Apple Captive Network Assistant opens the portal.

## Related Pages

- [Rules](rules) — conditions and actions, including Show remediation page
- Access Profiles
- Configure EAP-TLS for Cloud RADIUS Authentication
