<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods -->

# Understanding Disk Encryption Detection via DetectProduct and GetEncryptionState methods

## [Overview](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#overview)

This article explains how to use the `DetectProduct` and `GetEncryptionState` methods to assess the presence and operational state of disk encryption solutions on endpoints. It covers how encryption detection is reported and interpreted for both software-based and hardware-based encryption tools, including FileVault and BitLocker.

## [DetectProduct method Usage](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#detectproduct-method-usage)

**Purpose**

The `DetectProduct` method identifies all encryption software installed on an endpoint, regardless of whether the encryption is actively running.

**Behavior**

- When invoked with `category = 3` (encryption), the method returns all disk encryption applications installed.
- This includes tools that may not currently be encrypting the system.

**Example JSON Input**

JsonCopy{
"input": {
"method": 0,
"category": 3
}
}
## [GetEncryptionState method Insights](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#getencryptionstate-method-insights)

The `GetEncryptionState` method provides detailed information on whether an endpoint's drives are encrypted and which encryption product is responsible.

**Key Response Fields**

- `encryption_active`

  - Other Products: Indicates `true` if encryption is actively in use, including states like encrypting, encrypted, partially encrypted, or suspended.
  - FileVault: Reflects whether FileVault is enabled. Returns `true` if FileVault is turned on.
- `fully_encrypted`

  - Returns `true` if all encryptable drives are completely encrypted.
  - On Apple Silicon devices, drives may still be encrypted through hardware even if FileVault is off. This is reflected by `"encryption_type": "hardware"`.
- `locations`

  - Lists all disk volumes with the following relevant sub-fields:

    - `encryptable`: Indicates whether the drive can be encrypted. Does not imply the drive is currently encrypted.
    - `state`: Reports encryption status per volume. Possible values include unencrypted, encrypted, suspended, partial, etc.

## [Behavior of Specific Encryption Products](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#behavior-of-specific-encryption-products)

### [BitLocker](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#bitlocker)

Works optimally in admin mode, which grants full access to retrieve detailed encryption metadata, such as the encryption algorithm.

In normal mode, the methods may report only basic information (e.g., state and path), and omit advanced fields. This difference is due to permission restrictions in normal mode.

### [FileVault](/docs/mdsdk/knowledge-base/understanding-disk-encryption-detection-via-compliance-methods#filevault)

Provides accurate and consistent values in both `encryption_active` and `fully_encrypted`.

On Apple Silicon systems, encryption can persist via hardware encryption even when FileVault is off.
