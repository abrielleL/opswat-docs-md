<!-- source: https://www.opswat.com/docs/manac/knowledge-base/admin-helper-tools -->

# Admin Helper Tools

This page provides executables that use API calls to help MetaDefender NAC administrators with tasks that might otherwise be tedious.

## [Mass Reauthenticate](/docs/manac/knowledge-base/admin-helper-tools#mass-reauthenticate)

**Description:** Performs a bulk action — re-authenticate, expire, or purge — on all devices matching a Policy Group and/or authenticated username. By default it forces re-authentication.

**Download Links:**

- [Windows](https://nac-downloads.opswat.com/admin-tools/mass-reauth.exe)
- [Linux](https://nac-downloads.opswat.com/admin-tools/mass-reauth)

**CLI arguments:**

- `-action` : Action to perform on matching devices. One of:

  - `reauth` (default) — force re-authentication.
  - `expire` — expire the device's authentication.
  - `purge` — delete the device record entirely.
- `-group` : Name of Policy Group to act on. Must match exactly including capitalization and whitespace. If the group name includes spaces and you are providing the name via command-line argument, be sure to wrap the name in quotes. No quotes are needed when providing the group name interactively.
- `-user` : Only act on devices whose authenticated username matches this value (case-insensitive, exact match). Can be combined with `-group` to scope to one user within a group, or used on its own to act on a user across all groups. A `-group`, a `-user`, or both must be provided.
- `-dry-run` : Show which devices would be acted on without actually doing it.
- `-reset-creds` : Not only force re-authentication, but also forget the currently authenticated username for each device. Only applies to the `reauth` action.
- `-skip-cert-validation` : Skip certificate validation when making API calls. Useful if you are using the `-url` argument with an IP address.
- `-only-active` : Only act on currently-active clients.
- `-url` : Base URL to use in API calls. Defaults to "[https://portal.myweblogon.com:8443"](https://portal.myweblogon.com:8443%22).
- `-username` : Admin username used to authenticate API calls. (Password will be prompted interactively.)

**Additional Notes:**

The program can be executed without any arguments by simply double-clicking it. In that case you will be prompted to enter the admin username and, separately, the Policy Group and/or target username to act on (password is always prompted interactively). You may leave either the group or the target username blank, but you must provide at least one — the program will re-prompt until you do. The base URL will be the default, the action will be `reauth`, and `-dry-run` and `-reset-creds` will be false.

Before any action is performed you will see the list of matching devices and be asked to confirm by typing `yes`. The `expire` and `purge` actions are destructive — `purge` deletes the device record outright — so review the list carefully, and consider running with `-dry-run` first.

The password will not be displayed as you type it. Don't worry, this is expected.

**Troubleshooting Tips:**

- If the program reports zero matching devices, make sure you typed the group name and/or username correctly (the group name must match exactly).
- If you get an error involving "401", make sure the admin username and password you provided are correct.

## [Clear Enrollments](/docs/manac/knowledge-base/admin-helper-tools#clear-enrollments)

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
