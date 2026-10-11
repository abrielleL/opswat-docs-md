<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-md-core-is-not-reachable- -->

# Why MD Core is Not Reachable?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Issue Summary:** MetaDefender Core may become unreachable due to nginx failing to start properly after a restart or shutdown.

**Error Logs:** In nginx_error.log, you may see the following entry:

*[error] 10904#14248: OpenEvent("Global\ngx_reopen_3536") failed (2: The system cannot find the file specified)*

**Root Cause:** This issue occurs when nginx fails to clean up its temporary files during a shutdown or restart. On subsequent startups, these leftover files can interfere with nginx’s ability to launch, preventing MD Core from becoming reachable.

**Remediation Steps:**

1. **Stop the Service:**

- Open Services (services.msc) and stop **OPSWAT MetaDefender Core**.

2. **Clean Up Temporary Files:**

- Navigate to: C:\Windows\Temp\ometascan
- Delete all files inside this directory. Files you may find include:
- ometascan-nginx.pid
- nginx.conf
- Other temporary files

3. **Restart the Service:**

- Start the **OPSWAT MetaDefender Core** service again.

**Additional Notes:**

- Ensure you have administrator privileges to delete the files.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
