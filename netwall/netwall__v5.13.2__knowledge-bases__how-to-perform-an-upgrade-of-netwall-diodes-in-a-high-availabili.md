<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/knowledge-bases/how-to-perform-an-upgrade-of-netwall-diodes-in-a-high-availabili -->

# How to Perform an Upgrade of Netwall Diodes in a High Availability (HA) Deployment?

This article applies to all Netwall Diode releases deployed.

Pro Tip:

Recommended to perform updates outside of business hours, during a scheduled maintenance period.

1. Perform a [snapshot/backup](https://www.opswat.com/docs/netwall/configuration/backups) of the machine.
2. Review current configurations, such as SMTP, FTP server, keep note on how they are setup. Also check connectors such as AVEVA PI for PI replication, Pi to Pi, and statistics. On the terminal run `show runningconfig` to take note for Red and Blue side.

Example:

3. Review system logs for any errors or issue indicators, if none please proceed to step 4.
4. Upgrade the secondary instances. Following the [Software Update](https://www.opswat.com/docs/netwall/configuration/software-update) guide, Upload > apply. Once done, reboot.
5. Check that all configurations [SMTP, FTP etc.] and connectors to ensure they are migrated successfully.
6. Monitor the system log while the instance is in primary to make sure there are no unexpected errors.
7. Demote the primary instances [making the newly upgraded secondary now the primary]. Perform the same steps as above on the new secondary.
8. Once both sets are complete, demote the primary to become the secondary pair if desired.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
