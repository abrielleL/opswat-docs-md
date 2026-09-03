<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net -->

# How to de-integrate NAC from a Layer 2 / Layer 3 network (RBE/PBR)?

This article applies to a range of supported network management devices, the current NAC Enforcer and the Web UI.

To de-integrate or remove NAC from a Layer 2 or Layer 3 network, please follow the relevant instructions below.

Each set of instructions applied to a specific network management device and brand.

If you do not see your network device listed, please open a case with **OPSWAT Support** by following the instructions in the support box at the end of this article.

Pro Tip:

These steps should only be followed if approved by **OPSWAT Support**, or if enforcement has already been disabled in the NAC UI as defined in [This Article](https://docs.opswat.com/manac/nac-v8.0.7/knowledge-base/how-to-toggle-enforcement-on-layer-2-or-layer-3-networks--rbe-pb).

## [RBE (Layer 2 - RADIUS Based Enforcement)](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#rbe-layer-2----radius-based-enforcement)

### [Aruba Controllers](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aruba-controllers)

#### [Aruba Open or PSK SSIDS](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aruba-open-or-psk-ssids)

- Execute the following command on the **master controller**.

conf t
!
aaa profile "Customer's Open Profile"
no authentication-mac
!
end
!
write mem

- To prevent devices getting stuck in a blocked state, you can have the system mark all devices in quarantined states as compliant, by executing the following command.

aaa user delete role "SC_Quarantine_Role"

- To re-integrate NAC, type the following command.

conf t
!
aaa profile "Customer's Open Profile"
authentication-mac
!
end
!
write mem
#### [Aruba WPA2E SSIDS](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aruba-wpa2e-ssids)

Please Note:

The following method is only applicable to infrastructures that include at least one RADIUS server in addition to NAC.

This method cannot be used in cases where NAC is the only RADIUS server, as there must be an alternate RADIUS server to point at.

1. To remove RBE from the RADIUS path of your network, you must remove or demote the entry pertaining to the RBE server from the controller’s RADIUS configurations.

- Navigate to **Configuration>Authentication>AAA Profiles**, and select the **802.1X Authentication Server Group** of the profile used by your SSID.
- Either delete or demote the entry for the **NAC RBE Device**.
- Alternatively, this can be done from the CLI by replacing **devradius.pd.impulse.com** with the **NAC Appliance**, and replacing **rbetest2.pd.impulse.com** with an **alternate RADIUS server**, as illustrated below.

conf t
!
aaa server-group "Imp_PD_Dev_srvgrp-cdp10"
no auth-server "devradius.pd.impulse.com"
auth-server "rbetest2.pd.impulse.com" position 1
!
end
!
write mem

2. To prevent devices getting stuck in a blocked state, you can have the system mark all devices in quarantined states as **Compliant**, by executing the following command.

aaa user delete role "SC_Quarantine_Role"

3. To re-integrate NAC, enter the following command.

conf t
!
aaa server-group "Imp_PD_Dev_srvgrp-cdp10"
auth-server "devradius.pd.impulse.com" position 1
!
end
!
write mem
### [Cisco Controllers](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#cisco-controllers)

#### [Cisco Open SSIDS (AireOS versions prior to and including V 8.3.102.0)](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#cisco-open-ssids-aireos-versions-prior-to-and-including-v-831020)

1. To turn MAC filtering off, click on **WLAN>Security>Layer 2**, then uncheck **MAC Filtering**.
2. To set Layer 3 Security to None, click on **WLAN>Security>Layer 3**, then select **None** from the drop-down menu.
3. To uncheck AAA Override, click on **WLAN>Advanced**, then uncheck **AAA Override**, as illustrated below.

To re-integrate NAC, do the following.

4. To turn MAC filtering on, click on WLAN>Security>Layer 2, then check MAC Filtering.

5. To set Layer 3 Security to Web Policy, click on **WLAN>Security>Layer 3**, select **Web Policy** from the drop-down menu, then ensure that both **On MAC Filter Failure** and the **sc_quarantine_acl** ACL are selected.

6. To check AA Override, click on **WLAN>Advanced**, then check **AAA Override**.

#### [Cisco Open SSIDS (AireOS versions subsequent to and including V8.3.102.0)](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#cisco-open-ssids-aireos-versions-subsequent-to-and-including-v831020)

1. To turn MAC filtering off, click on **WLAN>Security>Layer 2**, then uncheck **MAC Filtering**.
2. To uncheck AAA Override, click on **WLAN>Advanced**, then uncheck **AAA Override**.

To re-integrate NAC, do the following.

3. To turn MAC filtering on, click on **WLAN>Security>Layer 2**, then check **MAC Filtering**.
4. To check AAA Override and set the NAC State, click on **WLAN>Advanced**, then check **AAA Override** and select **Radius NAC** or **ISE NAC**.

#### [Cisco WPA2E SSIDS](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#cisco-wpa2e-ssids)

Please Note:

The following method is only applicable to infrastructures that include at least one RADIUS server in addition to NAC.

This method cannot be used in cases where NAC is the only RADIUS server, as there must be an alternate RADIUS server to point at.

1. To set the RADIUS authentication server to an alternate RADIUS server, navigate to **WLAN>Security>AAA Servers**, then set **Server 1** to **Alternate RADIUS Server**.
2. To set Allow AAA Override to Disabled and set the NAC state to None, navigate to **WLAN>Advanced**, then uncheck **Allow AAA Override** and set **NAC State** to **None**.

To re-enable NAC, do the following.

3. To set the RADIUS authentication server to NAC RADIUS server, navigate to **WLAN>Security>AAA Servers**, then set **Server 1** to **NAC RADIUS Server**.
4. To check AAA Override and set the NAC State, click on **WLAN>Advanced**, then check **AAA Override** and select **Radius NAC** or **ISE NAC**.

### [Aerohive Controllers](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aerohive-controllers)

#### [Aerohive HM6 Open, WEP, WPAPSK WLANS](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aerohive-hm6-open-wep-wpapsk-wlans)

1. To disable MAC authentication, navigate to **Configuration>SSIDs>(Name of Open / WEP or WPAPSK SSID)**, then uncheck **Enable MAC Authentication**, click **Save** and push the updated policy.
2. To re-integrate NAC, navigate to **Configuration>SSIDs>(Name of Open / WEP or WPAPSK SSID**, then check **Enable MAC Authentication**, click **Save** and push the updated policy.

#### [Aerohive HM6 WPA2E/802.1X WLANS](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aerohive-hm6-wpa2e8021x-wlans)

1. Navigate to **Configuration>SSIDs>(Name of Secure SSID**), then change **SSID Access Security** to **Open**, click **Save** and push the updated policy.
2. To re-integrate NAC, navigate to **Configure>SSIDs>(Name of Secure SSID)**, then change **SSID Access Security** to **WPA/WPA2 802.1X (Enterprise)**, click **Save** and push the updated policy.

#### [Aerohive HMNG Open, WEP, or WPAPSK WLANs](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aerohive-hmng-open-wep-or-wpapsk-wlans)

1. To turn off MAC authentication, navigate to **Configure>(Name of policy)>Wireless Settings>(Name of Secure SSID)>MAC Authentication**, then disable **MAC Authentication**, click **Save** and push the updated policy.
2. To re-integrate NAC, navigate to **Configure>(Name of Policy)>Wireless Settings>(Name of Secure SSID)>Mac Authentication**, then enable **MAC Authentication**, click **Save** and push the updated policy.

#### [Aerohive HMNG WPA2E/802.1X WLANs](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#aerohive-hmng-wpa2e8021x-wlans)

1. Navigate to **Configure>(Name of Policy)>Wireless Settings>(Name of Secure SSID)**, then change **SSID Access Security** to **Open**, click **Save** and push the updated policy.
2. To re-integrate NAC, navigate to **Configure>(Name of Policy)>Wireless Settings>(Name of Secure SSID)**, then change **SSID Access Security** to **Enterprise**, click **Save** and push the updated policy.

## [PBR (Layer 3 - Policy Based Routing)](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#pbr-layer-3----policy-based-routing)

To clear the **opswat_block AC**L, enter the device-relevant commands and instructions below.

### [NEXUS Router](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#nexus-router)

conf t
!
no ip access-list opswat_block
!
ip access-list opswat_block
permit ip any host 198.31.193.211
!
end
### [Cisco/Brocade ICX Router (Non NEXUS Router)](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#ciscobrocade-icx-router-non-nexus-router)

conf t
!
no ip access-list extended opswat_block
!
ip access-list extended opswat_block
permit ip any host 198.31.193.211
!
end
### [Alcatel Router](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#alcatel-router)

Pro Tip:

For this router, you will need to confirm the policy network group, as the group may be named **blockedhost** rather than **opswat_block** on some legacy devices.

If this is the case, replace **opswat_block** with **blockedhost** (or the given **name** on your specific device) before executing the script.

no policy rule block
!
no policy condition noncompliant
!
no policy network group opswat_block
!
policy network group opswat_block 169.254.0.1
!
policy condition noncompliant source network group opswat_block vrf default
!
policy rule block precedence XXX condition noncompliant action next-hop-enforcer
!
qos apply
!
write memory
!
copy working certified
### [HP Router](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#hp-router)

config
!
policy pbr opswat
no class ipv4 opswat_block
exit
!
no class ipv4 opswat_block
!
class ipv4 opswat_block
match ip any 198.31.193.211/32
exit
!
policy pbr opswat
class ipv4 opswat_block
action ip next-hop x.x.x.x - Must replace with Enforcer IP
exit
!
exit
!
wr mem
### [Huawei Router](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#huawei-router)

config
!
traffic policy opswat
undo classifier opswat_block behavior impulse_block precedence 5
!
traffic classifier opswat_block type or
undo if-match acl opswat_block
!
undo acl name opswat_block advance
!
acl name opswat_block advance
rule 5 permit ip destination 198.31.193.211 0
!
traffic classifier opswat_block type or
if-match acl opswat_block
!
traffic policy opswat
classifier opswat_block behavior opswat_block precedence 5
!
commit
!
quit
### [MLX Router](/docs/manac/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net#mlx-router)

conf t
!
no ip access-list extended opswat_block
!
ip access-list extended opswat_block
permit ip any host 198.31.193.211
!
ip rebind-acl opswat_block
!
end
!
wr memPro Tip:

If you encounter the following error:

**​​telnet@BG-MLX8-Core2(config)#no ip access-list extended opswat_block**

**Cannot delete l4 access-list opswat_block : Currently in use by PBR.**

**error - ACL In Use.**

Execute the following script:

**acl-policy**

**force-delete-bound-acl**

The following script is for removing the NAC route map, where **X = the Layer 3 interface that has the route map applied**.

X can be determined by issuing a **show ip policy** command, then reviewing the results to determine which interfaces have the route map applied.

conf t
!
interface X
no ip policy route-map opswat
!
end

Then, to restore the NAC route map, enter the following script.

conf t
!
interface X
ip policy route-map opswat
!
endSupport:

If you have followed the instructions above but have been unable to **De-Integrate NAC From A Layer 2 / Layer 3 (RBE/PBR) Network**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
