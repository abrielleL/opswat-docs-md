<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/user-guide/how-to-troubleshoot--logon-invalid---token-doesn-t-match-the-exp -->

# How to troubleshoot "Logon Invalid - Token doesn't match the expected account" on macOS?

> **Check Your Version:**
>
> This article applies to all Metadefender Endpoint releases deployed on MacOS systems

### **Issue:**

Users may encounter a "Logon Invalid - Token doesn’t match the expected account" error when attempting to log into **MetaDefender Endpoint** via the **SDP** application on a Mac.

**Symptoms:**

1. **UI Error:** When attempting to sign in, the application displays a red error banner at the top of the window stating:

![](https://uploads.developerhub.io/prod/2x2P/xk59ualqyxdxvgpijs9wb0oupmwyesuugjyayp3xfae0o1ijid3h3efoj9i3svaw.png)

2. **Log Error:** The `sdp-daemon.log` file will show an entry similar to the following, indicating the token format is not being recognized correctly:

`2026-01-05T17:54:11Z: auth token doesn't look like a JWT, assuming that it's a base64-encoded JSON blob...`

### **Cause**

This error typically occurs because the **SDP SENetworkExtension** is not enabled or was blocked during installation. Without this extension active, the application cannot properly validate the authentication token against the user's account.

### **Solution**

To resolve this issue, you must manually enable the Network Extension in your macOS System Settings:

1. Open the **Apple Menu** and select **System Settings**.
2. Go to **General** > **Login Items & Extensions**.
3. Scroll down to the **Extensions** section and click the **(i) (Info icon)** next to **Network Extensions**.
4. Find **SDP SENetworkExtension** and toggle the switch to **ON**.
5. If prompted, enter your administrator password to confirm the change.
6. Attempt to sign in to the SDP application again on the **MetaDefender Endpoint** > **SDP/VPN** > *Sign In* to the appropriate logon option for your company.

![](https://uploads.developerhub.io/prod/2x2P/vbablka9bnva02qtad1nxu1f12dmk800ewmvkf6959xf6diqdz0cbiu9oiqj8ajx.png)

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
