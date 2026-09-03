<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/the-command-line-options -->

# The command line options

This document provides essential command line options for installing and uninstalling the MetaDefender Endpoint Validation product.

## Install

The product can be installed via the command line interface by executing the following command

```powershell
msiexec /i /qn <msi file path>
```

## Uninstall

The product can be uninstalled via the command line interface by executing the following command

```powershell
msiexec /x /qn <msi file path/product code> PASSWORD=<admin_password> <option key>=<option value>
```

Presented below are the prospective keys along with their corresponding values:

| Key | Value | Require | Description |
| ---- | ---- | ---- | ---- |
| PASSWORD | <admin_password> | yes | The admin password |
| KEEPHIDDATA | 0/1 | no | Allow users to retain or delete HID information; do not retain HID data if the option is not used. |

## Notes

- The **/qn** option in the command line indicates that the action will be performed silently, without any user interface prompts.
- Following the command to get the product code:

```powershell
Get-WmiObject Win32_Product | Where-Object { $_.Name -eq 'MetaDefender Endpoint Validation' } | Select-Object -ExpandProperty IdentifyingNumber
```
