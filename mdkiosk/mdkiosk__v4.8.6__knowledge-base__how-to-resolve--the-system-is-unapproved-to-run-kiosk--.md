<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-resolve--the-system-is-unapproved-to-run-kiosk-- -->

# How to resolve "The system is unapproved to run Kiosk"?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MD Kiosk L-Series.

**MetaDefender Kiosk Linux** is one of our most advanced products, developed with a **strict internal policy framework** to ensure maximum security and reliability.

One key feature is the **System Integrity Check**. If a peripheral device or USB storage is connected **before the Kiosk boots**, the system will automatically detect the change and display a **security alert**. This mechanism is designed to prevent unauthorized tampering or pre-boot manipulation of the device.

Warning:

**USB keyboards, mice, and network adapters** are also considered **unapproved peripherals** if connected before the system boots.

**Mouse and keyboard input are not supported** in MetaDefender Kiosk Linux.

## [How to resolve?](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-resolve--the-system-is-unapproved-to-run-kiosk--#how-to-resolve)

To resolve the error, please check for any **connected peripheral devices or USB storage** attached to the Kiosk. If found, **unplug the device**, then **restart the Kiosk** by performing a full power cycle (power off and then power on).

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
