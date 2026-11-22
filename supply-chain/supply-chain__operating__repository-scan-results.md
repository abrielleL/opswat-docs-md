<!-- source: https://www.opswat.com/docs/supply-chain/operating/repository-scan-results -->

# Repositories

The **Reports** tab of the Reports page lists a scan report for every scanned repository and reference:

![](https://uploads.developerhub.io/prod/jdK6/0eya3zj1y99nyw3dgkea0th3pfzwsvjlba3hn0429va5caa4909rvh8luwv6rtp4.png)

Each row shows the connection, the scan status, the repository and reference, the job type, the quantum verdict, and whether threats, secrets, vulnerabilities, or license risks were detected. Use the search field to find a repository by name, and the filter button to filter by service, service type, status, workflow, vulnerabilities, quantum verdict, licenses, threats, or secrets:

![](https://uploads.developerhub.io/prod/jdK6/qhwecb3bpaothitlmzv0v76uxfbwdahm00qlto6coznhvuvdymoq18rchqboomvx.png)

## Report details

Click a report to open its details. The header summarizes the job: connection, repository, branch, scan type, status, workflow, date, and duration. From here you can **Delete** the report, **Rescan Repository**, or use **Export as** to download the results.

The report is organized into tabs:

- **Packages:** the Software Bill of Materials of the repository - every package that was discovered, with its vulnerabilities, dependency vulnerabilities, licenses, version, and ecosystem. The severity summary and the Package Risks card at the top give the totals at a glance:

![](https://uploads.developerhub.io/prod/jdK6/oi1lmhuub0qzk6ehk278tjdhquuk6fqm3cb0hdphjappp2dsx9z3voemkg9ye18b.png)

- **Files:** every processed file, with its status (Allowed or Blocked), detected threats, secrets, vulnerabilities, licenses, hash, and size. For container scans, this tab is named Layers and shows the image layers instead:

![](https://uploads.developerhub.io/prod/jdK6/gs7hlc917gcai1x6idw490v1sss12c9378ci8khdqfbp1kle49fzg3zed74rot2r.png)

- **Cryptography:** the Cryptographic Bill of Materials of the repository - every asset found in the repository, with its asset type, quantum status, and classical risk. The Asset type, Classical risk, and Quantum security level cards at the top give the totals at a glance:

![](https://uploads.developerhub.io/prod/jdK6/u2seepwvc4svsijoaaobnadzwsijrkx7yf8hgudoccjfzlxngc310fx0tfpagzxu.png)

- **Job History:** the previous scans of the same repository, so you can compare how the results evolved over time. Select scans in this tab to compare them. See [Compare scans](#compare-scans).
- **Breakdown**: where the scan spent its time. Files over time shows how many files are in each state (Waiting, Queued, Uploading, Scanning, Processing, Remediation, Done, and Failed), Time per file and Slowest files show which steps took the longest. The breakdown is available for scans made with version 4.3 or later.

![](https://uploads.developerhub.io/prod/jdK6/rx2f2jmz2pu59e7th87fi9m4v5zc3k7ks6szr8c3bthk40j6py7u2yysm9pmb95q.png)

## File details

Click a file in the Files tab to open its analysis. The Results cards summarize what each technology found - **Metascan **(antivirus engines), **Proactive DLP **(secrets), **Software Bill of Materials **(vulnerabilities), and **Cryptography **(cryptographic assets) - and the tabs above let you drill into the threats prevented, the secrets prevented, the SBOM findings, and the cryptographic assets.

The Timeline shows the time the file spent in each step: Scan queued, Discovered, Waiting, Queued, Uploading, Scanning, Processing and Remediation. Processed shows the post-processing time of the whole scan. If the file failed, the Timeline marks the step where it stopped and shows the failure reason.

![](https://uploads.developerhub.io/prod/jdK6/sgdu6qrnezezfofuni3x8psncg4ko125m6affl4a9svfbu0ngzscgw6j9tgz7zdk.png)

## Compare scans

Compare Scans shows how the findings changed between scans. You can compare 2 to 6 completed scans of the same repository, reference and workflow. For file scans, you can compare scans of the same file and workflow.

### Select the scans

To select the scans from a list:

1. Open one of these lists: the **Reports** tab of the Reports page, the **Job History** tab of a report, the **Job History** card of a reference in Inventory, or the **Analyze Jobs** table.
2. Select the checkbox of each scan. After the first selection, the scans that cannot be compared with it are disabled.
3. Click **Compare** in the selection bar.

![](https://uploads.developerhub.io/prod/jdK6/v5on35sbcds1d7zpubta0tii2kro41dzua4r85jsd95yj2uazmypmjcw5oz0b078.png)

To start from a report:

1. Open a completed report and click **Compare** in the header.
2. In the **Compare with another scan** panel, select 1 to 5 scans under **Compare against**. The panel lists only the scans that can be compared with the open report.
3. Click **Compare**.

These rules apply to the selection:

- All scans are completed. Running, failed and cancelled scans cannot be compared.
- Repository scans are of the same repository and the same reference (branch or tag).
- File scans are of the same file.
- All scans ran under the same workflow.
- Repository scans and file scans cannot be compared with each other.
- At most 6 scans are compared.

If the selection breaks a rule, the page shows **These scans can't be compared** and the reason. Click **Change selection** to go back.

### Read the comparison

The **Scope** card shows the repository or the file, the connection and the reference. Next to it, one card shows the date and the scan type of each scan:

- With 2 scans, the cards are **Baseline** and **Target**. Click the swap button between the cards to exchange them.
- With 3 to 6 scans, the cards are **Baseline**, **Scan 2** and so on, and **Latest**. The scans are in order of start time, oldest first.

![](https://uploads.developerhub.io/prod/jdK6/h3anqseavosx93n718vsasdw52golq12lnq39js9xqgry9ilswamjxvrjypjqkll.png)

The comparison is organized into tabs:

- **Overview**: one column for each scan, with the date, scan type, workflow, files processed, duration, CVEs by severity, vulnerable packages, threats and secrets. With 2 scans, the **Change** column shows the target relative to the baseline. With 3 to 6 scans, each value shows the change against the previous scan.
- **SBOM**: the **CVE Changes** card counts the CVEs by change and by severity. The **CVEs** table lists each CVE with its severity, package, ecosystem, version in both scans, fixed version and change. The **Packages** table compares the total packages, vulnerable packages and license risks.
- **Threats** and **Secrets**: the files where threats or secrets were found, with the file name, path and change.

Each finding has one of these changes:

- **New**: found in the target, but not in the baseline.
- **Resolved**: found in the baseline, but not in the target.
- **Persisting**: found in both scans.

Click **New**, **Resolved** or **Persisting** to filter the table. Click it again to show all changes.

![](https://uploads.developerhub.io/prod/jdK6/wlooad5bhn8drv1xt0jxskc1qh4otcp69195jqp8vh7vmdckxmerucfo3wpyqsbm.png)

> With 3 to 6 scans, the SBOM, Threats and Secrets tabs compare the Baseline with the Latest scan only. The scans in between appear only on the Overview tab.

### Large scans

The SBOM, Threats and Secrets tabs read the file list of each scan. The Overview tab does not.

- If the baseline and the target hold more than 2,000 files together, the page shows **These scans are large** with the number of files. Click **Read files and compare** to continue.
- The page reads the first 10,000 files of each scan. If a scan has more files, a warning names the scan. A finding in a file that was not read is not counted as New or Resolved.

### Share a comparison

The address of the comparison page holds the selected scans and the open tab. To share a comparison with another user, copy the address from the browser.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
