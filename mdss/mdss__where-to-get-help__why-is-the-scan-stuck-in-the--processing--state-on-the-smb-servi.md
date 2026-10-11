<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/why-is-the-scan-stuck-in-the--processing--state-on-the-smb-servi -->

# Scan stuck in the "processing" state on the SMB Service

> **Check Your Version:**
>
> This article applies only to releases before 3.5.2, all of which used the Python SMB service. The issue is fixed in 3.5.2 and later, including the legacy SMB service shipped with 4.6.0.

## Symptom

The log appears to be stuck with the following entries:

`Starting processing server. Listening on 127.0.0.1:6002`

`Starting health server. Listening on 127.0.0.1:7002`

`Using configured transport receive timeout of: 600`

`Starting worker`

Under normal conditions, every SMB process keeps logging, each in its own log folder named after its port (6002 to 6006), instead of remaining stuck at this stage.

## Possible Cause

SMB Service process stuck due to insufficient CPU resources The `psutil.open_files()` function hangs or freezes for several minutes, issue occurs specifically on Windows.

## Solution

The issue was fixed starting with Version 3.5.2

> **Support:**
>
> If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
