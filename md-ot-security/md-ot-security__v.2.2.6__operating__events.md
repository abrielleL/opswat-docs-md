<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/events -->

# Events

After MetaDefender Industrial Firewall & IPS learns about your network and its connections and communication, the MetaDefender Industrial Firewall & IPS monitors the network for deviations from the learned traffic and uses the OPSWAT policy engine to flag changes from unauthorized users and messages outside of defined parameters. These policies are available by default on the MetaDefender Industrial Firewall & IPS.

A policy is a set of rules made to prevent specified actions from occurring. You can apply policies to cause a blockage of all specified actions as defined in the policies.

When an appliance operates in **Monitor** mode, it compares new network activity against the learned traffic. If it detects a deviation from learned traffic, then it marks the deviation as an event. The appliance sends these events to the Human Machine Interface (HMI) that you connected to the MetaDefender Industrial Firewall & IPS.

## [Supported PLC events](/docs/md-ot-security/v.2.2.6/operating/events#supported-plc-events)

This dashboard shows the traffic being monitored by the MetaDefender Industrial Firewall & IPS and information of each traffic.

## [Other events](/docs/md-ot-security/v.2.2.6/operating/events#other-events)

This dashboard shows the traffic not being monitored by the MetaDefender Industrial Firewall & IPS and information of each traffic.

## [Acknowledge Events](/docs/md-ot-security/v.2.2.6/operating/events#acknowledge-events)

When user click on Acknowledge button on each row, the detail of event is displayed.

User can input comment and Add event to traffic rule learned by check the checkbox then select Activity and click Acknowledge button.

The status of event will be changed to:

- **Acknowledged** if user do not check “Add event to traffic rule learned“.
- **Added traffic rules** if user check “Add event to traffic rule learned“ and select Activity.

User also can export the events by clicking Export button.
