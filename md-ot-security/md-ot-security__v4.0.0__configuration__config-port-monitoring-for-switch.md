<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/configuration/config-port-monitoring-for-switch -->

# Config port mirroring for Switch

Currently, the MetaDefender OT Security Sensor usually runs with 3 NICs, one for **Active** scanning connected to a normal port on the switch, one for **Passive** scanning that connects to a mirror port, and one for connect to the Site manager server.

Below is the example basic setup for the system with MetaDefender OT Security Sensor.

## [Switch Port Mirroring](/docs/md-ot-security/v4.0.0/configuration/config-port-monitoring-for-switch#switch-port-mirroring)

On the switch, the user has to configure a mirror port to monitor all other ports. The mirror port will copy all traffic that goes through other ports and send it back to MetaDefender OT Security.

If the user configures port Fa0/1 as a mirror port, one of MetaDefender OT Security network interface cards must be connected to this mirror port for passive scanning, the second interface card can be connected to others (normal/monitored port) for active scanning.

**Note:** The switch OS version can supports LLDP is better. For Calalyst 2960, the OS version must be higher than 12.2(350)

Example for configuring port mirroring on Cisco switch:

PowershellCopySwitch#configure
Configuring from terminal, memory, or network [terminal]?
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#
Switch(config)#no monitor session 1
Switch(config)#monitor session 1 source interface Fa0/2 - 48
Switch(config)#monitor session 1 destination interface Fa0/1
Switch(config)#end
Switch#copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
