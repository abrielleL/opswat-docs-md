<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/admin-helper-tools -->

# Admin Helper Tools

This page provides executables that use API calls to help MetaDefender NAC administrators with tasks that might otherwise be tedious.

## [Mass Reauthenticate](/docs/manac/nac-v8.1.1/knowledge-base/admin-helper-tools#mass-reauthenticate)

**Description:** Forces re-authentication for an all devices in a particular Policy Group.

**Download Links:**

- [Windows](https://nac-downloads.opswat.com/admin-tools/mass-reauth.exe)
- [Linux](https://nac-downloads.opswat.com/admin-tools/mass-reauth)

**CLI arguments:**

- `-group` : Name of Policy Group to re-authenticate. Must match exactly including capitalization and whitespace. If the group name includes spaces and you are providing the name via command-line argument, be sure to wrap the name in quotes. No quotes are needed when providing the group name interactively.
- `-dry-run` : Show who would be forced to re-authenticate without actually doing it.
- `-reset-creds` : Not only force re-authentication, but also forget currently authenticated username for each device.
- `-skip-cert-validation` : Skip certificate validation when making API calls. Useful if you are using the `-url` argument with an IP address.
- `-only-active` : Only force currently-active clients to re-authenticate
- `-url` : Base URL to use in API calls. Defaults to "[https://portal.myweblogon.com:8443"](https://portal.myweblogon.com:8443%22).
- `-username` : Admin username used to authenticate API calls. (Password will be prompted interactively.)

**Additional Notes:**

The program can be executed without any arguments by simply double-clicking it. In that case you will be prompted to enter group name and admin username interactively (password is always prompted interactively). The base URL will be the default, `-dry-run` will be false, and `-reset-creds` will be false.

The password will not be displayed as you type it. Don't worry, this is expected.

**Troubleshooting Tips:**

- If the program reports zero clients in the given Policy Group, make sure you typed the group name correctly.
- If you get an error involving "401", make sure the admin username and password you provided are correct.

## [Clear Enrollments](/docs/manac/nac-v8.1.1/knowledge-base/admin-helper-tools#clear-enrollments)

**Description:** Deletes all device enrollments from the NAC virtual appliance

**Download Links:**

- [Windows](https://nac-downloads.opswat.com/admin-tools/clear-enrollments.exe)
- [Linux](https://nac-downloads.opswat.com/admin-tools/clear-enrollments)

**CLI arguments:**

- `-dry-run` : Perform a dry run without deleting anything. Shows what would be cleared without actually removing the enrollment records.
- `-url` : Base URL for the API calls. Defaults to "[https://portal.myweblogon.com:8443"](https://portal.myweblogon.com:8443%22).
- `-user` : Username for authentication used in API calls. (Password will be prompted interactively.)

**Additional Notes:**

The program can be executed without any arguments by simply double-clicking it. In that case you will be prompted to enter the username interactively (password is always prompted interactively). The base URL will be the default and `-dry-run` will be false.

The password will not be displayed as you type it. Don't worry, this is expected.

**Troubleshooting Tips:**

- If you get an error involving "401", make sure the username and password you provided are correct.
