<!-- source: https://www.opswat.com/docs/mdss/4.5.2/operations/password-protected-files-encrypted-archives -->

# Password Protected Files and Encrypted Archives

## Overview

**Password-protected** or **encrypted files**, such as Word documents, archives, and PDFs, cannot be scanned without providing the appropriate password to the scanner instance. To address this limitation, MetaDefender Storage Security offers several features, which we will detail below.

## Password Storage

One option is to utilize the **Password Storage** feature from MetaDefender Core as explained [here](https://www.opswat.com/docs/mdcore/operating/inventory-management#password-storage).

This feature enables you to define and manage a list of static passwords used for file decryption, making it particularly useful for automated workflow scenarios. When this feature is enabled, the scanner can decrypt and scan the file seamlessly, meaning it will not appear as password-protected in Storage Security.

## Unlocking Encrypted Files within Storage Security using the GUI

This feature empowers you to take control of sensitive data by enabling immediate scans of encrypted files. Simply provide the necessary passwords through the intuitive user interface and Storage Security will analyze the files, ensuring comprehensive protection against hidden threats.

Unlocking Encrypted Files within MetaDefender Storage Security is simple **for users who prefer the GUI**:

1. Identify Encrypted Files: In the Reports page, look for files marked with a lock icon, indicating an "Encrypted" verdict. These files are automatically blocked to ensure security.

![](https://uploads.developerhub.io/prod/k8zL/eklsejjplwsop3v3mmjytnfzm80di7pvu6z9zdklcuw48y55qepo4dk3frgy30ri.png)

2. Provide Passwords: Click the lock icon to open a window where you can securely enter potential passwords. Need to try multiple passwords? Easily add more with the "plus" symbol. You can also visualize your entered passwords using the "eye" icon.
3. Initiate Rescan: Click the rescan icon to begin the decryption process. MDSS will attempt to decrypt the file using each password provided.

![](https://uploads.developerhub.io/prod/k8zL/l8wtqciak4zownp25uqj8r54qo9t118r4eyxfi1jbroahw21t6pxuwg7rkhg1ce4.png)

![](https://uploads.developerhub.io/prod/k8zL/hxupcm8knxr4a1u7py0v0xrcn07qjsydx5xhu7maeze4bxa3qwqpdge1n8jgrc3y.png)

Currently, you can rescan one encrypted file at a time. We are actively working to enhance this feature, allowing you to provide passwords for multiple encrypted files simultaneously in future releases.

## Unlocking Encrypted Files within Storage Security using the API

For **users who prefer the API integration**, MetaDefender Storage Security offers a flexible approach to On-Demand Scanning of encrypted archives:

The dedicated API endpoint allows you to initiate rescans of encrypted files programmatically. This means you can trigger a rescan at any time, regardless of whether you have passwords to provide.

If passwords are available, simply include them in your API request. MDSS will attempt decryption using the provided passwords and return the scan results. This enables seamless integration of encrypted archive scanning into your automated workflows and security processes.

This API-driven approach provides advanced users with the control and flexibility they need to manage encrypted archives effectively within their existing systems. [Full API documentation](https://docs.opswat.com/mdss/metadefender-storage-security-api#file-ondemandscan)  is available to guide your implementation.

**Request Body:**

```json
{

	"fileId": "{string}",
	"scanId": "{string}",
	"storageProtocolType": "{int32}",
	"passwords": ["{array[string]...}"]
}
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
