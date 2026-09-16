<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes -->

# YARA engine release notes

#### [v5.0.2](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v502)

Release date 9/17/2025

- **Bugfix:** File under “C:/Program” is deleted

#### [v5.0.1](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v501)

Release date 9/11/2025

- **Bugfix:** Fixed an issue with dependency check creating a file under "C:\Program"

#### [v5.0.0](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v500)

Release date 9/8/2025

- **Upgraded to YARA-X v1.5.0** The engine now uses the latest version of YARA-X, offering improved rule validation, stricter syntax enforcement, and enhanced performance.
- **Customizable Adaptive Sandbox Rules** You can now enable or disable specific rule groups within the Adaptive Sandbox Ruleset, allowing for more flexible and targeted threat detection.

- **UI Feedback for YARA Rule Errors** Any issues with uploaded YARA rules are now clearly indicated in the **Core UI**, making troubleshooting faster and more intuitive.

#### [v4.3.0](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v430)

Release date 4/9/2025

- Added Adaptive Sandbox curated rules to identify the most common attack vectors
- Improved application security

#### [v4.2.0](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v420)

Release date 12/1/2024

- Digitally sign all binary files.

#### [v4.1.0](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v410)

Release date: 10/8/2024

- Upgrade Yara to version 4.5.1

#### [v4.0.9](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v409)

Release date: 8/19/2024

- Upgrade YARA to version 4.3.1.
- Upgrade OpenSSL to version 3.1.3.
- Change the module name from "Yara" to "YARA".

#### [v4.0.8](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v408)

Release date: 10/24/2022

- Expose matched info in the scan result
- Support multiple hits

#### [v4.0.7](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v407)

Release date: 9/7/2022

- Support Debian 11

#### [v4.0.6](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v406)

Release date: 7/12/2022

- Fix memory leak issue

#### [v4.0.5](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v405)

Release date: 3/29/2021

- Upgrade Yara to 4.0.5

#### [v4.0.2](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v402)

Release date: 1/25/2021

- Upgrade Yara to 4.0.2

#### [v4.0.1](/docs/mdcore/v5.22.0/release-notes/yara-module-release-notes#v401)

Release date: 6/20/2020

- Upgrade Yara to 4.0.1
- A new method to load database
