<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-to-add-usbs-to-allowlist-to-skip-media-scanning- -->

# How to add USBs to Allowlist to skip Media Scanning?

Allowlist provides the option to exclude certain specific USBs or specific vendor USB from being scanned by the OPSWAT Applications. This option is available for Regular USBs and Encrypted USBs.

**Prerequisites: Gather USB Device Details**

Use a system utility (e.g., Device Manager on Windows) or a USB tool to retrieve the following:

- **Vendor name**
- **Product ID**
- **Instance Path**

Here’s an example of gathering the information from Windows:

**Access the OPSWAT IT Access Management Console**

- Log in to your OPSWAT IT Access management console.
- Navigate to the policy configuration section where file scanning rules are defined.
- Navigate to Advanced Endpoint Protection and select Enable Removable Media Protection.
- Activate **Allowlist** and add any of the three gathered items from the previous step by simply entering the information and pressing Enter when done. (Multiple different instances can be added.)

**Note**: you also have a time setting for when this **Allowlist** is enabled. You can either leave it in the default state of **any time** (which is 24/7) or **specific time** which let’s you have this rule active for a limited, specific timeframe:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
