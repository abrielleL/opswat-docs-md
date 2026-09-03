<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-can-i-not-execute-script-file-like--vbs-or--ps1-----in-harde -->

# Why can I not execute script file like .VBS or .PS1.... in Hardened Image

This article applies to all MD Kiosk Hardened Image versions

One of the security features of the Kiosk Hardened Image is the restriction of executable file types such as `.bat`, `.ps1`, `.vbs`, `.reg`, and others, which can run potentially harmful commands on the system. This helps prevent unauthorized execution and enhances protection of the Kiosk system at the backend.

**How to resolve this situation**:

To execute these file types on the Hardened Kiosk Image, you must manually open Command Prompt or PowerShell with administrator privileges, then run the file directly from the console.

For example:

Warning

There will be another restriction on other services like .vbs,… In those cases, please contact Support for further instructions.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/portal/support).
