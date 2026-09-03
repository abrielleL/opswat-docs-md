<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-am-i-seeing-the--invalid-core-setup--message- -->

# Why Am I Seeing the "Invalid Core Setup" Message?

This article applies to all MetaDefender Kiosk releases deployed on Windows systems.

Users may encounter the following error on the **MetaDefender Kiosk** UI when attempting to scan files: **"Invalid Core Setup."**

This error typically indicates a misconfiguration in the integration between **MetaDefender Kiosk** and **MetaDefender Core**.

It may be caused by one or more of the following:

- The API key does not match a valid local admin user in MetaDefender Core
- MetaDefender Core URL is incorrect or inaccessible
- MetaDefender Core is not licensed
- MetaDefender has a license and is activated, but no AV engines have been downloaded and enabled yet (excluding other engines like DLP, CDR, etc.). At least one active engine is required. At least one active engine is required.
- The workflow rules selected in the MetaDefender KIOSK Workflow do not exist on the Core.

### [Resolution](/docs/mdkiosk/v4.8.5/knowledge-base/why-am-i-seeing-the--invalid-core-setup--message-#resolution)

- **Access Integration Settings**
- Open the **Kiosk Management Console**, then go to: **Configuration** > **Integration**

- **Verify API Key**
- Confirm that the API key entered corresponds to a **local admin user** in MetaDefender Core.

- Refer to [this article](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-generate-an-api-key-on-the-core-deployment-) for instructions on how to check the User directory (SYSTEM or LOCAL) and the API key associated with a user in MetaDefender Core.
- **Verify MetaDefender Core URL**
- Ensure the MetaDefender Core URL is accurate, including the correct protocol (`http` or `https`), IP address or hostname, and port number. Example: `https://192.168.1.100:8008`
- **Check MetaDefender Core Licensing**
- Confirm that MetaDefender Core is **licensed**. An unlicensed Core instance will prevent proper integration. For instructions on verifying the MetaDefender Core license status, please refer to [this article](https://www.opswat.com/docs/mdcore/installation/metadefender-core-licensing#check-your-license-details).
- **Check the AV Engines on MetaDefender Core**
- To verify the antivirus (AV) engines enabled on MetaDefender Core:

1. Open the **MetaDefender Core** web UI.
2. Navigate to **Inventory** > **Modules** > **MetaScan**
3. Under the **MetaScan** section, review the list of AV engines and confirm which ones are currently enabled.

- **Verify Workflow Rule Existence on MetaDefender Core**
- To ensure that the workflow rules selected in the MetaDefender KIOSK configuration exist on MetaDefender Core:

1. Open the **MetaDefender KIOSK** UI.
2. Navigate to **Workflow > Process**.
3. Identify the selected workflow rule(s).

4. Then, log in to the **MetaDefender Core** UI and confirm that the corresponding workflow(s) exist and are properly configured.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
