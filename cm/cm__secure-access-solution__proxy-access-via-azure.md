<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/proxy-access-via-azure -->

# Proxy access via Azure

My OPSWAT Central Management utilizes a secure access method called proxy-based access. This method uses a combination of proxies to provide device compliance based access control to applications that can limit access based on location. This approach is designed with Azure AD's Location based Conditional Access policies.

To enable this feature:

- Navigate to **Secure Access > Access Methods > Proxy**.
- Under this tab, enable proxy-based access by enabling **Enable Azure Protection**.
- Copy the Host IP address and save for later.
- Select **Save**.

*Note: For Azure Protection to work, cross-domain API must be enabled and the port set to 1139. For more information on cross-domain API, click *[*here*](https://docs.opswat.com/macloud-sdp/developer-guide/cross-domain-api)*.*

Once enabled in My OPSWAT Central Management, you will need to configure Microsoft AD accordingly:

- Navigate to Azure's portal and sign into your account.
- Continue on to **Conditional Access**, and select **Named locations**.
- Select **+IP ranges location**.
- Fill out name, and add the IP range based on the Host IP address in My OPSWAT Central Management '/32' at the end of the address.
- Select **Create.**
- Navigate to **Policies**, and select **+ New Policy**.
- Fill out name and assign relevant users.
- Select **Conditions > Locations** **> Exclude**, and select the IP range you created.
- Under **Access Controls**, select **Grant** and change to **Block access.**
- Enable the policy.
- Select **Create**.

![](https://uploads.developerhub.io/prod/1yda/i7hezp2ucb8gpwk4j24jquqhh9d4gdipxhqma8t42z4qwk127h8sfkxmqhek3obu.png)

After creating this policy, My OPSWAT Central Management will be able to determine access to Microsoft products based on the device's compliance state.

*Note: The minimum OPSWAT agent version to support proxy-based access control is: 7.6.2301.163 (Windows only).*
