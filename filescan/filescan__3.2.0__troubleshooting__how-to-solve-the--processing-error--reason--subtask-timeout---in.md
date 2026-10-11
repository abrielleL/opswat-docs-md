<!-- source: https://www.opswat.com/docs/filescan/3.2.0/troubleshooting/how-to-solve-the--processing-error--reason--subtask-timeout---in -->

# How to solve the "Processing error (reason: subtask_timeout)" in MetaDefender Sandbox?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Issue**: Customers may encounter the following error during file analysis in MetaDefender Sandbox:

*Processing error (reason: subtask_timeout)*

Root Cause: This error typically occurs when the Sandbox's timeout settings are too low to accommodate the full execution of analysis tasks. Specifically, the REPORT_INTERRUPT_TIMEOUT parameter is set too short, causing the system to interrupt the report generation prematurely.

**Resolution**:

To fix this issue increase the value of the REPORT_INTERRUPT_TIMEOUT parameter. This change allows the Sandbox more time to complete its processing tasks before timing out.

Please see additional details about these parameters in the link below:

<https://www.opswat.com/docs/filescan/configuration/jobs>

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
