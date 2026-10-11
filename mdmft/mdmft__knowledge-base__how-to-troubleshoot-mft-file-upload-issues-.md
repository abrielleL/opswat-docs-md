<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues- -->

# How to Troubleshoot MFT File Upload Issues?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Check Your Version:**

This article applies to all MFT releases deployed on Windows and Linux systems.

## [**Overview**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#overview)

This article provides a concise troubleshooting guide for upload issues in OPSWAT MFT. Upload failures are commonly caused by file-specific restrictions, WAF or firewall blocks, proxy or load balancer limits, DNS/FQDN routing differences, or MFT service and storage issues.

## [**Top Potential Breaking Points and Solutions**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#top-potential-breaking-points-and-solutions)

### [**File-Specific Restrictions**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#file-specific-restrictions)

Upload failures may be caused by the file itself, especially when only one file, file type, or file size is affected.

**Common causes:**

- The file size exceeds the configured limit.
- The file extension, MIME type, or content is blocked.
- The file name contains unsupported characters or is too long.
- The file is corrupted, encrypted, or password-protected.

**Solution:**

Test with:

- A small `.txt` or `.pdf` file.
- A different file with the same extension.
- A file with a similar size.
- The same file after renaming it.
- The same file from another workstation or network.

| Test Result | Likely Cause |
| --- | --- |
| Small files work, large files fail | Size limit or timeout |
| Only one file fails | File-specific block or corruption |
| Same extension always fails | File type or MIME restriction |
| Renamed file works | File name or pattern-based rule |

---

### [**WAF, Firewall, Proxy, DNS, or Routing Issues**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#waf-firewall-proxy-dns-or-routing-issues)

A WAF, firewall, proxy, load balancer, secure gateway, or DNS/FQDN routing path may block, redirect, or interrupt the upload before it reaches MFT.

This is especially likely when uploads fail through the public FQDN but work through a direct IP address, internal path, or local server test.

**Common causes:**

- Request body or upload size limits.
- Blocked file type, extension, MIME type, or content.
- Malware, DLP, WAF, or TLS inspection.
- Multipart/form-data inspection issues.
- Timeout, connection reset, rate limit, or false positive security rule.
- DNS resolving to an unexpected WAF, proxy, or load balancer path.
- Certificate, SNI, or host header mismatch.

##### [**Important**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#important)

If the upload request does not appear in MFT logs, it may have been blocked before reaching MFT. In that case, review the WAF, firewall, proxy, gateway, or load balancer logs for the failed upload timestamp.

**Solution:**

Check external security or routing logs for:

- Client source IP address and MFT destination.
- HTTP `POST` or multipart upload requests.
- Blocked file type, MIME type, or content.
- Size limits, timeouts, resets, or inspection failures.
- HTTP `403`, `413`, `415`, `429`, `502`, or `504` responses.

Test the MFT FQDN:

nslookup mft.example.com
curl -vk https://mft.example.com

Test direct IP access, if allowed:

curl -vk https://<MFT_IP_ADDRESS>

If the application requires the FQDN host header:

curl -vk https://<MFT_IP_ADDRESS> -H "Host: mft.example.com"

| Test Result | Likely Cause |
| --- | --- |
| FQDN fails, IP works | DNS, WAF, proxy, or load balancer issue |
| FQDN works, IP fails | Host header, certificate, or direct IP restriction |
| Both fail | Service, firewall, or network issue |
| Page loads but upload fails | Upload size, timeout, or inspection issue |

**Recommended actions:**

- Allow legitimate authenticated MFT upload traffic.
- Increase upload size and timeout limits where appropriate.
- Allow required file types and MIME types.
- Confirm that the FQDN resolves to the expected destination.
- Review certificate, SNI, and host header behavior.
- Add a focused WAF or proxy exception for the MFT upload path if needed.

---

### [**MFT Service, Server, or Storage Issues**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#mft-service-server-or-storage-issues)

If the upload reaches MFT but still fails, the issue may be on the MFT server or storage layer.

**Common causes:**

- MFT service or application errors.
- Low disk space or an unavailable temporary upload directory.
- Unavailable destination storage.
- The service account lacks write permissions.
- Storage quota, antivirus, or EDR interference.

**Solution:**

Check the following:

- MFT services are running.
- Users can log in and upload a small test file.
- MFT application and system logs are reviewed.
- Disk space and the temporary upload path are available.
- Destination storage and permissions are configured correctly.
- Antivirus or EDR activity on the MFT server is not interfering.

---

### [**External Path Versus Local MFT Server Upload**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#external-path-versus-local-mft-server-upload)

This is the key isolation test.

If a file fails through the normal user access path, test the same file directly from the MFT server to determine whether MFT can process it without external network or security components.

##### [**Key Isolation Test**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#key-isolation-test)

Copy the failed file to the MFT server and upload it through the MFT UI using localhost, 127.0.0.1, or the server IP address. If this succeeds, MFT is likely functioning correctly, and the issue is most likely external to MFT.

**Solution:**

From the MFT server, open the MFT UI using one of the following:

`https://localhost:8010`

`https://127.0.0.1:8010`

`https://<MFT_SERVER_IP_ADDRESS>:8010`

If required, also test with the FQDN:

`https://mft.example.com`

Then upload the same file through the UI.

| Test Result | Meaning |
| --- | --- |
| Upload succeeds locally but fails externally | Likely WAF, firewall, proxy, load balancer, DNS, or routing issue |
| Upload fails locally and externally | Likely MFT, file, storage, permission, or server issue |
| Localhost/IP works but FQDN fails | FQDN path may route through external security or load balancing |
| Only that file fails | File-specific issue or security inspection block |

---

## [**Summary**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#summary)

Most MFT upload issues are caused by:

- File-specific restrictions.
- WAF, firewall, proxy, DNS, or routing issues.
- Upload size or timeout limits.
- MFT service, storage, or permission issues.

## [**Key Takeaway**](/docs/mdmft/knowledge-base/how-to-troubleshoot-mft-file-upload-issues-#key-takeaway)

The key isolation test is to upload the same failed file directly from the MFT server using localhost or the server IP address. If that succeeds, MFT is likely functioning correctly, and the issue is most likely external to MFT.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
