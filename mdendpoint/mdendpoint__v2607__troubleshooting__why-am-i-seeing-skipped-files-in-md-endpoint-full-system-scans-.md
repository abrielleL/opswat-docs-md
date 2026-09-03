<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/why-am-i-seeing-skipped-files-in-md-endpoint-full-system-scans- -->

# Why am I seeing skipped files in MD Endpoint full system scans?

There are some cases where MD Endpoint scan session cannot access the content of a file, even with administrator privileges.

The root causes are typically because the file is blocked from being used by other processes, or attempting to read it may cause issues for the operating system.

For example:

- OS system files: system libraries, drivers, configuration files, log files, and executable files necessary for the OS to function properly.
- Application data files: files storing user info, settings, history, passwords, or other data are locked by applications.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
