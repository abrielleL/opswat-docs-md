<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/request-add-application-to-oesis-framework -->

# Request Add Application to OESIS Framework

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Request to have your application added to the OESIS Framework, right from My OPSWAT Portal.

## Get started

1. Sign in to [My OPSWAT Portal](https://my.opswat.com/portal/oem-portal/oesis-submission). No account yet? Sign up first.
2. Go to **OEM Portal → OESIS Submission → Add Submission**.
3. Choose **Add Application to OESIS Framework**.

## Fill in the form

### Installer

Provide the installer in either or both of these ways:

- **Application Package:** upload the installer. Maximum 5 GB.
- **Download URL:** a public http(s) link to the installer.

> **Note:** If you give both, we use the Download URL. If we can’t reach the link, we’ll ask you to fix it.

### Application

- **Application name:** your application’s name.
- **Version:** the exact version of the installer.
- **Operating system:** Windows, macOS or Linux. One OS per submission.
- **App category:** the category your application belongs to.

> **Tip:** When you add a package, we detect the name, version and OS and fill them in for you. Please check that they are correct.

### Supported options

Tick at least one: **Detection**, **Patch**, **Vulnerability**, **App Removal**.

> **Important:** Your application is added only if **every** option you tick passes testing.

### Optional details

- **License key:** allows OPSWAT to test all features. Enter it as text or upload a file (maximum 5 MB).
- **Additional information:** anything that helps testing, such as install steps, test accounts or known limitations.

### Technical contacts

- **Contacts:** who OPSWAT contacts about technical issues.

## Track your status

No more emailing back and forth. See where your submission stands at any time.

- **All submissions in one place:** the **OESIS Submission** page shows your own submissions and your organization’s submissions.
- **We need more information:** you get an email with the reviewer’s note. Open the submission in My OPSWAT Portal, use **Edit & resubmit** to send the update within **30 days**. Otherwise, the submission is closed.
- **Your result is ready:** you get an email. Open the submission and click **Download Report** for the detailed result of each option.

**Possible results:** PASSED (your application is added) or REJECTED (it is not added; the report explains why).

## Questions?

Contact [oesis-addapp@opswat.com](mailto:oesis-addapp@opswat.com).
