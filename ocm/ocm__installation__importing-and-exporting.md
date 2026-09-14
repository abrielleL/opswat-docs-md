<!-- source: https://www.opswat.com/docs/ocm/installation/importing-and-exporting -->

# Importing and Exporting

The following guideline describes how to import data from an older version of OPSWAT Central Management (from version 5.2.7).

Navigate to the **Import/Export** page from the sidebar and select which method you would use to transfer data. There are 3 options: [Importing from URL](/docs/ocm/installation/importing-and-exporting#importing-from-url), [Importing from file](/docs/ocm/installation/importing-and-exporting#importing-from-file) and [Exporting to file](/docs/ocm/installation/importing-and-exporting#exporting-to-file).

After a successful import or export, system will log a new entry in the migration history table .

## [Importing from URL](/docs/ocm/installation/importing-and-exporting#importing-from-url)

The following guideline describes how to import data from an older version of OPSWAT Central Management (from version 5.2.7) using its URL

1. Fill out the information and then click the **IMPORT** button.

- **Username, Password:** The administrator credential used to access the older OPSWAT Central Management server

- **Central Management 5.x URL:** The URL of the older OPSWAT Central Management server

2. The information dialog will be opened, please check the migration information before go on to the next step.

3. The loading dialog will be opened.

4. **Import History** will update with the result from the finished import process.

5. The dialog will be closed and the **Import/Export** page will be reloaded automatically with updated **Import History** if the result is successful.

Info

Multiple imports from the same server will only update new changes from the last import. If no change is detected for a specific section, the import history will display '0' in the corresponding column.

## [Importing from file](/docs/ocm/installation/importing-and-exporting#importing-from-file)

The following guideline describes how to import OPSWAT Central Management's data from a .json file.

1. Select the file to be imported via **Choose file.** Select **TEST** to check the validity of the chosen file and continue to the next step if the test is successful.

2. The information dialog will be opened, please check the migration information before go on to the next step.

3. The loading dialog will be opened.

4. The result dialog shows whether the data is imported successfully. Select **Finish** to complete the process.

5. **Import History** will update with the result from the finished import process.

Info

Import History only lists the data that was imported successfully in each import process..

Warning

Importing users data also requires importing user directories data.

## [Exporting to file](/docs/ocm/installation/importing-and-exporting#exporting-to-file)

The following guideline describes how to export OPSWAT Central Management's data to a .json file.

1. Check out the information of exported data.

2. Name the exported file, fill in the PIN and select **EXPORT** to start the export process.

3. The file will be downloaded by the browser.
