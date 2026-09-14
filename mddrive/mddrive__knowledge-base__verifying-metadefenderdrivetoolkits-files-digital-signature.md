<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature -->

# Verifying MetaDefenderDriveToolkit's files Digital Signature

#### [Overview:](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#overview)

When you receive files from OPSWAT, you need to be sure they are genuine and haven’t been tampered with. This guide shows you how to independently verify OPSWAT-delivered files using detached digital signatures on Linux, macOS, and Windows.

By following the steps below, you can:

- Confirm that your files were really produced by OPSWAT
- Detect any modification or corruption during transfer or storage
- Integrate a repeatable, automated verification step into your own processes

Detached digital signatures provide a cryptographic way to validate both **integrity** (no changes) and **authenticity** (signed by a trusted OPSWAT key).

#### [What You Need:](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#what-you-need)

To verify OPSWAT files, you’ll need:

- **Original files** For example: MetaDefenderDriveToolkit.zip
- **Detached signature files** Base64-encoded signature files matching the originals, for example: MetaDefenderDriveToolkit.zip.dig.signed
- **OPSWAT certificate file** A certificate file that contains the public key used for verification, for example: cert.crt (You can request this certificate file from OPSWAT.)

With these three components in the same folder, you can fully validate that the files you received are authentic and unaltered.

### [Prerequisites](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#prerequisites)

The verification process uses OpenSSL and simple platform-native scripting. Below are the minimal requirements for each platform.

#### [Linux](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#linux)

- Bash shell
- OpenSSL installed and available on your PATH

#### [macOS](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#macos)

- Bash shell (included by default)
- OpenSSL (install via Homebrew if needed: brew install openssl)

#### [Windows](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#windows)

- PowerShell
- OpenSSL installed, for example:

  - Via Chocolatey: choco install openssl
  - Or via Git for Windows / official OpenSSL packages

Once these are installed, you’re ready to use the reference scripts below.

### [Reference Implementations](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#reference-implementations)

Our ready-to-run scripts for Linux, macOS, and Windows make verification fast and effortless—so you always know your downloads are genuine and tamper-free. Each script automatically:

- Extracts the public key from the OPSWAT certificate
- Finds all detached signature files (*.dig.signed)
- Matches them with their original files
- Decodes and verifies each signature using OpenSSL (SHA‑256)
- Prints a clear summary showing which files are valid (OK), failed (FAIL), or skipped (SKIP)

Choose your platform, run the script, and get instant, trustworthy results. These reference scripts make it effortless to confirm your OPSWAT-delivered files are authentic and untouched—no guesswork, just clear pass/fail output you can rely on.

#### [Linux / macOS (Bash Script)](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#linux--macos-bash-script)

BashCopy#!/usr/bin/env bash
set -euo pipefail
CERT_FILE="cert.crt"
PUBKEY_FILE="pubkey.pem"
if [[ ! -f "$CERT_FILE" ]]; then
echo "ERROR: Certificate not found: $CERT_FILE" >&2
exit 1
fi
# Extract public key from certificate
openssl x509 -in "$CERT_FILE" -pubkey -noout > "$PUBKEY_FILE"
shopt -s nullglob
tmpdir="$(mktemp -d)"
trap 'rm -rf "$tmpdir"' EXIT
fail=0
verified=0
skipped=0
found=0
for sig_b64 in *.dig.signed; do
found=1
file="${sig_b64%.dig.signed}"
if [[ ! -f "$file" ]]; then
echo "SKIP: $sig_b64 (missing original file: $file)"
((skipped++)) || true
continue
fi
sig_bin="$tmpdir/$(basename "$sig_b64").bin"
# Decode Base64 signature to raw binary
openssl base64 -d -A -in "$sig_b64" -out "$sig_bin"
echo "VERIFY: file=$file sig=$sig_b64"
# Verify signature
if openssl dgst -sha256 -verify "$PUBKEY_FILE" -signature "$sig_bin" "$file" >/dev/null; then
echo "OK: $file"
((verified++)) || true
else
echo "FAIL: $file" >&2
fail=1
fi
echo
done
if [[ "$found" -eq 0 ]]; then
echo "WARN: No *.dig.signed files found in $(pwd)"
fi
echo "Summary: verified=$verified skipped=$skipped"
[[ "$fail" -eq 0 ]]
#### [Windows (PowerShell Script)](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#windows-powershell-script)

PowershellCopy# Requires: OpenSSL installed and available in PATH
# Usage: .\validate.ps1 -CertFile "cert.crt"
param(
[string]$CertFile = "cert.crt"
)
$PubKeyFile = "pubkey.pem"
if (!(Test-Path $CertFile)) {
Write-Error "Certificate not found: $CertFile"
exit 1
}
# Extract public key from certificate
& openssl x509 -in $CertFile -pubkey -out $PubKeyFile
$fail = 0
$verified = 0
$skipped = 0
$found = 0
Get-ChildItem -Filter *.dig.signed | ForEach-Object {
$found = 1
$sig_b64 = $_.Name
$file = $sig_b64 -replace '\.dig\.signed$', ''
if (!(Test-Path $file)) {
Write-Host "SKIP: $sig_b64 (missing original file: $file)"
$skipped++
return
}
$sig_bin = "$($sig_b64).bin"
& openssl base64 -d -A -in $sig_b64 -out $sig_bin
Write-Host "VERIFY: file=$file sig=$sig_b64"
$result = & openssl dgst -sha256 -verify $PubKeyFile -signature $sig_bin $file
if ($LASTEXITCODE -eq 0) {
Write-Host "OK: $file"
$verified++
} else {
Write-Host "FAIL: $file"
$fail = 1
}
Remove-Item $sig_bin
}
if ($found -eq 0) {
Write-Host "WARN: No *.dig.signed files found in $(Get-Location)"
}
Write-Host "Summary: verified=$verified skipped=$skipped"
exit $fail
#### [Usage Instructions](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#usage-instructions)

1. Place the original files, signature files, and certificate in the same directory.
2. Save the script into **validate.ps1** (Windows) **or validate.sh** (Linux/macOS), place it into the same directory as your files, then run the appropriate script for your platform. For example:

   1. Windows: .\validate.ps1
   2. Linux/macOS: Add permission for the script with chmod +x ./validate.sh, then run it with ./validate.sh
   3. Note: if you want to change the file name of the certificate, you need to
3. Review the output for OK, FAIL, and SKIP messages.

   1. OK: File is signed with OPSWAT certificate.
   2. FAIL: **Fail to verify with OPSWAT certificate.**
   3. SKIP: The original file not found.

**For example, o**n Windows platform

PowershellCopyPS C:\Workspace\DS-workspace> dir
Directory: C:\Workspace\DS-workspace
Mode LastWriteTime Length Name
---- ------------- ------ ----
-a---- 18/03/2026 14:40 1174 cert.crt
-a---- 12/03/2026 15:13 149611480 MetaDefenderDriveToolkit.zip
-a---- 18/03/2026 13:50 344 MetaDefenderDriveToolkit.zip.dig.signed
-a---- 19/03/2026 17:49 1310 validate.ps1
PS C:\Workspace\DS-workspace> .\validate.ps1
VERIFY: file=MetaDefenderDriveToolkit.zip sig=MetaDefenderDriveToolkit.zip.dig.signed
OK: MetaDefenderDriveToolkit.zip
Summary: verified=1 skipped=0
PS C:\Workspace\DS-workspace>

**The folder contains:**

- MetaDefenderDriveToolkit.zip
- MetaDefenderDriveToolkit.zip.dig.signed
- cert.crt
- validate.ps1

**Output explanation:**

- VERIFY: file=MetaDefenderDriveToolkit.zip sig=MetaDefenderDriveToolkit.zip.dig.signed Verify the MetaDefenderDriveToolkit.zip file with detached signature MetaDefenderDriveToolkit.zip.dig.signed
- OK: MetaDefenderDriveToolkit.zip Verification is OK
- Summary: verified=1 skipped=0 One file is verified

---

#### [Troubleshooting & Security Considerations](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#troubleshooting--security-considerations)

- **Common failure causes:**

  - Wrong certificate used for verification
  - Missing or mismatched original files
  - Corrupted or truncated signature files
  - Algorithm mismatch (ensure SHA-256 is used)
- **Best practices:**

  - Treat the certificate as a trust anchor; validate its source.
  - Keep OpenSSL and your OS up to date.
  - Automate signature verification in your build or deployment process.
  - Never bypass verification failures.

### [Summary](/docs/mddrive/knowledge-base/verifying-metadefenderdrivetoolkits-files-digital-signature#summary)

This guide enables you to independently verify detached digital signatures on Linux, macOS, or Windows using OpenSSL and platform-appropriate scripting. This ensures your files are authentic and unaltered, regardless of your environment.
