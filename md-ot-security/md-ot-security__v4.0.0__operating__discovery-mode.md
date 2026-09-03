<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/operating/discovery-mode -->

# Discovery Mode

Discovery mode is the mode in which MetaDefender OT Security will learn about your system.

It is the default mode when you first start the MetaDefender OT Security application.

Time in discovery mode will be essential for MetaDefender OT Security to be able to better understand the system, give certain standards to evaluate which are the trusted assets, what are daily activities in the system.

Which activities is suspicious, what are the risks that need to be prevented.

When in this mode:

- No violation of allowlist will be triggered.
- The time that the trusted asset was in an inactive state will be learned and updated in the asset policies.
- Existing connections between assets will be learned and added to the connection policies.
- Open ports and protocols on that port will also be learned and added to the asset policies.

It is very important when in Discovery mode that your system is in a normal state. In addition to our predefined values based on industry standards, the knowledge learned by MetaDefender OT Security is an indispensable piece for us to protect your system in the best way. So MetaDefender OT Security may need at least one day to learn your network.

You can always view and adjust what MetaDefender OT Security learns on the asset policy, connection policy, asset details.
