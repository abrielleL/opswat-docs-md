<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/fail-open-mode -->

# Fail-Open Mode

The Fail Open feature ensures continued network connectivity if the switch is unable to communicate with the RADIUS server. When this feature is enabled, any authenticated devices are automatically assigned to the specified Fail Open VLAN, maintaining network access under these circumstances.

**Enable Fail Open Mode**

1. Login to your NAC VM as 'admin' user
2. Navigate to **Failover Mode**
3. Input a specific VLAN
4. Select **Enable Failover mode**
5. Upon enable successfully, any devices authenticate to the Network will be assigned to the VLAN

![](https://uploads.developerhub.io/prod/97qW/b118c34bcxziclc7230tf91xent8z4jkgaro7s4e58iagqt2jntghz84prygc7qw.png)

**Note**: While Fail Open mode is enabled, all authenticated devices will not write session on My OPSWAT Central Management console --> Logs --> RADIUS Events.
