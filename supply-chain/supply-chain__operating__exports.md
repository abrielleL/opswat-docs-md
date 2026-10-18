<!-- source: https://www.opswat.com/docs/supply-chain/operating/exports -->

# Exports

Scan results can be exported at two levels: all scans at once, from the Reports page, or a single report, from its details page.

## Exporting all results

On the **Reports** page, open the **Export** menu in the upper-right corner:

- **Export as PDF - All Scans:** a summary document of all your scans:

![](https://uploads.developerhub.io/prod/jdK6/zaznuwr532sxgh8swn1tzky1k6bfgh3i9auwbmyvxy8fm204rbv8hk4lss4nbu3g.png)

- **Export as CSV - All CVEs:** a spreadsheet with every CVE found across your repositories:

![](https://uploads.developerhub.io/prod/jdK6/emmpdw5dd9b5gh6uty11vhhfeagumxdrfc4wpbky32yoqglf65cqjkpm808xir84.png)

- **Export as CSV - All Packages:** available while the **Packages** tab is selected - a spreadsheet with every discovered package.

## Exporting a single report

Open a report from the Reports page and use the **Export as** menu in the upper-right corner. The following formats are available:

- **PDF - Overview:** a human-readable summary of the scan:

![](https://uploads.developerhub.io/prod/jdK6/ffsrhbn6qvcsoz166jdd4i49tq66a8uns9t49z2rhn7dxw70sohy9icyx2lgv42k.png)

- **PDF - SBOM:** the Software Bill of Materials as a document:

![](https://uploads.developerhub.io/prod/jdK6/sic8jv0rropqzy0w5fcaztb72d7s9jadr91lu048v7fcu1unjbalvorusqggqjyp.png)

- **PDF - SBOM with Dependencies:** the Software Bill of Materials as a document, including the dependencies of each package:

![](https://uploads.developerhub.io/prod/jdK6/eamr8l8lq7d78lps33j3fubxmqouqz27ohfs2ym6zqedba88n24vb6geubngv9ch.png)

- **CycloneDX:** the SBOM in the standard CycloneDX format, for use in other tools:

![](https://uploads.developerhub.io/prod/jdK6/gbfja0yxczuj2t1rmwkkdjeo6r2hplhlwmirao047ue1oquwkmwmhs111u05itin.png)

- **SPDX 3.0:** the SBOM in the standard SPDX 3.0 format:

![](https://uploads.developerhub.io/prod/jdK6/48qvtkbax74akkzhyqppovxiicgbo7alje83py88fugf05pblz50x2rwe8fvmnma.png)

- **CSV - SBOM:** the SBOM as a spreadsheet:

![](https://uploads.developerhub.io/prod/jdK6/n9u4y528xjvnuwva3ojqspem23hqf3tjlal3tfi42li13fxkibhhqkvogujv0q4i.png)

**Note:** Cryptographic Bill of Materials (CBOM) export is not supported yet. To review the cryptographic assets, use the Cryptography tab of the Reports page or of a report.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
