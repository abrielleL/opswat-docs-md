<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk- -->

# How to Collect Logs and Open a Support Case for the OESIS Framework?

This article is applied to all **MetaDefender Endpoint Security SDK** releases on **Windows, MacOS and Linux**.

This article explains the correct process for opening a support case for **MetaDefender Endpoint Security SDK (MDESDK)** and how to collect the necessary logs. Supplying this information at the start of your case helps the OPSWAT Support team investigate and resolve issues more quickly.

## [Information to Include in Your Support Case](/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk-#information-to-include-in-your-support-case)

To help us investigate your issue effectively, please include the following details in your support ticket:

**Required information:**

1. 🧩 **Product Name & Version** *e.g., Google Chrome 141.0, Mozilla Firefox ESR 142.0, ESET Endpoint Security 12.0.2062.0*
2. 💻 **OS Details** *e.g., Windows 11 en-US , macOS Tahoe 26 Dutch*
3. ⚙️ **SDK Version and Architecture** *e.g., SDK 4.3.5028.0 x64, SDK 4.3.4463.0 ARM64*
4. 📘 **Type of Support Needed** *(for new products or new versions)*

   - Detection (compliance and remediation)
   - Patching
   - Vulnerability detection
5. 📝 **Issue Details**

   - Clear description of the issue
   - Steps to reproduce
   - How many devices are impacted
   - Expected behavior vs. actual behavior

**To speed up troubleshooting, please also provide:**

1. **📦 Product Installer File:** If available, please provide the installer and a **temporary license** (some product functions may be restricted without a proper license).
2. 🖼️ **Screenshots evidence** A few screenshots would help in these cases:

   - Product UI value differs from SDK returned value.
   - Application not shown in Control Panel although SDK reports “successful install”.
3. 🔑 **Process privilege** Let us know whether you are invoking SDK with a **non-admin** or **admin** user.
4. 🔧 **Is the process belong to a service?** If you are calling SDK as a sub-process of your service, please also let us know.

## [Collecting Debug Logs (Mandatory for Most Issues)](/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk-#collecting-debug-logs-mandatory-for-most-issues)

To investigate issues, OPSWAT Support requires **v4Debug logs**. Please follow the below steps to collect them:

Note:

The SDK process must have **write permission** to the log folder (by default, the SDK installation directory). Without sufficient permission, the SDK **cannot generate log files**.

1. Retrieve **v4Debug.dat** file from the **SDK engine package** under the `config` directory.

   - Or you can create it manually:

     - Create a blank text file.
     - Rename it to **v4Debug.dat**.
2. Place **v4Debug.dat** file in the same folder as the **SDK libraries** (libwa* files).
3. Run the SDK, debug logs will be collected automatically.
4. Reproduce the issue so it is recorded in the logs.
5. Look for generated log files in this format:

v4DebugInfo_XYZ_....log
wahost_log_<timestamp>.log (on MacOS)Note:

*wahost log will only generate when* `wahost` feature is enabled

6. Collect all generated log files.
7. Compress the logs into a **.zip** file and attach them to your support case.

Note:

If you want to change the generated log folder or other configurations, please refer to this detailed article: [**How do I configure v4Debug.dat for enhanced logging? - MetaDefender Endpoint Security SDK**](https://www.opswat.com/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging)

## [If You Experience a Crash](/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk-#if-you-experience-a-crash)

Please provide the following to expedite the troubleshoot process:

- A full **user-mode crash dump** ([DumpType=2](https://learn.microsoft.com/en-us/windows/win32/wer/collecting-user-mode-dumps#:~:text=10-,DumpType,-Specify%20one%20of)) .dmp file.
- Corresponding **v4Debug logs** collected during the crash.
- Steps performed before the crash (how to reproduce it).
- Detailed about SDK information used.
- Whether the issue occurs in other SDK versions (older/newer).
- Frequency of the issue (every time, sometimes, rarely).
- How many devices are affected by the crash.

## [If You Cannot Provide Logs](/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk-#if-you-cannot-provide-logs)

If logs are not available, please give as many details as possible, including:

- Exact error or issue observed.
- Steps to reproduce the problem.
- Environment details (OS, SDK version, etc…)

## [Summary](/docs/mdsdk/knowledge-base/how-to-collect-logs-and-open-a-support-case-for-mdesdk-#summary)

For faster issue resolution, please always provide the following information:

- Product name, version, installer, and a clear issue description.
- The most detailed possible explanation of the observed behavior and the expected behavior.
- Collect and attach debug logs (using `v4Debug.dat` or `WaDiagnose.exe`).
- For crashes, provide crash dumps along with reproduction steps.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
