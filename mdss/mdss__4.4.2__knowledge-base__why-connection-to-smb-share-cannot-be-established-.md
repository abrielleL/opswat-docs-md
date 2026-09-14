<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/why-connection-to-smb-share-cannot-be-established- -->

# Why connection to SMB share cannot be established?

This article applies to all MetaDefender Storage Security versions.

## [Issue:](/docs/mdss/4.4.2/knowledge-base/why-connection-to-smb-share-cannot-be-established-#issue)

MetaDefender Storage Security connection with SMB fails with error:

`smbprotocol.exceptions.SMBOSError: [Error 0] [NtStatus 0xc00000c9] Unknown NtStatus error returned 'STATUS_NETWORK_NAME_DELETED': '\\{IP_HOSTNAME}ftp\CN`

## [Description](/docs/mdss/4.4.2/knowledge-base/why-connection-to-smb-share-cannot-be-established-#description)

- `NtStatus 0xc00000c9` corresponds to `STATUS_NETWORK_NAME_DELETED`.
- This error typically occurs when the network share or resource you are trying to access has been removed, deleted, or is temporarily unavailable.
- It can also happen if the SMB session has become stale (e.g., the server closed the connection due to timeout, network issues, or a manual server-side operation).

## [Possible Causes:](/docs/mdss/4.4.2/knowledge-base/why-connection-to-smb-share-cannot-be-established-#possible-causes)

- The network share `\\[IP_HOSTNAME]\ftp\CN` was deleted or unshared on the server. The SMB server might be up but the whole path might be unshared.
- The server at `[IP_HOSTNAME]` rebooted, crashed, or restarted its SMB service.
- There is a network connectivity issue between our SMB service and customer’s SMB server.
- Permissions on the share changed, making it inaccessible.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
