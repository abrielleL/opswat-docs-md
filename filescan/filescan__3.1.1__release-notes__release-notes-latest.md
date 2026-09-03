<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-latest -->

# Release Notes for v3.1.1

### Date: 27th May 2026

Warning

**Upgrading directly** from versions prior to 2.5.1 to 3.1.1 is **not possible!**

**Recommended Upgrade Path:** First upgrade to **2.5.1**, then install **3.1.1**.

## MetaDefender Aether™ v3.1.1 (including MetaDefender Sandbox™ capabilities)

MetaDefender Aether v3.1.1 provides database package updates via proxy and several minor enhancements.

### What’s New

- **Database Package Updates via Proxy -** Database packages can also be downloaded if the system connects to the Internet via a proxy server: [Database package updates](/adminguide/database-package-updates)

### Improvements

- **Suppressed AV Misdetections for Demo Report -** The release artifact contained a demo report in JSON format that was incorrectly detected by some AV engines. This report has been encoded to suppress these misdetections.

### Bug Fixes

- **Fixed CEF Syslog Summary -** The broker component could not generate the CEF Syslog summary due to a data conversion issue.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
