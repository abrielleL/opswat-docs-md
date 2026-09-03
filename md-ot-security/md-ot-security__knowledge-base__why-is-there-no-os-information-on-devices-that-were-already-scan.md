<!-- source: https://www.opswat.com/docs/md-ot-security/knowledge-base/why-is-there-no-os-information-on-devices-that-were-already-scan -->

# Why is there no OS information on devices that were already scanned?

**Check Your Version:**

This article applies to specific versions of MetaDefender OT Security. Please check instructions for settings that apply to your specific version.

## [**Background**](/docs/md-ot-security/knowledge-base/why-is-there-no-os-information-on-devices-that-were-already-scan#background)

For common traditional IT devices (Computers with Windows or Linux OS), the OS info mostly come from active scanning. The lacking of OS info on some devices could be due to:

1. Active scan settings is not configured on a NIC of the sensor.
2. The OS scanning is not enabled for some device types that preliminary identified.
3. Possible discrepancy between auto active scanning and manual scanning.

## [**Solution**](/docs/md-ot-security/knowledge-base/why-is-there-no-os-information-on-devices-that-were-already-scan#solution)

On versions of MetaDefender OT Security from 3.1.0 though 3.4.9.

Check if the active scanning settings are configured for the sensor and OS scanning is enabled for the asset category:

### [**I. Active Scanning:**](/docs/md-ot-security/knowledge-base/why-is-there-no-os-information-on-devices-that-were-already-scan#i-active-scanning)

1. Go to **Settings** → **Network & Discovery**
2. Enable **Active Discovery.**

### [**II. OS Scanning:**](/docs/md-ot-security/knowledge-base/why-is-there-no-os-information-on-devices-that-were-already-scan#ii-os-scanning)

1. Go to **Policies → Port Scan Rules**.
2. Search for the device types (e.g **Computer** or **Virtual Machine**).
3. Next, check the box for **Enable Smart Effective Scanning**.
4. Then, select **Allow Scan Port** and **Allow Scan OS**.
5. After that, the application will automatically scan the OS for all devices with the types specified.

---

On versions of MetaDefender OT Security 3.4.10 and higher

We understand the auto OS scan settings for device type is not very visible and can be looked over. Our enhancement is to provide an explicit OS scanning item on the “Smart Asset Profiling” where user can run OS scan/ discovery for select assets:

1. Navigate to **Assets** → **Smart Asset Profiling**.
2. Select **OS Scanning.**

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
