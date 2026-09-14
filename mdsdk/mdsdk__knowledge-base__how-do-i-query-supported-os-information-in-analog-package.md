<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-do-i-query-supported-os-information-in-analog-package -->

# How do I query supported OS information in Analog package?

In November 2024, the MDES SDK will introduce a new JSON file in the Analog package, named `os_info.json`. This new file allows users to map OS attributes (such as OS ID) from other Server files, enabling the visualization of OS family, OS name, OS version, and more for enhanced display within the Server component of their product. The JSON schema is outlined below:

JsonCopy{
"win": [
{
"os_family": "Windows 11", // Name of the Windows family
"list": [ // List of Windows editions
{
"os_name": "Windows 11 Enterprise", // Name of the Windows edition
"os_id": 81, // ID of the Windows edition
"versions": [ // List of Windows edition versions
{
"release_label": "11-23h2-e" // Release version of the Windows edition
},
...
]
},
...
]
},
...
],
"mac": [
{
"os_family": "macOS", // Name of the macOS family
"list": [ // List of macOS editions
{
"os_name": "macOS Sonoma", // Name of the macOS edition
"os_id": 1400 // ID of the macOS edition
},
...
]
},
...
],
"linux": [
{
"os_family": "Debian-based", // Name of the Linux family
"list": [ // List of Linux flavors
{
"os_name": "Ubuntu", // Name of the Linux flavor
"os_id": 4, // ID of the Linux flavor
"versions": [ // List of Linux flavor versions
{
"release_label": "24.04" // Release version of the Linux flavor
},
...
]
}
]
}
]
}

You can access the `os_info.json` file by downloading the Analog package and then navigating to the following directory: `analog/server/os_info.json`.
