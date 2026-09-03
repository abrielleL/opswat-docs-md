<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/why-i-am-getting-error--no-available-rule-is-present-for-scannin -->

# Why I am getting error "No available rule is present for scanning"

When triggering a scan, you may encounter a scan failure with the following error message:

Error

opswat.mdcs.scanning.ScanFailedException: InitiateScanCommandHandler: Scan request for object failed. StatusCode: InternalServerError Error: No available rule is present for scanning.

## Cause

This error typically occurs when the workflow name configured in MetaDefender for Secure Storage (MDSS) does not match the workflow name set in MetaDefender Core.

MetaDefender Storage Security

MetaDefender Core

## Steps to Resolve:

1. **Log into MetaDefender Core**

   - Navigate to Workflows.
   - Identify the workflow associated with MDSS.
   - The workflow name should be either: "MetaDefender Storage Security" or "MetaDefender for Secure Storage"
2. **Verify and Update the Workflow in MDSS**

   - If the workflow name in Core is "MetaDefender Storage Security", log into MDSS Configuration.
   - Go to **Workflows** and click on your workflow

- Edit the scan configuration and update the rule name to "MetaDefender Storage Security".

- Ensure the workflow name exactly matches the one in Core.

3. **Apply Changes and Restart the Service**

- Click “Save” to save the configuration.
- Restart the scanning service if necessary and retry the scan to verify if the issue is resolved.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
