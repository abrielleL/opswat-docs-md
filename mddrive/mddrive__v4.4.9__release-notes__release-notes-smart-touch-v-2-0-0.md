<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/release-notes/release-notes-smart-touch-v-2-0-0 -->

# MetaDefender Drive Smart Touch v2.0.0

|  |  |
| --- | --- |
| **Released on Jul 2, 2026** | This release includes new features and new user experiences |
| **New Features** | - **Enroll CM from Smart Touch** Enroll MetaDefender Drive in Central Management directly from Smart Touch, without having to boot the Drive on a PC. Once connected, enrollment is reflected across Smart Touch, Drive, and DTK, and settings and reports begin syncing with cloud or on-premises Central Management. For more details, refer to [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive with Smart Touch](/docs/mddrive/v4.4.9/configuration/enroll-cm-from-smart-touch) - **Show File Details In Secure File Storage** View detailed metadata for clean, unsafe, and unscanned files in Secure File Storage, helping users confirm file identity, understand its source, and make more informed decisions before taking action. For more details, refer to [MetaDefender Drive with Smart Touch Operations - Secure File Storage](/docs/mddrive/v4.4.9/process/smart-touch-secure-storage) |
| **Improvements** | - **Media Validation Agent now allows access to Secure File Storage** Use MetaDefender Drive with Media Validation Agent through the existing shared manifest validation setup, allowing files shared from the Drive to be accessed on protected endpoints. - **Activate Smart Touch with Drive Toolkit** Smart Touch now can be activated using Drive Toolkit |
| **Bug Fixes** | - **WiFi Management & Network Connectivity Improvements:** Enables operators to fully manage WiFi on SMC in air-gapped environments (forget networks, connect hidden SSIDs). Fixes false-negative WiFi status on SMC when external ping targets are unreachable in restricted networks. - Resolved an issue that caused Smart Touch license activation to loop indefinitely on first attempt. - Fixed an issue where Smart Touch constantly updates all engines |
|  |  |
