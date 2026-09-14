<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security -->

# How to disable SMB1 and enforce SMB3 for enhanced security

## [Purpose](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#purpose)

The purpose of this document is to provide guidance on disabling SMB1 on the client side (Kiosk) and enforcing secure communication using SMB3 only.

## [Why disable SMB1?](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#why-disable-smb1)

SMB1 is an outdated protocol with known vulnerabilities that can expose systems to attacks such as ransomware. Disabling SMB1 significantly reduces the attack surface.

Run the following PowerShell command with administrative privileges to disable SMB1 protocol at the client side (Kiosk)

`Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`

This command will remove the SMB1 client component from the device (Kiosk)

## [Why can't we disable SMB2 independently?](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#why-cant-we-disable-smb2-independently)

SMB2 and SMB3 share the same protocol stack in Windows. Disabling SMB2 alone is not possible because doing so would also disable SMB3 and impacting SMB3 functionality.

## [How to enforce SMB3 connections only](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#how-to-enforce-smb3-connections-only)

If you want to ensure that only SMB3 protocol is used for the connections. There are two approaches

#### [Approach 1: Enforce from the SMB server side](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#approach-1-enforce-from-the-smb-server-side)

On the SMB server, run the following PowerShell commands with administrative privileges to disable SMB1 protocol at the server side:

`Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protoc`

`Set-SmbServerConfiguration -EnableSMB2Protocol $false`

When SMB1 and SMB2 are disabled on the server, only SMB3 connections are allowed. Clients (Kiosk) that support SMB3 will successfully negotiate and connect using the secure protocol. However, any clients (Kiosk) that only support SMB1 or SMB2 will fail to connect.

#### [Approach 2: Enforce from the client side](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-disable-smb1-and-enforce-smb3-for-enhanced-security#approach-2-enforce-from-the-client-side)

On the SMB client (Kiosk), run the following PowerShell commands with administrative privileges to enforce allowing encrypted connection only

`Set-SmbClientConfiguration -RequireEncryption $true`

When encryption is required on the SMB client (Kiosk), SMB2 will never be used because it does not support encryption. If the server supports SMB3, the client (Kiosk) will successfully negotiate an encrypted SMB3 connection. However, if the server only supports SMB2, the connection will fail.

Enforce encrypted connection only is not supported in Kiosk Hardened Image

The command mentioned in approach 2 to enforce using encrypted connections only is not supported in Kiosk Hardened Image which is running Windows 10 IoT Enterprise LTSC
