<!-- source: https://www.opswat.com/docs/supply-chain/operating/dashboard -->

# Dashboard

The MetaDefender Software Supply Chain dashboard gives you an overview of the security posture of all your scanned repositories: overall risk indicators, the vulnerabilities that were found, the riskiest packages and repositories, how vulnerabilities evolve over time, and actionable security suggestions.

Use the two filters in the upper-right corner to scope all of the dashboard data: the connection filter (**All Connections** by default) limits the data to a single connection, and the time-range filter switches between **Last 24 hours**, **Last 7 days**, **Last 30 days**, and **All time**.

![](https://uploads.developerhub.io/prod/jdK6/96vglfh7k07hujqdfpzruo97tuc4hqp06o0b597vnxji61kxnfgir21n2whj6agf.png)

## Risks Summary

The Risks Summary card shows four key security indicators:

- **Risk Score:** the average of the risk scores across all scanned repositories, on a 0-100 scale, where 0 means clean.
- **Threats:** the number of detected threats.
- **Secrets:** the number of detected secrets, such as credentials or tokens committed to the code.
- **Critical Vulnerabilities:** the number of vulnerabilities with Critical severity.

![](https://uploads.developerhub.io/prod/jdK6/gfcyh8i8iryrib3w2cn43qemrndiu5188f31i8f82n5kf4eb1smgvr73sg68da4c.png)

The arrow next to a value indicates its trend within the selected time range: a red rising arrow means the value increased, while a green falling arrow means it improved.

## [Risk Score](https://www.opswat.com/docs/supply-chain/operating/dashboard)

Every scan produces a risk score from 0 to 100 for the scanned repository, where higher means riskier. A scan with no findings scores 0.

The score is not a sum of findings. It is calculated in two stages: the severity of the worst finding sets a baseline, and the volume of findings raises the score from there.

- **Stage 1**

The most severe finding in the repository determines its baseline score:

| **Most severe finding** | **Baseline** |
| ---- | ---- |
| No findings (clean) | 0 |
| Low-severity vulnerability Medium-severity vulnerability Unknown-severity vulnerability High-severity vulnerability Critical-severity vulnerability Exposed secret Malware / infected file | 5 20 30 40 70 75 80 |

- **Stage 2**

Each severity present then contributes additional points on an **exponential saturation curve**: `contribution = ceiling × (1 − e^(−count / growth_rate))`

Both **ceiling** and **growth_rate** are defined per severity. They are calibration values. The curve produces **diminishing returns**: the first findings of a given severity contribute the most, each subsequent one contributes less, and the contribution approaches that severity's ceiling without ever exceeding it. The final score is the baseline plus all contributions, capped at **100**.

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
