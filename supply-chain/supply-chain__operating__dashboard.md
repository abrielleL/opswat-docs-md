<!-- source: https://www.opswat.com/docs/supply-chain/operating/dashboard -->

# Dashboard

The MetaDefender Software Supply Chain dashboard gives you an overview of the security posture of all your scanned repositories. It has two tabs:

- **Overview**: overall risk indicators, the vulnerabilities that were found, the riskiest packages and repositories, how vulnerabilities evolve over time, and actionable security suggestions.
- **Cryptography**: the cryptographic assets found in your scans and how ready they are for post-quantum cryptography.

On the Overview tab, use the two filters in the upper-right corner to scope the data. The connection filter (All Connections by default) limits the data to a single connection. The time-range filter switches between Last 24 hours, Last 7 days, Last 30 days, Last 90 days and All time; the default is Last 30 days. The filters do not apply to the Cryptography tab.

![](https://uploads.developerhub.io/prod/jdK6/96vglfh7k07hujqdfpzruo97tuc4hqp06o0b597vnxji61kxnfgir21n2whj6agf.png)

![](https://uploads.developerhub.io/prod/jdK6/19qgas76n552dxey3npnystzwjljifpfj1863ajq1o1h2usonjb1tfs6sk96mjwl.jpeg)

## Risks Summary

The Risks Summary card shows four key security indicators:

- **Risk Score:** the average of the risk scores across all scanned repositories, on a 0-100 scale, where 0 means clean.
- **Threats:** the number of detected threats.
- **Secrets:** the number of detected secrets, such as credentials or tokens committed to the code.
- **Critical Vulnerabilities:** the number of vulnerabilities with Critical severity.

![](https://uploads.developerhub.io/prod/jdK6/gfcyh8i8iryrib3w2cn43qemrndiu5188f31i8f82n5kf4eb1smgvr73sg68da4c.png)

The arrow next to a value indicates its trend within the selected time range: a red rising arrow means the value increased, while a green falling arrow means it improved.

## Vulnerabilities and Top Risks

Three cards provide a breakdown of what was found across your repositories:

- **Vulnerabilities Found:** the total number of vulnerabilities, categorized by severity: Critical, High, Medium, Low, and Unknown.
- **Top Risky Packages:** the packages with the highest risk. The number next to each package is the number of critical vulnerabilities found in it.
- **Top Risky Repositories:** the scanned repositories with the highest risk scores, on a 0-100 scale.

![](https://uploads.developerhub.io/prod/jdK6/sllnz6x07rek466m1r2yy7tezynaajt43rku1nhzj00jev2rs3pu7siqpxnkjl70.png)

Use the **View Reports** links in the corner of the cards to open the Reports page pre-filtered to the corresponding data.

## Vulnerability Trend

The Vulnerability Trend chart provides a visual representation of how vulnerabilities evolve across your environment over the selected time range. The summary above the chart shows the current totals for each severity level, together with their trends. By tracking changes in vulnerability counts, you can identify patterns, monitor remediation progress, and detect emerging threats.

![](https://uploads.developerhub.io/prod/jdK6/92g7of33rl1ihtcl8btpofjja601sy2dx3hsuzv7pcr43nrtdee01cysx813ni0a.png)

The chart is interactive: hover over any data point to reveal a tooltip with the exact vulnerability counts for that period, and click the legend items below the chart to toggle the visibility of individual severity levels for a focused comparison.

## Security Suggestions

The Security Suggestions table lists the most impactful package updates you can make, based on the top risky packages found in your repositories:

- **Fix:** the suggested action, for example updating a package to a newer version.
- **Repository:** the repositories where the package was found.
- **Current Version** and **Recommended Version:** the detected version and the version that resolves the issues.
- **Effect:** the number of vulnerabilities that the update would fix.
- **Impact:** the severity of the improvement.

Use the copy button at the end of a row to copy the update command to your clipboard, or click the row to open the package details.

## Cryptography

The Cryptography tab gives you an overview of the cryptography in your software. It summarizes every cryptographic asset that MetaDefender Core found across all your jobs: algorithms, certificates, protocols, related crypto material (such as keys) and libraries. It shows which assets are weak against today’s attacks or not quantum safe, and it recommends post-quantum replacements.

## Cryptographic posture

The Cryptographic posture card shows five key indicators:

- **Crypto assets**: the number of distinct assets found, one per asset type and name. An asset found in many files counts once.
- **Not quantum safe**: the number of assets in NIST category 0.
- **Quantum readiness**: the share of assets with a NIST category that are in categories 1 to 6. Assets without a category are left out.
- **Affected files**: the number of files with at least one asset that was not assessed as quantum safe, out of all scanned files.
- **Classical risk**: the number of assets that are deprecated or disallowed against today’s attacks.

![](https://uploads.developerhub.io/prod/jdK6/540vrex42eqwhglrj14pujed14vb5lnawxuznlo0p4hx587cy4d4gi745nph3bkf.png)

## Asset type, Classical risk and Quantum level

Three cards break the assets down:

- **Asset type**: the total number of assets and the number of each type: Algorithm, Certificate, Protocol, Related material and Library. Select a type to open the matching assets in Reports.
- **Classical risk**: assets by MetaDefender Core’s verdict against today’s attacks: Disallowed, Deprecated, Acceptable or Unknown. Unknown means Core did not have enough information to decide. It does not mean that the asset is safe.
- **Quantum level**: assets by NIST category, from L0 (not quantum safe) to L6, plus Unknown for assets without a category.

In the Classical risk and Quantum level charts, select a segment to highlight it. Then select **View results** to open the matching assets in Reports. With no segment selected, **View results** opens all assets.

![](https://uploads.developerhub.io/prod/jdK6/ufvvvjobkr9zkw8smbynjwyuagudufp6vqxm9y1544igj7b473qgucglscexjpkm.png)

## Priority assets

The Priority assets card lists the 5 assets found in the most jobs, in three tabs:

- **Not quantum safe**: assets in NIST category 0.
- **Weak today**: assets that are deprecated or disallowed against today’s attacks.
- **Protocols & certificates**: protocols and certificates that are not quantum safe because of the algorithms they use.

Each row shows the asset name, its type, the recommended replacements, and the number of jobs and files where it was found. Select a row to open the asset details. Select **View Reports** to open the full list for the active tab.

## Worst files

The Worst files card lists the 5 files with the most assets that were not assessed as quantum safe, in the newest completed job of each repository. Each row shows the file name, its folder and the number of assets that are not quantum safe. The color of the count is relative to the worst file in the list. Select a file to open its details.

![](https://uploads.developerhub.io/prod/jdK6/b8d98xryt66nvuf2ynifcjedsfnimp4u8fvbpur2uvj69iup10sbsmeslu30vmu8.png)

## Migration plan

The Migration plan card shows the post-quantum replacements that MetaDefender Core recommends for your assets that are not quantum safe. The replacements are grouped by algorithm, for example ML-KEM (FIPS 203). Each tile shows:

- The replacement algorithm and its NIST standard.
- What the replacement applies to, for example key exchange.
- The number of assets it replaces, and up to 5 of them. Select an asset to open its details.

The tiles are sorted by the number of assets they replace, most first. The plan is based on the 100 assets that are not quantum safe and appear in the most jobs. A note under the tiles shows how many assets have no recommended replacement. Select **View Reports** to open all assets that are not quantum safe.

![](https://uploads.developerhub.io/prod/jdK6/cv2el90h6ngp3a2e7q7c2vvqrja7vk0d5wqtrjj66cnc9uz3rsof2zzp1fl7k13g.png)

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
