<!-- source: https://www.opswat.com/docs/supply-chain/operating/scheduling-automatic-scanningqnr -->

# Hash Scanning

MetaDefender Software Supply Chain supports differential (hash) scanning: it detects whether files have changed since the last scan, and skips the files that have not. Scans run faster while still identifying new or modified content.

## Configure hash scanning

Hash scanning is configured per workflow:

- Go to the **Workflows** page and open the workflow you want to configure.
- In the workflow diagram, click the **Hash Scanning** step. The Hash Scanning panel opens:

![](https://uploads.developerhub.io/prod/jdK6/wuv3lb6y5uowun2ttidqtli06cpq4cpaq4n158ki8y55m8l4hb0jwsc95y3t9mk7.png)

- Turn the toggle to **Enabled** and set the scan frequency in the **Days Before Rescan** field - files that have not changed within the specified number of days are skipped:

![](https://uploads.developerhub.io/prod/jdK6/srxcty13606pkq5o96em96kvwtut9a4sqelolqic922i63hpa7ke9y0wu6wxqevn.png)

- Click **Save Changes**.

When the next scan starts, the system compares the latest version of your repository against the previously scanned version and only scans the changes.

If Hash Scanning is not activated then all files are scanned.
