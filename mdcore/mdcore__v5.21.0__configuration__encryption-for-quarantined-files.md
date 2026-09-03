<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/encryption-for-quarantined-files -->

# Encryption for Quarantined Files

## [Overview](/docs/mdcore/v5.21.0/configuration/encryption-for-quarantined-files#overview)

Since 5.14.0 - MetaDefender Core offers an enhanced encryption option for quarantined files, providing a significant security improvement over the standard encryption method.

## [Benefits of Advanced Encryption for Quarantine](/docs/mdcore/v5.21.0/configuration/encryption-for-quarantined-files#benefits-of-advanced-encryption-for-quarantine)

- **Stronger Security**: Advanced encryption provides superior protection for quarantined files
- **Data Integrity**: Ensures quarantined files remain unaltered and protected
- **Industry Standard**: Uses encryption standards recognized across the security industry
- **Performance**: Optimized for efficient operation

## [Configuration](/docs/mdcore/v5.21.0/configuration/encryption-for-quarantined-files#configuration)

Please go to Settings -> Security > Encryption quarantine files

Info

- Standard encryption is enabled by default
- Existing quarantined files will remain encrypted with the method used when they were quarantined
- Enabling advanced encryption will only affect newly quarantined files
- There is no performance impact when using advanced encryption
## [Recommendations](/docs/mdcore/v5.21.0/configuration/encryption-for-quarantined-files#recommendations)

For environments with sensitive data or compliance requirements, we strongly recommend enabling advanced encryption for quarantined files to provide maximum security for potentially malicious content.
