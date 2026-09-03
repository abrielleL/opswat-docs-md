<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-time-synchronization-issues-affect-my-opswat-central-managem -->

# How time synchronization issues affect My OPSWAT Central Management v10 and MetaDefender Endpoint?

> **Check Your Version:** This article applies to all My OPSWAT Central Management version 10.x and MetaDefender Endpoint all versions.

## Issues

My OPSWAT Central Management v10 (OCM10) may not fully reflect endpoint statuses—for example, it might not show antimalware status, missing patch information, or may display time synchronization errors in the device details.

## Root causes

Accurate time synchronization is critical for both OCM10 and MetaDefender Endpoint. These components rely on consistent timestamps to validate reports.
If the system time is incorrect, reports may be considered invalid and rejected. This behavior is part of OPSWAT’s security design to prevent users or malicious actors from resubmitting outdated data to bypass validation mechanisms.

## Solution

Configure the Central Management server to use the **UTC timezone** to ensure consistent timekeeping across systems. This helps prevent timestamp discrepancies and ensures proper validation of reports and compliance checks.

> > **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
