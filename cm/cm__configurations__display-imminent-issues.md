<!-- source: https://www.opswat.com/docs/cm/configurations/display-imminent-issues -->

# Display Imminent Issues

Administrators now have the option to display imminent issues on the remediation page. **Imminent issues** are potential compliance problems that, although not currently affecting the system, could impact the compliance status of end-user machines in the near future if left unaddressed.

By highlighting these imminent issues, end-users are informed about their machine's security status and can take proactive measures to resolve any impending problems. This proactive approach helps prevent disruptions in access to resources protected by My OPSWAT Central Management and ensures continued compliance.

To enable this feature, administrators can follow these steps:

1. Log into the My OPSWAT Central Management console and navigate to **Settings > Rebranding.**
2. Select a rebranding package you would like to update.
3. You will see the option to “**Display imminent issues”** in the **Display** section.
4. Make the needed changes and click **Save.**

![](https://uploads.developerhub.io/prod/97qW/r813ycacbvfn4w044gkvcmvgwsn2usxjed3h2tq3x142yqd7l2m1pjwknvi9cq12.png)

(*): *To prevent confusion among end-users, we display imminent issues on the remediation page only when they are about to become actual issues soon. For example, suppose a compliance check requires users to perform a backup every 10 days. In that case, we will show the imminent issue only for users who have not backed up their devices in the last 7 days, indicating that their devices will have a backup issue in 3 days if they neglect the backup.*

When enabled, My OPSWAT Central Management will display the imminent issues in the **Imminent** section on the remediation page. On the right side of each imminent issue, end-users will see the time left to resolve it before it changes to an actual one and affects the machines' compliance status.

![](https://uploads.developerhub.io/prod/97qW/jbg3fr63rurpjtjuq4kj6mi9jxi9d0lhjl9o44gm3b3xl2iql7xfmm2weo4rmehw.png)

The imminent issues display feature supports only the policy  compliance checks listed below

- **Anti-Malware**
  - Signature definition is updated at least every [N] day(s)
  - No full system scan completed in the last [N] day(s)

![](https://uploads.developerhub.io/prod/97qW/p4mw7x7cyytcp3jb7bh0tpdouuyapjpyyxbfwt1m2ddkapnddogv4manjgso9354.jpeg)

- **Backup**
  - No backup activity within the last [N] day(s)

![](https://uploads.developerhub.io/prod/97qW/39emwyd1h2u0l8f2we9l22of3e6dbie2dxopibeun5cvrnixlqftzuo5yslmrugv.jpeg)

- **Operating System**
  - Update(s) have been available for [N] day(s) or more
  - Device has not been rebooted in over [N] day(s)

![](https://uploads.developerhub.io/prod/97qW/2t2w042dhcxzwc5cqoir8hq7uxiyny3wiaubbkw7lb6txzq1e7sgp4suqjuecufo.jpeg)

- **Security & Health (Mobile)**
  - Device has not been rebooted in over [N] day(s)

![](https://uploads.developerhub.io/prod/97qW/xq12c048t6w2hvxhyu7ntl7z9407rejyg5pykcm9nunuzee7i9auiu6h0gva1wk2.jpeg)

- **Vulnerabilities and Exposures**
  - Device has CVEs match the conditions below: CVEs with [severity level] for [N] day(s) or more

![](https://uploads.developerhub.io/prod/97qW/hziyht8g8262f2as3v0x08l3yhc4m6m7rm7egi4hmlnn00sl4zbil9r7lsrhch85.jpeg)

- **Patch Management**
  - Patch management agent has reported: [Any/Required missing patches] in [all categories/the following category] with [all/specific severity level] : [critical, important, moderate, low] over [N] day(s)

![](https://uploads.developerhub.io/prod/97qW/r4pbr5eejvr75x98qheg13ba4b9971j8ow3fdbtd5fh8trqraerju41baxyvhaef.jpeg)
