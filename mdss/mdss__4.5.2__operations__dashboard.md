<!-- source: https://www.opswat.com/docs/mdss/4.5.2/operations/dashboard -->

# Dashboard

The MetaDefender Storage Security dashboard is the page where you can see an overview of your storage and find information about file processing and usage statistics as well as details about currently running processes or upcoming ones.

![](https://uploads.developerhub.io/prod/k8zL/ieacim70ac6qcafh147umx1082nap168k3xbawqxk52dnp3pqktfg9vklglripqq.png)

#### Key Features at a Glance

- The dashboard begins with a dynamic activity feed, displaying the most recent scan results, file processing statuses, and any detected threats. This immediate visibility allows you to quickly assess the current state of your storage security.
- Quick access to essential configuration settings, user management, and other key sections of MetaDefender Storage Security is available through the navigation menu on the right. Customize your setup, manage users, and fine-tune your security policies directly from this central location.
- Gain a quick understanding of your system's performance with key statistics displayed prominently in the center. See the total number of files processed, detected threats, and other critical metrics at a glance.
- Dive deeper into file processing details with a breakdown of processed, sanitized, and blocked files. Understand the efficiency of your security measures and identify any potential bottlenecks.
- Monitor threat detection effectiveness with clear visualizations of potentially malicious files, permanently unavailable files, and possible threats.
- Track system performance over time with an interactive graph. Analyze file processing trends and identify any performance anomalies.
- Access in-depth analysis of individual files, including threat assessment results and remediation actions.  This granular view allows you to understand the specific threats detected and take appropriate action.

#### Why the Dashboard Matters

The MetaDefender Storage Security dashboard is designed to be your primary point of interaction with the system. It provides the essential information you need to:

- Stay informed about the real-time security status of your storage.
- Understand system efficiency and identify areas for optimization.
- Customize settings and policies to meet your specific security requirements.
- Quickly address detected threats and mitigate potential risks.

## Dashboard Counters

Previously, the MetaDefender Storage Security dashboard provided a consolidated view of compliance and security metrics, offering insights into potential violations and threats. While these metrics remain critical for understanding your security posture, they are now presented in more detail within their respective technology sections: Multiscanning, Content Disarm and Reconstruction (CDR), and Data Loss Prevention (DLP).

#### Key Compliance and Security Metrics (Now Found in Dedicated Sections)

These categories, though no longer directly visible on the main dashboard, are still essential for comprehensive security analysis and are now located within the dedicated sections for each technology:

- Compliance Violations (DLP Section):
  - PCI-DSS (Payment Card Industry Data Security Standard): Tracks files containing Credit Card Numbers (CCN).
  - HIPAA (Health Insurance Portability and Accountability Act): Identifies files containing protected health information (e.g., full name, address, date of birth, phone number, email, SSN, bank account, passport).
  - GDPR (General Data Protection Regulation): Monitors files with personally identifiable information (PII) as defined by GDPR (e.g., full name, address, date of birth, phone number, email, bank account, passport).
- Security Alerts (Multiscanning and Vulnerability Assessment Sections):
  - Malware: Displays the number of potentially dangerous files detected by our multi-scanning technology.
  - Vulnerabilities: Shows the number of files with known vulnerabilities identified by our File-Based Vulnerability Assessment engine.
- PII Data (DLP Section) tracks files containing personally identifiable information (e.g., full name, bank account, passport, email, SSN).

Why These Metrics Still Matter

- Demonstrating adherence to industry regulations.
- Identifying potential malware and vulnerabilities.
- Protecting sensitive information from unauthorized access.

Where to Find These Metrics Now:

For detailed information on these metrics, please click on each dedicated sections for: Multiscanning, CDR and DLP.

> **Info**
>
> Please check the [MetaDefender Core sample regular expression page](https://docs.opswat.com/mdcore/proactive-dlp/sample-regular-expressions) for a list of rules that are being used to match full names, US addresses, birth dates, etc.

> **Info**
>
> The small arrows below each category shows you a percentage increase or decrease based on the previous scan.

## Processing Overview

You can select to view data for the last week, month or even the last year. The height of the bar represents the volume of files processed by MetaDefender Storage Security. Hover over it to see more details:

![](https://uploads.developerhub.io/prod/k8zL/ieacim70ac6qcafh147umx1082nap168k3xbawqxk52dnp3pqktfg9vklglripqq.png)

The processed quantity field represents the total amount of data processed with MetaDefender Storage Security. This quantity will exceed your actual storage data if you have triggered more than one process in the defined time unit (day or month). That is because every time you process a file this quantity will be increased even if you’ve processed the same file multiple times.

The number of suspicious files, as well as the counters on the top of the page, represent unique files. If the hash of the file has not changed, MetaDefender Storage Security will only count it once.

## Active jobs

The dashboard displays an overview of all active jobs. To see them in detail, click **View Running Jobs**.

![](https://uploads.developerhub.io/prod/k8zL/04nggmjdssf67aahh226bskq97ke9s5xmnh2ophduy8ivxz6w67f0jxjjysb4qu6.png)

By clicking on **View Running Jobs**, you will be redirected to a page that contains the following information:

![](https://uploads.developerhub.io/prod/k8zL/hf70yfocienm12eiss70jxrhjtertylgkrltzr0u7mk9453gyeh2iyjtuar7xhnq.png)

## Ongoing Jobs details

When clicking on the job you will be redirected to the ongoing job page:

![](https://uploads.developerhub.io/prod/k8zL/v5ynmdy75x71fcvxe0xnu5udtuhh71j2ark3rpnujni8c8xdj0e3zllzppjp9x1q.png)

Here you can find the information we previously mentioned as well as the time elapsed since this job was started. Click back if you want to go back to the dashboard.

## Real time processing and upcoming processes

On the dashboard page, if you scroll down, you will find more information about real time processing and upcoming scheduled processes. This area, like the whole page, is updated in real time so you can always know what’s happening.

![](https://uploads.developerhub.io/prod/k8zL/lbc5z5q7mj4uzqvu16s2rdsdmh51oho4xb1bzpl0yps361vh2yvxf24xoq9fe767.png)

> **Info**
>
> Real time processing requires a lot of internal communication. This could impact the performance of other scans

> **Warning**
>
> Starting real time processing and other type of scans in parallel with remediations that modify the files in storage could trigger a loop scanning.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
