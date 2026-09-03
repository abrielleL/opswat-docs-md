<!-- source: https://www.opswat.com/docs/supply-chain/operating/repository-scan-results -->

# Repositories

The **Reports** tab of the Reports page lists a scan report for every scanned repository and reference:

![](https://uploads.developerhub.io/prod/jdK6/m2z9zn4saf2sy5flvo3fuyt4ej5a9vrdfyknx3233z0x87rksj6995j1eh2584gv.png)

Each row shows the connection, the scan status, the repository and reference, the job type, and whether threats, secrets, vulnerabilities, or license risks were detected. Use the search field to find a repository by name, and the filter button to filter by service, service type, severity, licenses, threats, or secrets:

![](https://uploads.developerhub.io/prod/jdK6/tyv2suxmdfgykgeudidvf6i3gsu936tts34m5v3f78ur6jv0guqnnax2sun8rqwv.png)

## Report details

Click a report to open its details. The header summarizes the job: connection, repository, branch, scan type, status, workflow, and date. From here you can **Delete** the report, **Rescan Repository**, or use **Export as** to download the results.

The report is organized into tabs:

- **Packages:** the Software Bill of Materials of the repository - every package that was discovered, with its vulnerabilities, dependency vulnerabilities, licenses, version, and ecosystem. The severity summary and the Package Risks card at the top give the totals at a glance:

![](https://uploads.developerhub.io/prod/jdK6/xnu4uguz4mnrmrb1n3qdpmboycc09xpkumm0amqt131ruox3auekid3rugi4kpfp.png)

- **Files:** every processed file, with its status (Allowed or Blocked), detected threats, secrets, vulnerabilities, licenses, hash, and size. For container scans, this tab shows the image layers instead:

![](https://uploads.developerhub.io/prod/jdK6/hut0qqcpbhp2hoykytkmvqksesm0ahx6quy96ulpo7og8eskc88gnprnjgg6ivo0.png)

- **Job History:** the previous scans of the same repository, so you can compare how the results evolved over time.

## File details

Click a file in the Files tab to open its analysis. The Results cards summarize what each technology found - **Metascan** (antivirus engines), **Proactive DLP** (secrets), and **Software Bill of Materials** (vulnerabilities) - and the tabs above let you drill into the threats prevented, the secrets prevented, and the SBOM findings:

![](https://uploads.developerhub.io/prod/jdK6/nzfv1si9ydcsx1mpfk3t7ssq1rj6le1xph1wdx2ngrlavrh649vhkqncjfd726lc.png)
