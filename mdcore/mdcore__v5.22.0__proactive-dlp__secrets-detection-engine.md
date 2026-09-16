<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/proactive-dlp/secrets-detection-engine -->

# Secrets Detection

Nowadays, it is very common for people to commit secrets into repositories or even to store them in code by accident. There are many types of secrets, including keys, passwords, API tokens, and other sensitive information. If anyone had access to these secrets, they could use them maliciously. When secrets are exposed to the public, they are compromised and have to be replaced, which can be very expensive. The Proactive DLP now has the ability to help prevent secrets from being exposed. Using the Secret Detection feature, you will be able to scan your files for secrets they might contain.

## [Supported file types](/docs/mdcore/v5.22.0/proactive-dlp/secrets-detection-engine#supported-file-types)

- Text based files, e.g: source code, configuration files.

## [Supported Secrets](/docs/mdcore/v5.22.0/proactive-dlp/secrets-detection-engine#supported-secrets)

- Amazon Web Services (AWS)

  - AWS Access Key ID
  - AWS Secret Access Key
  - AWS Temporary Access Key ID
  - AWS Session Token
  - AWS STS Token
- Microsoft Azure

  - Azure SAS Signature
  - Azure Access Key
  - Azure Access Token
  - Azure Tenant ID
  - Azure Client ID
  - Azure Client Secret
  - Azure Username
  - Azure Password
- Google Cloud Platform (GCP)

  - Google Cloud Api Key
  - Google Cloud Key *(We search for the base64 encoded version of the key as well)*
  - Google OAuth Client ID *(We search for reversed client ID as well)*
  - Google OAuth Client Secret
- Private keys (PEM, PPK)
- IBM keys

  - IBM Cloud key
  - IBM COS HMAC Credentials
  - IBM API Connect Credentials
- Generic passwords
- Generic API tokens
- PostgreSQL credentials
- MYSQL credentials

## [Enabling Secret Detection](/docs/mdcore/v5.22.0/proactive-dlp/secrets-detection-engine#enabling-secret-detection)

Policies > Workflow rules > Workflow name > Proactive DLP > Detect secret

## [Example](/docs/mdcore/v5.22.0/proactive-dlp/secrets-detection-engine#example)

Info

The following examples do not represent actual secrets.

| Example |  |
| --- | --- |
| 'AWS_ACCESS_KEY_ID' = 'AKIAIOSFODNN7EXAMPLE' | **Amazon Web Services** |
| 'aws_secret_ access_key' = 'wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY' |  |
| 'AWS Temporary Access Key ID' = 'ASIAIOSFODNN7EXAMPLE' |  |
| 'AWS Session Token' = 'FQoGZXIvYXdzEF8aD0YjK34RwRy8tSJEXAMPLEFa3fLgDzZrW2Z8t9Z9Yg4MupJys4I+2 H4ZDQDbTdEXAMPLES5N5OesDL5x5j5fiUqhEXAMPLEJUu1QuyK0CvLIn6JFV7lEXAMPLE' |  |
| 'Azure SAS Signature' = '?sv=2020-08-04&ss=bfqt&srt=sco&sp=rwdlacupx&se=2023-05-01T22%3A17%3A16Z&st=2023-04-24T14%3A17%3A16Z&spr=https&sig=FictionalSignature%3D' | **Microsoft Azure** |
| 'Azure Access Key' = 'Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsu Fq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==' |  |
| 'Azure Access Token' = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1u Q19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVG ZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbn QuY29yZS53aW5kb3dzLm5ldC8iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3d zLm5ldC8wMTIzNDU2Nzg5L2I4YmY0M2YtNmVlOC00ZmUxLWEzOTEtMGRiOG I1ZDM3Y2Y2LyIsImlhdCI6MTU5Mzg5OTQ2NCwibmJmIjoxNTkzODk5NDY0LCJl eHAiOjE1OTM5MDMzNjQsImFjciI6IjEiLCJhaW8iOiJBU1FBRG8vOEhBQUFBQVFB Q2dIY0FBQUY1YmVyM0l1dCIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI5OTljZDI2M C0zZjVhLTQ1NzctYmEwZC0xMjg2MmFmMjMxODgiLCJhcHBpZGFjciI6IjAiLCJmY W1pbHlfbmFtZSI6IkJyb3duIiwgImdpdmVuX25hbWUiOiJKb2huIiwiaXBhZGRyIjoiMT IzLjQ1LjY3Ljg5IiwibmFtZSI6IkpvaG4gQnJvd24iLCJvaWQiOiI5Zjg4ZWI4YS0yYmUyLT Q5ZmEtOTk5My1kYjg4YzUyZTAzZTgiLCJwdWlkIjoiMTAwMzAwMDA4Rjg4RUI4QSIsI nNjcCI6InVzZXJfaW1wZXJzb25hdGlvbiIsInN1YiI6ImtmcGZ2eWJrVG9QZ1MzVzF0dW x0VzJYUkNkVzlpWU0zR1RtM0RtWWp0VlEiLCJ0aWQiOiIwMTIzNDU2Nzg5L2I4YmY 0M2YtNmVlOC00ZmUxLWEzOTEtMGRiOGI1ZDM3Y2Y2IiwidW5pcXVlX25hbWUiOi Jqb2huLmJyb3duQGV4YW1' |  |
| 'Azure Tenant ID' = '12345678-9abc-def0-1234-56789abcdef0' |  |
| 'Azure Client ID' = 'a1b2c3d4-e5f6-1234-5678-90abcdef1234' |  |
| 'Azure Client Secret' = 'P@ssw0rd!a1b2c3d4e5f6g7h8i9j0k!l@Mn0' |  |
| 'Azure Username' = 'john.doe@example.com' |  |
| 'Azure Password' = 'Azure$tr0ngP@ssw0rd123!' |  |
| 'Google Cloud API Key' = 'AIzaSyDc7A03Xm8f9gh1ij2k3456L789mNO0pqR' | **Google Cloud Platform** |
| 'Google OAuth Client ID' = '123456789012-abcdefghijklmno1pqrstuvwxyz.apps.googleusercontent.com' |  |
| 'Google OAuth Client Secret' = 'Xyz1A2B3C4d5e6F7g8H9i0' |  |
| -----BEGIN RSA PRIVATE KEY-----  MIIEowIBAAKCAQEAzC0EXAMPLEKEYCONTENTVwIDAQAB  -----END RSA PRIVATE KEY----- | **Private keys**  **(PEM, PPK)** |
| 'IBM Cloud API Key' = 'fYgHijKlmn123_OPqrst456-UvWx789zABCDEF01' | **IBM keys** |
| ' IBM COS HMAC Access Key ID' = '1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p' |  |
| 'IBM API Connect Client Secret' = 'AbCdEfGhIjKlMnOpQrStUvWxYz123456' |  |
| Host: db.example.com Port: 5432 Database: example _ db Username: example _ user Password: P@ssw0rd!123 | **PostgreSQL credentials** |
| Host: db.example.com Port: 5432 Database: example _ db Username: example _ user Password: P@ssw0rd!123 | **MYSQL credentials** |
| 'Generic Password' = 'S3cureP@55w0rd!2023' | **Generic passwords** |
| 'Generic API Key' = '1234abcd5678efgh9012ijkl3456mnop' | **Generic API tokens** |
