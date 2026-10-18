<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/dell-emc-isilon-onefs -->

# Dell EMC Isilon OneFS

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## On-Demand Scanning

EMC Isilon OneFS has the ability to scan files before they are opened, or after they are closed.

Note

Not compatible with Deep CDR

EMC Isilon OneFS On-Demand Scanning is not currently compatible with OPSWAT [Deep CDR](https://onlinehelp.opswat.com/cdr/).

## Configure ICAP Servers

From the OneFS Storage Administration WebUI, navigate to **Data Protection → Antivirus → ICAP Servers**

- Click **Add an ICAP server**.
- Check the **Enable ICAP server** checkbox.
- Enter the **ICAP server URL** (example: **icap://opswat-icap1.domain.corp:1344/OMSScanReq-AV** ).
- Enter a description for the ICAP server.
- Click **Add server**.
- Repeat as necessary for all ICAP servers.

## Enable the Antivirus scanning service

From the OneFS Storage Administration WebUI, navigate to **Data Protection → Antivirus → Settings**

- Check the **Enable antivirus service** checkbox.
- Select **Attempt to quarantine file when threat is found** from the **Action on detection** drop-down box.
- Configure the **Maximum file scan size** as desired. Note that scanning very large files may impact user experience as they will not be available until the scan completes.
- Configure **Path prefixes** as needed. These are the paths on the filesystem that will trigger a scan when files are added to them.
- If you would like to only scan certain file types, utilize the **Enable Filters** checkbox:

  - To scan all files **except for a file extension**, choose **Scan files not matching filters** and enter one or more filters in the box below.
  - To scan **only certain file extensions**, choose **Scan files matching filters** and enter one or more filters in the below box.
- Configure when to scan the files:

  - To scan files before they are able to be accessed by the user, check the **Enable scan of files on open** checkbox. To allow access to the file when scanning fails (not recommended), check the **Enable file access when scanning fails** checkbox.
  - To scan files as they are closed, check the **Enable scan of files on close** checkbox.
- Configure scan report retention.
- Click the **Save Changes** button.

## Review Detected Threats

To review information on threats that have been detected, navigate to **Data Protection → Antivirus → Detected Threats.**

- Files that have been quarantined will be listed here, along with the threat name, file path, remediation method, policy, and timestamp of the detected file.
- Click the **View details** button next to a threat to view detailed information.
- To release the file and allow it to be accessed by users, click the **More** drop-down box, and select **Release file**.

## Schedule scan of files

In addition to scanning files as they are opened or closed, OneFS can also scan files on a schedule (e.g. daily or weekly scan).

To configure a scheduled scan policy, navigate to **Data protection → Antivirus → Policies.**

## Configure scheduled scan:

- Click the **Create an antivirus policy**.
- Check the **Enable antivirus policy** checkbox.
- Give the policy a name in the **Policy name** box.
- Give a description of the policy in the **Description** box.
- Add directory paths in the **Paths** section (e.g. /ifs/home/ )
- If desired, set a limit on the recursion depth (e.g. how deep into the filesystem to traverse) in the **Recursion depth** section (not recommended).
- Select the impact policy settings:

  - If you wish to run the policy no matter the impact, check the **Enable force run of policy regardless of impact policy** checkbox (not recommended).
  - Select the impact policy from the **Impact Policy** drop-down box (DEFAULT).
- To configure the policy to run on a schedule, click the **Scheduled** radio button:

  - Choose the schedule interval (e.g. Daily, Weekly, Monthly, Yearly).
  - Configure the policy to run at the desired time.
- Click the **Create Policy** button to save.
