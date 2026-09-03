<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry- -->

# How to create a playbook to check for a Windows Registry?

This article applies to all MetaDefender Endpoint releases deployed on Windows MetaAccess IT Access

Playbook checks whether a Windows Registry Key and Value Exists

If TRUE, mark the device as Compliant

If FALSE, mark the device as Non-Compliant

## [Outline](/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry-#outline)

## [Registry](/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry-#registry)

We are checking if the “global” key exists, with the value/string “restport”

## [Task](/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry-#task)

Registry key: HKEY_LOCAL_ MACHINE\SOFTWARE\OPSWAT\Metascan\global

Warning:

We are removing the Computer\ from the path

## [Conditional Node](/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry-#conditional-node)

## [Actions](/docs/macloud-sdp/kb/how-to-create-a-playbook-to-check-for-a-windows-registry-#actions)

Left: Returns compliant if the registry exists

Right: Returns non-compliant if the registry does not exist

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
