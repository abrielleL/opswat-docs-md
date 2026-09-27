<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/troubleshooting/troubleshooting-guide-for-cybereason-activeprobe-issues -->

# Troubleshooting Guide for Cybereason ActiveProbe Issues

This document aims to help users troubleshoot Cybereason ActiveProbe issues on macOS.

## Issues

### Real-time protection is not enabled

![](https://uploads.developerhub.io/prod/2x2P/yatjbypbygspenh1tzixcmlf096uloyzumehhi912f7fciyxypixcweqw63jqjnu.png)

### No successful scan recently

![](https://uploads.developerhub.io/prod/2x2P/ais5hog5qfofig1scl7wvw65fdwhce85qsztrx0csum3orrkva76002w83nzxw0f.png)

This guide provides quick checks that users can perform directly on the endpoint. The results help:

- You confirm the current Cybereason status on the device.
- Our team determine whether the MetaDefender Endpoint support package logs may have rotated when the issue happened.

## Troubleshooting Guide

### Real-time protection is not enabled

To troubleshoot this issue from the endpoint, please verify the following to ensure MetaDefender Endpoint can retrieve the correct status from Cybereason:

- **Confirm Cybereason real-time protection processes are running**
  - Open **Activity Monitor** on the Mac
  - In the search box, type `cybereason`
  - Verify that the main Cybereason processes are present and running. If they are not running, please restart the Cybereason service or reboot the device, then check again.

![](https://uploads.developerhub.io/prod/2x2P/kuevlte3efbwkoeujd03yp58tnmztfqqyc2c6r9i1xhsj5pl8lral3o2td391h9g.png)

- **Verify the device has network connectivity**
  - Open Terminal.
  - Run the following command: `ping google.com`
  - Confirm that you see replies (not “host unreachable” or timeouts). If there is no network connectivity, please resolve the network issue and then recheck the real-time protection status in MetaDefender Endpoint.
- **Verify the Cybereason configuration flag**
  - On the endpoint, open the file: `/usr/local/cybereason/config.plist`
  - Locate the setting: `am.toggerValue`
  - Confirm that: `am.toggerValue = 1`

![](https://uploads.developerhub.io/prod/2x2P/w4266fscbypl1qausf0wtnsa21lrgjifzglh725m3w6mym7umciqxr241d21129d.png)

## No successful scan recently

MetaDefender Endpoint reads the last full scan information from the following file on the endpoint:`/usr/local/cybereason/av_status.json`

Follow the steps below:

- Check the `lastFullScan` field
  - Open the file:  `/usr/local/cybereason/av_status.json`
  - Interpret the value:
    - If `lastFullScan` contains a **valid date/time**, that is the last full scan Cybereason reports to MDE.
    - If `lastFullScan` is **empty or missing**, Cybereason has no record of a completed full scan on this device.

![](https://uploads.developerhub.io/prod/2x2P/z8fwrase6cdhjekxq9fgp2oj16dstzmcxq88fdlnpcirgfv5h8vuj89fdg9cfk4t.png)

- Trigger a new full scan if lastFullScan is empty or missing:
  - Start a **full scan** from the Cybereason Dashboard on the endpoint (Contact Cybereason Admin).
  - Wait for the full scan to complete.
  - After completion, verify that `lastFullScan` in `av_status.json` is now populated.
  - Click “Recheck” on the MetaDefender Endpoint tray icon and confirm the “Last successful scan” updates.

> **Info**
>
> According to the vendor, the `lastFullScan` field is **reset every time Cybereason ActiveProbe is upgraded to a newer version**. This means:
>
> - After an upgrade, `lastFullScan` may appear empty or show an older value.
> - A new full scan must be run after each upgrade to repopulate this field and allow MDE to show an up-to-date “Last successful scan” status.

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
