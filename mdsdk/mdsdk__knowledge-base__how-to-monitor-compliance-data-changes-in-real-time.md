<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time -->

# How to Monitor Compliance Data Changes in Real-Time?

**Disclaimer:** The Real-time Monitoring is currently in Beta. Expect potential changes or improvements in future versions.

## [Background](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#background)

We recognize that traditional periodic compliance checks may pose challenges in ensuring timely adherence across all endpoints. To address this, the Real-time Monitoring feature has been introduced as an alternative to scheduled checks. This feature enables proactive tracking and instant detection of changes at endpoints without relying on periodic scans.

## [Goal](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#goal)

- Implement a proactive mechanism for detecting and capturing compliance data changes in real-time.
- Ensure continuous compliance and security of all endpoints.
- Instantly access reliable security information from devices without the need for repeated scans.
- Minimize the time gaps between periodic checks, reducing potential vulnerabilities that attackers could exploit.

## [Scope](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#scope)

Real-time Monitoring currently supports the Windows and macOS environments with specific methods and applications that are listed in the Support Chart version 3. For more details, you can access [this documentation](https://www.opswat.com/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3).

## [Usage](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#usage)

### [1. Verify Real-Time Monitoring Support for a Method](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#1-verify-real-time-monitoring-support-for-a-method)

Before proceeding, confirm whether a specific method supports Real-Time Monitoring by referring to Support Chart version 3. For details on how to use Support Chart version 3, please see [How Can I Leverage The Support Chart Version 3](https://www.opswat.com/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3).

For example, when reviewing Support Chart version 3 for ANTIMALWARE products, you may find that Windows Defender (Signature ID: 477) supports Real-Time Monitoring through the GetRealTimeProtectionState method (Method ID: 1000).

### [2. Enable Real-Time Monitoring](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#2-enable-real-time-monitoring)

To activate the Real-Time Monitoring feature, register for tracking real-time changes in a specific method's state using wa_api_register_handler, with event_type set to 10. The following code snippet demonstrates how to monitor the GetRealTimeProtectionState method of Windows Defender in real-time.

CppCopy#include <iostream>
#include <string>
// Callback function to handle method state change events
void OnRTMEventReceived(wa_wchar* json_event)
{
std::wcout << L"[Callback] GetRealTimeProtectionState state change event received: " << json_event << std::endl;
// TODO: Parse and process the json_event string as needed
// Example of json_event content:
// {
// "result": {
// "code": 0,
// "details": {
// "antispyware": false,
// "antivirus": false
// },
// "enabled": false,
// "method": 1000,
// "signature": 477,
// "timestamp": "1742553608",
// "timing": 7718
// }
// }
// Important: You own the memory of json_event, so free it after use
wa_api_free(json_event);
}
int main()
{
// Step 0: Setup SDK (via wa_api_setup)
// ...
// Step 1: Define handler configuration
std::wstring json_in = LR"JSON(
{
"event_type": 10,
"config": {
"signature": 477,
"method": 1000
}
}
)JSON";
// Step 2: Register handler
wa_int handlerId = 0;
auto returnCode = wa_api_register_handler(json_in.c_str(), OnRTMEventReceived, handlerId);
if (WAAPI_SUCCESS(rc))
{
std::wcout << L"Handler registered successfully. Handler ID: " << handlerId << std::endl;
}
else
{
std::wcout << L"Failed to register handler. Error code: " << returnCode << std::endl;
return 1;
}
// ... other application logic ...
// When application about to end: Deinitilized SDK by call wa_api_teardown
// ...
return 0;
}
### [3. Unregister When No Longer Needed](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#3-unregister-when-no-longer-needed)

To stop monitoring the method, call:

CppCopywa_api_unregister_handler(handler_id);
## [Known Issues](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#known-issues)

### [Potential Delay in Real-Time Monitoring](/docs/mdsdk/knowledge-base/how-to-monitor-compliance-data-changes-in-real-time#potential-delay-in-real-time-monitoring)

Real-time Monitoring is designed to support a wide range of applications, each with its own mechanism for returning status updates. As a result, you may experience a delay of up to **3 seconds** when implementing real-time monitoring for supported application methods.
