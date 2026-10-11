<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/can-i-use-media-manifest-futures-with-mobile-phone-storage -->

# Can I use Media Manifest futures with mobile phone storage

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MD Kiosk versions

The **Media Manifest** feature is a valuable tool for verifying whether a device has been scanned by the MetaDefender Kiosk. It ensures that only scanned and approved files are accessible for use.

However, this feature is **not currently supported for mobile phone storage**, as the MetaDefender Kiosk is unable to generate a manifest file on mobile devices after scanning. Since the **validation agent relies on the presence of this manifest file** to determine access, verification on mobile storage is not possible at this time.

If the **OMVA** is installed, the mobile phone storage **will be allowed** by default.

If the **MDE Validation** is installed, the mobile phone storage **will be blocked** by default.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
