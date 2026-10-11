<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/advanced-search -->

# Threat Hunting

View as Markdown Ask ChatGPT about this page Ask Claude about this page

A more comprehensive search is accessible by clicking on the **Hunting** button on the menu:

Warning

Please note that a login is required to access the detailed search.

In this document, we showcase some of the diverse threat hunting capabilities available in the [advanced search](https://www.filescan.io/advanced-search) feature.

With the advanced search option, you have access to numerous fields for refining your search, including verdict, file type, hashes, YARA rules, and more.

When you click on the search button, it retrieves the reports that match your search criteria. Please note that the maximum available date interval for retrieval is three months.

## [Examples](/docs/filescan/3.2.0/datasheet/advanced-search#examples)

*Note: Since the search can take time, opening the serach examples also takes time too.*

### [Malicious Documents](/docs/filescan/3.2.0/datasheet/advanced-search#malicious-documents)

Office Files with Foreign Language and Active Content: [report example](https://www.filescan.io/uploads/63d8695196add6d1cf4945a3/reports/e9ce37c2-2e3c-42b0-97b5-60915491b87b/overview), [search example](https://www.filescan.io/search-result?filetype=ms-office&verdict=malicious&tag=macros-on-open&unique_files=false&method=and&signal_groups=TXT000)

Office Files using default Symmetric Key Encryption: [report example](https://www.filescan.io/uploads/636c2d9d82dd9f2e26533a63/reports/3739cc91-230c-48aa-9f34-f66d01e0cc53/overview), [search example](https://www.filescan.io/search-result?filetype=ms-office&verdict=malicious&tag=velvetsweatshop&unique_files=false&method=and)

Office Files utilizing the EMBED.Equation exploit: [report example](https://www.filescan.io/uploads/63d869511c9cbf7d6254b2d2/reports/d4c8816b-4604-40f8-a37e-8d772a7311d9/overview), [search example](https://www.filescan.io/search-result?filetype=ms-office&verdict=malicious&unique_files=false&method=and&signal_groups=EMU005)

Office Files with Auto-Execution and Process Spawns: [report example](https://www.filescan.io/uploads/63d8c7f61c9cbf7d6254d3e2/reports/9a7dad6d-ca7d-4362-a188-49fa8e34533d/overview), [search example](https://www.filescan.io/search-result?filetype=ms-office&verdict=malicious&tag=macros-on-open&unique_files=false&method=and&signal_groups=EMU006)

Phishing PDFs: [report example](https://www.filescan.io/uploads/638bf26704e0e79bdf40af36/reports/13134165-1f5d-4d8e-953b-556e6526cd43/overview), [search example](https://www.filescan.io/search-result?verdict=malicious&tag=phishing&rate_from=5&unique_files=false&method=and&signal_groups=PDF000)

### [Suspicious Executables](/docs/filescan/3.2.0/datasheet/advanced-search#suspicious-executables)

Packed PE files with process hollowing capabilities: [report example](https://www.filescan.io/uploads/63d698020d26fb7d57b32662/reports/6d249d09-96e2-47cc-b04c-bb281b83996e/overview), [search example](https://www.filescan.io/search-result?filetype=exe&verdict=malicious&tag=packed&unique_files=false&method=and&signal_groups=SIG006)

PE file with a RDTSC timing instruction: [report example](https://www.filescan.io/uploads/63d9003b2d4f6d560e23d661/reports/fa0cab2c-fbe9-44d1-9fee-76418d734688/overview), [search example](https://www.filescan.io/search-result?filetype=exe&verdict=malicious&unique_files=false&method=and&signal_groups=DS002)

### [Unusual File Types](/docs/filescan/3.2.0/datasheet/advanced-search#unusual-file-types)

Malicious Windows Shortcut Files spawning rundll: [report example](https://www.filescan.io/uploads/63d8696e1c9cbf7d6254b3cf/reports/6075dc42-e8a9-4dad-920c-78b698ce6c18/overview), [search example](https://www.filescan.io/search-result?filetype=lnk&verdict=malicious&tag=rundll32&unique_files=false&method=and)

Malicious files delivered via VHD image files: [report example](https://www.filescan.io/uploads/638a13c6eed772f2afbff862/reports/8d0a231d-c508-4192-894d-14e131904293/overview), [search example](https://www.filescan.io/search-result?verdict=malicious&tag=vhd&unique_files=false&method=and)

### [Mobile Threats](/docs/filescan/3.2.0/datasheet/advanced-search#mobile-threats)

Malicious APKs: [report example](https://www.filescan.io/uploads/63c901c4db7e620ca7326d02/reports/9789aa14-2fff-4358-9f85-2244026e2538/overview), [search example](https://www.filescan.io/search-result?filetype=apk&verdict=malicious&rate_from=5&unique_files=false&method=and&signal_groups=A001)

APKs reading the device ID (IMEI): [report example](https://www.filescan.io/uploads/63a6ff7740a5b95bba45acf5/reports/39434c5d-7774-4020-92dd-f21ffdf44224/overview), [search example](https://www.filescan.io/search-result?filetype=apk&verdict=malicious&rate_from=5&unique_files=false&method=and&signal_groups=DC001)

### [Malicious Web Threats](/docs/filescan/3.2.0/datasheet/advanced-search#malicious-web-threats)

E-Mails containing macro-enabled attachments: [report example](https://www.filescan.io/uploads/63d65bf11c9cbf7d62541fc2/reports/863e4abb-f438-40fa-826c-fac51e348b19/overview), [search example](https://www.filescan.io/search-result?filetype=mail&verdict=malicious&tag=macros&unique_files=false&method=and)

Phishing URLs: [report example](https://www.filescan.io/uploads/63d87ad489bd67c10fdbb5d2/reports/4ee9c6e6-ca0e-4058-83d6-f999fe90704e/overview), [search example](https://www.filescan.io/search-result?source_type=url&verdict=malicious&tag=phishing&unique_files=false&method=and)

### [Additional Resources](/docs/filescan/3.2.0/datasheet/advanced-search#additional-resources)

[Personal Threats Overview Page](https://www.filescan.io/threats-overview)

[CLI for API (pip package)](https://github.com/filescanio/fsio-cli)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
