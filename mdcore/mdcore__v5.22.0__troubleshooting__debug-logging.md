<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/debug-logging -->

# Debug logging

Enabling debug logging level on MetaDefender Core should only be used when absolutely necessary, and advised by the OPSWAT team.

Letting MeteDefender Core operate for a long time under debug logging mode will likely cause performance degradation, out of disk space, and possibly an IO bottleneck issue on the system.

**Tips:** We should only enable the debug logging level when:

- We already know the steps to reproduce or trigger the issue symptom.
- Or, we already know the issue will very likely come back very soon.
- Or, the OPSWAT team checked and confirmed there should be more useful information tracked with the debug log and relevant to the issue.

1. To provide debug logs for the OPSWAT support team, the level of the logfile for the given service ometascan must be set to `debug` (see how at [How to enable debug logging for MetaDefender Core](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-enable-debug-logging-for-metadefender-core-)).
2. Execute the scenarios requested by the support team
3. Collect the generated log files by following the steps at

   - [**How to Create Support Package With Web Console**](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-with-web-console)
   - [**How to Create Support Package With Bundle Tools**](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-)
4. **After collecting the debug logs, the log level should be set back to** `info`**, as the size of the logfile will increase significantly in debug mode.**

For information on how to interpret the log files, consult: [Log Message Format](https://www.opswat.com/docs/mdcore/configuration/log-message-format)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
