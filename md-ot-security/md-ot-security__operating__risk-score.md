<!-- source: https://www.opswat.com/docs/md-ot-security/operating/risk-score -->

# Risk Score

The **Risk Score** tab on an asset's detail view shows a single composite score (0–10) summarizing that device's risk, broken down into four weighted factors.

## [How the score is calculated](/docs/md-ot-security/operating/risk-score#how-the-score-is-calculated)

Each factor contributes to the total using the same formula:

**Contribution = Weight × Raw value**

The **Risk Score** is the sum of all four factor contributions. In the example above: 0.50 × 9.8 + 0.20 × 0 + 0.10 × 0 + 0.20 × 7.5 = **6.40 (High)**.

Weights are configured enterprise-wide, not per asset. See **Settings → Application → Risk Score Settings** in the Enterprise - Application Settings guide to view or change them.

## [Factors](/docs/md-ot-security/operating/risk-score#factors)

| Factor | Default weight | Raw value | Card also shows |
| --- | --- | --- | --- |
| Vulnerabilities | 50% | Max CVSS v3.1 score across the asset's open CVEs | CVE count, a link to View Vulnerabilities |
| Alerts | 20% | Highest pending alert severity (Low=2.5, Medium=5, High=7.5, Critical=10) | Pending alert count, a link to View Alerts |
| Misconfigurations | 10% | 10 if any abnormal misconfiguration exists on the asset, else 0 | Normal/Abnormal status, a link to View Misconfigurations |
| Asset Criticality | 20% | The asset's assigned criticality (Low=2.5, Medium=5, High=7.5, Critical=10) | Criticality label, an Edit criticality link |

Each factor card shows its own weight, raw value, and the resulting contribution, so you can see exactly which factor is driving the score up or down for that device.

## [Reading the scale](/docs/md-ot-security/operating/risk-score#reading-the-scale)

The Risk Score header shows a colored gauge with the current score marked against four bands:

- 0 – 2.5: Low
- 2.5 – 5: Medium
- 5 – 7.5: High
- 7.5 – 10: Critical

## [Asset Criticality](/docs/md-ot-security/operating/risk-score#asset-criticality)

Unlike the other three factors, Asset Criticality is not derived automatically — it is a per-asset field an operator sets manually. Click **Edit criticality** on the Asset Criticality card to change it (Low/Medium/High/Critical); the Risk Score recalculates immediately using the new value.
