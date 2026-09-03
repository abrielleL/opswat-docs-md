<!-- source: https://www.opswat.com/docs/supply-chain/operating/packages -->

# Packages

The **Packages** tab of the Reports page is the package-centric view of your scan results: every package discovered across your scans, aggregated into a single Software Bill of Materials. The severity summary at the top shows the total number of vulnerabilities across all packages.

![](https://uploads.developerhub.io/prod/jdK6/2gq9apy7adfvl03avqlpuzc7wll66wj2cytwnttyueeuiti94ktbn1nmh30sokj4.png)

For each package you can see its version, the repositories where issues were found, the number of vulnerabilities by severity, the license risks, and when it was last updated. Use the search field to find a package by name, and the column filters to filter by severity or license risk. Click a package to open its details.

## Package details

Click a package in the Packages tab to open its **Package Overview** - the list of all scanned versions of that package, each with its vulnerabilities, license risks, release date, and the recommended version to upgrade to:

![](https://uploads.developerhub.io/prod/jdK6/1n6orrblwuw5ajbu4tqbbpg0bijykfldqw0oa73tg4piweoswuwlmwskvs976r6n.png)

Click a version to open the **package version details**. You can also land here directly from the **Packages** tab of a report or from the **Security Suggestions** table on the dashboard. The page shows:

- a warning banner with the recommended upgrade, when vulnerabilities were found in this version;
- **Package Summary:** the supplier, the release date, and the latest available version and release;
- **Software Bill of Materials:** the vulnerability totals by severity - click a severity to filter the CVE list below;
- **License Risks:** the number of blocked licenses, with the details of each license;
- **CVEs:** every vulnerability found in this version, with its severity and the versions that fix it. Expand a row for the description, the CVSS score, and the references, or use the arrow at the end of the row to open the reference in a new tab;
- **Connections:** where the package was found - the connection, repository, reference, and scan date.

![](https://uploads.developerhub.io/prod/jdK6/jr3se3vugous0u57qpytpdqz3j4vvtznvun47z7txjci8f39a062y1s3kql4g2ly.png)

## Package labels

You can attach labels to packages to categorize them - for example, to mark a finding as a false positive. Labels are managed from the **Packages** tab of a report:

- Click the label icon at the end of a package row. The Labels panel opens, showing the labels already attached to the package:

![](https://uploads.developerhub.io/prod/jdK6/p0iopjfmybrv3vn6osip9otn23hx6wnfdizpoatif9penwmfcy0vyu26hwkqaqxi.png)

- Select an existing global label, or choose **New Label** to create one:

![](https://uploads.developerhub.io/prod/jdK6/hry07ocoh4x8jy6t7wzq5glep23xx8g4vqiqwvcurhv5j2cwcqvd6nrgfnhwkpi2.png)

- Give the new label a **Name** and select its **Value Type**:

![](https://uploads.developerhub.io/prod/jdK6/f7mkybh8wdpxtrdvsz05pijna8s4l440v8lan9zv7pmr0n3qnv1nwdc4js51g3d4.png)

- The value can be a free **Text**, a **Date**, or a **Dropdown** with predefined options:

![](https://uploads.developerhub.io/prod/jdK6/hcbzxaaq23kphpsev07ihyb6mwjm02ampxqyqe4hyur0xspwob8okqvwyfm91gm2.png)

- For dropdown labels, define the available options and select the value to apply:

![](https://uploads.developerhub.io/prod/jdK6/9jova7rjkp49aeg7hv8lcttkxczfrr8y7hqjxj5lhbux2hpjgv8i0tw46llo1mrc.png)

- Click **Attach**. The label is displayed in the **Labels** column of the package:

![](https://uploads.developerhub.io/prod/jdK6/vdokbkbbxodux948abch893nram3qpoz2m70waop42c20vmcu46wvprz6ezaapf9.png)
