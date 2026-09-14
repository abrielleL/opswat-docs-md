<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-did-the-deployment-of-the-threat-intelligence-module-fail- -->

# Why did the deployment of the Threat Intelligence Module Fail?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

One common reason for this failure is the absence of the required Microsoft Visual C++ Redistributable for Visual Studio 2015-2022 (version 14.38 or higher) on the system.

## [Resolution:](/docs/mdcore/knowledge-base/why-did-the-deployment-of-the-threat-intelligence-module-fail-#resolution)

1. Verify Installation: Ensure that the Microsoft Visual C++ Redistributable for Visual Studio 2015-2022 (version 14.38 or higher) is installed on your machine.
2. Download and Install: If the required redistributable is missing, download and install the x64 version from the following link: [Microsoft Visual C++ Redistributable Download](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
3. Disable/Enable: Retry deploying the Threat Intelligence Module and verify if the issue is resolved.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
