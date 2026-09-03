<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/execution-profiles -->

# Execution Profiles

**Execution Profiles** allow users to control the file analysis process by selecting predefined or custom settings that influence how a file is scanned. Profiles define the depth of analysis, processing speed, and the level of detail in the generated report.

Pro Tip

Use **Speed Profile** for bulk scanning or in automated environments to process files faster.

## [Built-in Profiles](/docs/filescan/3.1.1/configuration/execution-profiles#built-in-profiles)

There are two built-in profiles available:

### [Analysis Profile](/docs/filescan/3.1.1/configuration/execution-profiles#analysis-profile)

Provides **in-depth** analysis by generating a very detailed report suitable for malware analysts. Executes all available analysis steps to provide the most comprehensive results, but usually takes longer to complete due to its thoroughness.

### [Speed Profile](/docs/filescan/3.1.1/configuration/execution-profiles#speed-profile)

Optimized for **fast execution** in automated environments, focuses on higher throughput, reducing the time needed for scans. Uses early termination: the scan stops immediately once a strong verdict (malicious or benign) is determined. This profile produces less detailed results compared to the Analysis Profile.

## [Custom Profiles](/docs/filescan/3.1.1/configuration/execution-profiles#custom-profiles)

Users can create custom profiles by defining their own analysis settings. This allows fine-tuning the scanning process to match specific requirements.

## [Profile settings](/docs/filescan/3.1.1/configuration/execution-profiles#profile-settings)

Info

These settings are **user-specific**: changes made by one user do not affect others.

### [Creating a Custom Profile](/docs/filescan/3.1.1/configuration/execution-profiles#creating-a-custom-profile)

Navigate to: **User -> My Settings -> Scan Profiles** and click the **Add profile** button

Chose a name and description for your new profile and select the desired features. Hover your mouse over the **information icons** next to each feature for more details. Optionally, select the profile as **Default** for all scans, and click the **Save** button.

### [Editing or removing a Profile](/docs/filescan/3.1.1/configuration/execution-profiles#editing-or-removing-a-profile)

Navigate to: **User -> My Settings -> Scan Profiles** and click the **Meatballs menu** next to the profile.

Info

Built in profiles cannot be removed and options are not editable, only the **Default** flag can be modified.

## [Scanning files with Profiles](/docs/filescan/3.1.1/configuration/execution-profiles#scanning-files-with-profiles)

Use the **File selector** on the main page and open the **Advanced Options** tab to select a profile and override the default profile selection for a new scan.

## [Scanning a file with custom settings](/docs/filescan/3.1.1/configuration/execution-profiles#scanning-a-file-with-custom-settings)

Use **Custom options** on the profile selector and select the desired options. This will be applied to the current scan, only.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
