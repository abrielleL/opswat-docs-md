<!-- source: https://www.opswat.com/docs/cm/patch-management/patch-dashboard -->

# Patch Dashboard

**Patch Dashboard** gives you a centralized view of OS and application patch posture, and deployment results across your environment. Use dashboard widgets to discover security gaps, prioritize what to fix first, and confirm your deployment outcome.

In the left navigation, select **Patch Management > Overview**.

Choose the tab you need:

- **Operating System**: OS patch posture across Windows, Linux, and macOS.
- **Third Party Applications**: Installed-software posture.
- **Driver & Firmware**: Driver, BIOS, and firmware update posture.
- **Job**: Deployment activity and outcomes.

![](https://uploads.developerhub.io/prod/97qW/hh0dk5bjntn5bsszys7681h3azk4azjb6l5omc69hn3jzgukmjc47ahd7dhchma6.png)

## Discover and Prioritize Risk

Use the dashboard widgets from Operating System or Third Party Applications tab to find your biggest gaps and decide what to fix first.

Quick jump to your specific goal:

- [Assess overall exposure](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#assess-overall-exposure)
- [Prioritize what to fix](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#prioritize-what-to-fix)
- [Find long-standing risks](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#find-long-standing-risks)
- [Track risk trend (Application)](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#track-risk-trend-application)
- [Check for approval bottlenecks (OS)](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#check-for-approval-bottlenecks-os)
- [Determine platform-specific risk](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#determine-platform-specific-risk)
- [Focus on high-impact patches](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#focus-on-high-impact-patches)

### Assess overall exposure

| Widgets | Details |
| ---- | ---- |
| - Patch Risk Summary (OS) ![](https://uploads.developerhub.io/prod/97qW/gal6jj3zbs2a42j4p4t0vudl7qmxuc07e5m1vnqfgkk9cunyejw2hwl44e4s825q.png) - Summary (Applications) ![](https://uploads.developerhub.io/prod/97qW/yh3k2numvxlwtf45vl7e12jhhjfcte2jtw9nygorkmjawaov51vk76v1v3lkmgyx.png) - Update Risk Summary (Driver & Firmware) ![](https://uploads.developerhub.io/prod/97qW/wb7fj63mnfq0nxazlirdy9cemxyshbd59fktqxq1ai92fm2uocvm9mjf1odh0ir1.png) | Gives the quickest overview of your patch posture and critical gaps. |

### Prioritize what to fix

If your organization tracks remediation targets, start with SLA compliance. Otherwise, start with severity.

| Priority | Widgets | Details |
| ---- | ---- | ---- |
| SLA Compliance | - Missing OS Patches SLA Compliance  ![](https://uploads.developerhub.io/prod/97qW/h87xiuxtvg3ry9caf2coca5por7nodpmcimlz08ljogy065xq62zqhqco45woar5.png) - Application Patches SLA Compliance  ![](https://uploads.developerhub.io/prod/97qW/1ffrzdgb4nqgxg9i2njo4dt0163wdz36fvpf3tpxyrntnvag3rmll0xprt04vbj0.png) - Missing Driver & Firmware Updates SLA Compliance ![](https://uploads.developerhub.io/prod/97qW/nfjo14uc1yzdn06qt6i8i89zy432ebxjzkfmo7xbfejmgoyl76gfeic9s91036d9.png) | Show patches that require immediate attention based on configured SLA. See [Patch SLA](https://www.opswat.com/docs/cm/patch-management/patch-sla) for configuration guideline. |
| Severity | - Missing Patches by Severity ![](https://uploads.developerhub.io/prod/97qW/j4gi708rrh50pevsjm4jv3lru7mth21oaxozuv56ueu8bpc9cq48x0o2q7gwr9eu.png) - Application Patches by Severity ![](https://uploads.developerhub.io/prod/97qW/w41hl2fycp4aqo3b89pkrcvebyyzv0hl1pfigahe5uo4nwxn6swyopolh3y0ix9x.png) - Missing Updates by Severity (Driver & Firmware) ![](https://uploads.developerhub.io/prod/97qW/sjjaewvbwidn4ny454tu6ihgltb3c64gag4ut553f6ihwqkwbf7i7sp8mhs0r146.png) | Break down missing patches and application updates by severity level. See [Manage Missing Patches and Outdated Applications](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches) for more details. |

### Find long-standing risks

| Widgets | Details |
| ---- | ---- |
| - Missing OS Patches by Release Date ![](https://uploads.developerhub.io/prod/97qW/esv00egijxc8f5vytpj2ioaf3c0q89i9bctqxno60jrr5jmosuguxddeigi8asej.png) - Application Vulnerability by Age ![](https://uploads.developerhub.io/prod/97qW/ront9nl23ohqvkc3nvrc9wjlwl9ybdcte9d5ykjvk8iecv7spaynm7j040rb3e02.png) - Missing Driver & Firmware Updates by Release Date ![](https://uploads.developerhub.io/prod/97qW/05x6maazf85j04ypymxr9lgmvt8s1k2xpez00otogum7nf49tzfxsolfa832ua9r.png) | Surfacing long-standing missing patches and vulnerable applications that may indicate neglected devices or unsuccessful remediation efforts |

### Track risk trend (Application)

| Widgets | Details |
| ---- | ---- |
| Vulnerabilities Trend Last 14 Days ![](https://uploads.developerhub.io/prod/97qW/aoow5vh6gsq5vxg6ii8u3okha36xy8yozu8ssjff1c8amn81mtt54jl41he7nse3.png) | Show whether application vulnerabilities are increasing, decreasing, or remaining unchanged over time |

### Check for approval bottlenecks (OS)

| Widgets | Details |
| ---- | ---- |
| Pending Approval by Severity ![](https://uploads.developerhub.io/prod/97qW/isoadmbv9pkh26wwq5bsonrcdcigpu00jhz9hfrmivu6srs4jgzm0na31qx5qzi0.png) | Identify updates awaiting approval and their severity levels, helping you spot bottlenecks that may prevent timely deployment. |

### Determine platform-specific risk

| Widgets | Details |
| ---- | ---- |
| Missing Patches by Operating System ![](https://uploads.developerhub.io/prod/97qW/k4od6z67xnb207l6wlc9lelve1ikvuussb9blv5nmaoz7uzf4vlz87ty5dsoj1oc.png) | Shows how missing patches are distributed across Windows, Linux, macOS, and other platforms |

### Focus on high-impact patches

| Widgets | Details |
| ---- | ---- |
| - Top 10 Missing Patches by Devices (OS)  ![](https://uploads.developerhub.io/prod/97qW/f9ah4ms7n3r49i2k9him49jze6pqllwyorv2la5qjeopbc2yp03tzm830ltj3ixq.png) - Top Applications by Affected Devices ![](https://uploads.developerhub.io/prod/97qW/1eutjb0ukbhxh4xv76j4iro7emp4gfzlpm695fasmyncj7y0876gac1tck44e24c.png) - Top 10 Missing Updates by Devices (Driver & Firmware) ![](https://uploads.developerhub.io/prod/97qW/zcylzdn21x5fw1iw100g1974eiqqt7dqt079qienppty32544gyd00l9klm1w2n8.png) | Identifies the patches or applications affecting the most devices. Fixing these closes the most gaps for the least deployment effort. |

## Monitor and Review Deployments

Use the** Jobs** tab to confirm your deployments worked and catch problems early. These widgets cover both OS and application deployments.

Quick jump to your specific goal:

- [Confirm deployments succeeded](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#confirm-deployments-succeeded)
- [Review device-level outcomes](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#review-device-level-outcomes)
- [Investigate deployment issues](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#investigate-deployment-issues)
- [Track deployment volume](https://www.opswat.com/docs/cm/patch-management/patch-dashboard#track-deployment-volume)

### Confirm deployments succeeded

| Widget | Details |
| ---- | ---- |
| Deployment Summary ![](https://uploads.developerhub.io/prod/97qW/bf9tmg05pb0g7k92o0pz0ry5m8kuxq86ud7ut1ckop58a6m2onvwd7141zs3vow1.png) | Overview of all active and completed deployment states. |
| Patch Installation Success Rate ![](https://uploads.developerhub.io/prod/97qW/hif1jricbbia1gq8e6ne3q6mkmolmnsu72ihxt4ptq2kbh0i7bi87i8egc6or579.png) | Ratio of successful installs to total installation attempts. Your clearest signal that patching is working. |

### Review device-level outcomes

| Widget | Details |
| ---- | ---- |
| Deployment Results by Device ![](https://uploads.developerhub.io/prod/97qW/mqo9ua5acmn169mhikvfvairdakh9atq9jqnbj1h7n6qyfa9bp7yuty4hb90oxyj.png) | Groups every endpoint by outcome, so you can spot patterns across devices. |

### Investigate deployment issues

| Widget | Details |
| ---- | ---- |
| Deployment Issues Trend ![](https://uploads.developerhub.io/prod/97qW/8adk0egizqhlsd8ovv0z2xkpyu3pfcnmzrr2eyrgjyhg9g5tawpkvgad23j0zp7z.png) | Daily failure counts by error reason. Helps you spot a systemic cause instead of a one-off error. |

### Track deployment volume

| Widget | Details |
| ---- | ---- |
| Deployment History ![](https://uploads.developerhub.io/prod/97qW/gxlocdmhdrr9188p5rprovn9wd8ne7treahzp9akryu5dfjay75xqdb279s17xbn.png) | Daily deployment volume over time. |
| Top 10 Deployments by Target Devices ![](https://uploads.developerhub.io/prod/97qW/pc58a0suf4ccuhglxt8ebvng18mreega4jfb4oemlm0d3pu0i02oc72yt2aa38vm.png) | Your largest jobs by number of targeted endpoints. Worth watching closely. |

## Act on what you find

The Dashboard helps you identify risks. To investigate further and take action, select any widget or chart to open the [Patches](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches) list, where you can drill down on missing patches and outdated applications in greater detail.

You can then:

- Push urgent fixes with [On-Demand Deployment](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment)
- Automate recurring patching with [Policy Deployment](https://www.opswat.com/docs/cm/patch-management/policy-deployment)
- Track active and completed deployment jobs in real time with [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
