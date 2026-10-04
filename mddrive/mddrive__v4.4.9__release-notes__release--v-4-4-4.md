<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/release-notes/release--v-4-4-4 -->

# MetaDefender Drive v4.4.4

|  |  |
| --- | --- |
| **Released on Apr 24, 2026** | This release includes new features and issue fixes |
| **New Features** | - **Recommend Engine based on Hardware:** MetaDefender Drive now automatically recommends the optimal scan configuration based on the machine’s hardware resources, fully replacing the legacy Lite Mode with a smarter, hardware‑aware experience. - **Extend NTFS partition from 12G to 64GB:** For Drive 2, Digital Display, and Smart Touch (not supported on 64GB Drive), reflashing to the latest version using DTK expands reporting and engine update space from 12GB to 64GB, enabling storage of more reports and In-Session engines |
| **Improvements** |  |
|  | - **Improved stability:** by prioritizing the UI so it remains responsive during CPU-intensive scans - **Improved In-Session UX and Stability:**    - Making it more friendly especially when a previous session is running.   - Showing splash while In-Session is loading   - Reducing mis-scans and support overhead by making the chosen scan path immediately visible during in-session scanning.   - Enables quick identification of the physical Drive via its serial number and faster lookup of its related reports in CM. |
| **Bug fixed** |  |
|  | - Drive can't connect to OCM with HTTPS enabled using self-signed certificate chain - AV engines sometimes not showing on Drive - Report Sync hang with spinner forever - Scan Error message not reflected in scan report |
