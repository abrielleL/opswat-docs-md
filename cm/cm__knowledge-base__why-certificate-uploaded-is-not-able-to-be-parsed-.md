<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-certificate-uploaded-is-not-able-to-be-parsed- -->

# Why certificate uploaded is not able to be parsed?

> ## **Check your version**
>
> This article applies to all OPSWAT MetaDefender Central Management version 10.x deployed on Linux or Windows systems.

## **Symptoms**

When trying to add an SSL certificate or private key in PEM format to CM10, the upload fails with the following error

![](https://uploads.developerhub.io/prod/97qW/c546na20x1ydn8gb06b3qf8xsg6twz0k06m24h77dl579aurob6jepm1rtjonp7x.png)

This indicates that CM10 was not able to parse the PEM file or files.

And the end of the certificate or key looks like the following:

### **Certificate:**

![](https://uploads.developerhub.io/prod/97qW/7p126yjx6pfxq5mpu0v3xr4c3jj937y0mt4rqg87y6h66vszrssonbk7goquwmo6.png)

Example of a Certificate in PEM formart creatred by OpenSSL

### **Key:**

![](https://uploads.developerhub.io/prod/97qW/2cwfb97m7ddattv0lota6nlq7csncsx5sorms7by43zgng2dl7o6ni6kczjnfo2v.png)

Example of a Key in PEM formart creatred by OpenSSL

 

## **Root cause**

The CM10 certificate parser expects PEM files to end with a terminating newline character after the
 `-----END CERTIFICATE----- ` or `----END PRIVATE KEY -----`boundaries. While RFC 7468 does not strictly mandate a trailing newline, the CM10 parser requires one in order to correctly process the file.

Certificates exported from some tools commonly omit this trailing newline, including:

- Windows certmgr exports
- Certain OpenSSL one-liner exports
- Copy-paste from a browser or text field

## **Resolution**

Add a newline at the end of the PEM file, after the `-----END CERTIFICATE----- ` or ` ----END PRIVATE KEY -----`boundaries. boundary. The file should look like this:

![](https://uploads.developerhub.io/prod/97qW/1n7iothnt4jh48s3c9aftjmdwb1awic986qlh3mjq2z5egxn4li3i44kvd75avqy.png)

![](https://uploads.developerhub.io/prod/97qW/w5h458ks9bu2fmtw8uufut3ik4y4nym32oj2nlyxhxski1x3czvl2xkxl3ba9zlx.png)

### **Adding the newline**

**Linux / macOS:**

```plaintext
echo "" >> cert.pem
or
echo "" >> key.pem
```

**Windows PowerShell:**

```plaintext
Add-Content -Path cert.pem -Value ""
Add-Content -Path key.pem -Value ""
```

**Manually:** Open the file in a text editor that shows line endings (Notepad++, VS Code, vim) and press Enter after the final `-----END CERTIFICATE-----` or `-----END CERTIFICATE----- ` line so the cursor moves to a new empty line.

### **Verifying the fix**

Before re-uploading, confirm the file ends with a newline character (`LF` or `CRLF`):

**Linux / macOS:**

```plaintext
tail -c 1 cert.pem | xxd
tail -c 1 key.pem | xxd
```

Expected output ends in `0a` (LF) or `0d 0a` (CRLF).

**Windows PowerShell:**

```plaintext
(Get-Content cert.pem -Raw)[-1]
(Get-Content key.pem -Raw)[-1]
```

Expected output is a newline character.

After verification, retry the upload to CM10 via the Management Console.

## **Support**

> If you need further assistance, please contact OPSWAT Support through the [OPSWAT Portal](https://my.opswat.com/) or your assigned support representative.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
