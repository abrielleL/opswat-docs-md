<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/is-the-scheduled-scan-in-metadefender-storage-security-based-on- -->

# Is the Scheduled Scan in MetaDefender Storage Security Based on OS Time or an Internal Timer?

> **Check Your Version:**
>
> This article is applied to MetaDefender Storage Security deployments.

## Overview

This article explains how the **scheduled scan timing** works in **MetaDefender Storage Security**, specifically whether it relies on the operating system’s time or an internal timer mechanism within the product.

---

### Question

There may be uncertainty about how **scheduled scans** are triggered in MetaDefender Storage Security — specifically whether the scheduling is determined by the **operating system’s local time** or by an **internal timer** within the product.

---

### Clarification

- The **scheduled scan** in MetaDefender Storage Security runs according to the **operating system’s local time**.
- For example, if a scheduled scan is configured to run **every 1 hour**, and the system time is currently **4:03**, the next scan will initiate at **5:03 (OS time)**.

---

### Additional Notes

- Ensure that the **system clock** and **timezone settings** on the host operating system are accurate, as these directly affect the timing of scheduled scans.
- Any drift or misconfiguration in system time may result in delayed or early scan execution.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
