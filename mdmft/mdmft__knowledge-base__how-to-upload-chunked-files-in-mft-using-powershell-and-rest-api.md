<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api -->

# How to upload chunked files in MFT using Powershell and REST API

Summarize Page    Connect to Cursor Connect to VS Code
## [Overview](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#overview)

This article explains how to upload files to OPSWAT MetaDefender Managed File Transfer using PowerShell and the **REST API** with **chunked upload**.

It covers:

- Authentication
- Transfer group creation
- File initialization
- Chunked upload
- Transfer finalization

---

## [✅ Prerequisites](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-prerequisites)

- Access to MetaDefender MFT API endpoint
- Valid username and password
- PowerShell 5.1+ or PowerShell 7+
- Network access to:

https://<mft-server>:8010/vault_rest

---

## [📂 File Preparation](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-file-preparation)

Ensure the file exists locally:

$upload_file = "C:\Path\To\file.zip"

---

## [🔐 Credentials File Format](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-credentials-file-format)

Create a file named:

$password2.txt

With content:

username=myuser
password=mypass

---

## [🔄 Workflow Summary](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-workflow-summary)

The upload process follows this sequence:

1. Authenticate → token
2. Create transfer group → `group_id`
3. Initialize file → `file_id`
4. Upload file in chunks
5. Close file transfer
6. Close group transfer

---

## [💻 PowerShell Script](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-powershell-script)

*(Place your cleaned-up version here — remove debug clutter and fix issues before publishing)*

👉 Important: Include only:

- final working version
- comments explaining each step

---

## [⚙️ Key Configuration Parameters](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-key-configuration-parameters)

| Parameter | Description |
| --- | --- |
| `$baseUrl` | API base endpoint |
| `$buf_size` | Chunk size (default: 10MB) |
| `transfer_method` | Stream or Chunk |
| `chunk_offset` | Byte position for each chunk |

---

## [📦 Chunk Upload Logic Explained](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-chunk-upload-logic-explained)

- File is read in fixed-size buffers
- Each chunk is sent with:

  - `file_id`
  - `group_id`
  - `chunk_offset`
- Offset increases after each upload

This prevents:

- Memory issues
- File corruption
- Large upload failures

---

## [✅ Validation](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-validation)

After execution, you should see:

Authenticated. Token: <token>
Group ID: <id>
File ID: <id>
Chunk upload completed successfully
File transfer closed: Success
Group transfer closed: Success

---

## [❗ Troubleshooting](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-troubleshooting)

### [🔴 Authentication fails](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-authentication-fails)

- Verify credentials format
- Confirm encoding method (CRLF vs `username:password`)

---

### [🔴 File transfer fails on close](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-file-transfer-fails-on-close)

- Check `file_checksum`
- Ensure hash matches server expectation:

Get-FileHash -Algorithm SHA256

---

### [🔴 Chunk upload errors](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-chunk-upload-errors)

- Verify:

  - `chunk_offset` correctness
  - chunk size (try reducing to 4MB)
- Check network stability

---

### [🔴 File corruption](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-file-corruption)

Ensure buffer is trimmed:

$body = New-Object byte[] $bytes_read
[Array]::Copy($buffer, 0, $body, 0, $bytes_read)

---

## [🔐 Security Considerations](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-security-considerations)

- Do not store plaintext passwords in production
- Use:

  - Windows Credential Manager
  - Secure vault solutions
- Always use HTTPS

---

## [🚀 Best Practices](/docs/mdmft/knowledge-base/how-to-upload-chunked-files-in-mft-using-powershell-and-rest-api#-best-practices)

- Use retry logic for chunk uploads
- Log all API responses
- Validate checksum after upload
- Tune chunk size based on network

Download: [MFT-chunkupload](https://kb-hosting-cs.s3.us-east-1.amazonaws.com/KB/Vault/MFT-chunkupload.ps1)

> **Support**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

>
