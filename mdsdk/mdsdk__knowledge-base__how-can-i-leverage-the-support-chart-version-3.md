<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3 -->

# How Can I Leverage The Support Chart Version 3?

**Disclaimer:** The Support Chart version 3 is currently in Beta. Expect potential changes or improvements in future versions.

## [Background](/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3#background)

Support Chart version 2 has been effective in capturing and managing details of supported methods across various support applications within the SDK. However, we identified some challenges with how the legend was structured, making it difficult to extract specific functions or capabilities of methods and to seamlessly incorporate newly supported functions as they become available.

To address these limitations, we are introducing Support Chart version 3, which features an improved legend and a refined approach to interpreting method statuses. This new version is designed to provide a clearer, more detailed understanding of method statuses, making it easier to explore status details in depth.

Furthermore, Support Chart version 3 introduces new status definitions for the Real-time Monitoring feature, enabling customers to track compliance data in real-time.

New Changes

There are two updates in the Legend compared to Support Chart version 2:

1. **Removal of the VA value:** The previously used **VA** value, which indicated "Implemented, requires admin", has been replaced by two separate values: **V** for "Implemented" and **A** for "Requires Admin."
2. **Removal of the X value:** The previously used **X** value, which indicated “Not Implemented/Not Tested“, will no longer be used.
3. **Introduction of the U qualifier:** A new **U** value has been introduced to indicate “Not Tested“, helping customers identify methods that are generally supported but have not been tested with specific product versions.
4. **Introduction of the T qualifier:** A new **T** value has been added to indicate "Real-time monitoring supported," helping customers identify which methods support real-time monitoring.
5. **Introduction of the B qualifier:** A new **B** value has been added to indicate that the API connection to the application appears broken and is actively being fixed.

## [Usage](/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3#usage)

### [1. Understanding the Legend Definitions](/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3#1-understanding-the-legend-definitions)

The legend includes two Status Indicators and a number of Status Qualifiers:

- Status Indicators

  - **V**: Implemented
  - **O**: Not Supported
- Status Qualifiers:

  - **A**: Requires Admin
  - **U:** Not Tested
  - **Z**: Implemented on Windows with Security Center (WMI) available
  - **T**: Real-time Monitoring Supported
  - **B**: One or more broken APIs

### [2. Determining the Support Value for Applications and Methods](/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3#2-determining-the-support-value-for-applications-and-methods)

Each application and method's support level is represented as a string that consists of relevant status indicators.

- Example: if the **GetRealTimeProtectionState** method in **ESET Endpoint Antivirus 7.0** is both implemented and supports real-time monitoring, its support value would be **VT**, where:

  - **V**: Implemented
  - **T**: Real-time Monitoring Supported
- Example: if the **GetRealTimeProtectionState** method in **ESET Endpoint Antivirus 7.1** is both implemented, and supports real-time monitoring, but has not been tested yet, its support value would be **VTB**, where:

  - **V**: Implemented
  - **T**: Real-time Monitoring Supported
  - **U**: Untested

### [3. Extracting and Interpreting Support Values](/docs/mdsdk/knowledge-base/how-can-i-leverage-the-support-chart-version-3#3-extracting-and-interpreting-support-values)

To utilize these values effectively, users should extract the individual status indicators from the string and compare them to the legend. This allows them to:

1. Understand the capability of each method.
2. Execute the method with the appropriate permissions and features.

By following this approach, users can ensure proper configuration and functionality of the application and method within the system.
