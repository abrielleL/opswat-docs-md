<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-does-kiosk-show--invalid-core-setup-- -->

# Why does Kiosk show "Invalid Core Setup"?

This article applies to all MetaDefender Kiosk releases deployed on Windows.

## [Introduction](/docs/mdcore/v5.22.0/knowledge-base/why-does-kiosk-show--invalid-core-setup--#introduction)

There are many different reasons why you may view the “Invalid Core Setup”, please review the below:

1. **Incorrect API key**

Navigate to Kiosk > Configuration > Integrations > Primary MetaDefender Core Server. Compare the API key with the admin local user on MetaDefender Core

2. **Incorrect MetaDefender Core “Server URL”**

*

Open the MetaDefender Core Website in the Kiosk machines Browser and copy the URL and paste it here, ending with the port

*

If MetaDefender Core has a certificate enabled for HTTPS, please use the [https://<FQDN>:8008](https://opswat.atlassian.net/wiki/spaces/~71202072e168519b204f5db27c73bcb68cc135/pages/3933306925/Why+does+Kiosk+show+Invalid+Core+Setup#)

Example: <https://certificateSAN:8008>

3. **Unlicensed MetaDefender Core or MetaDefender Kiosk**

Confirm that both the MetaDefender Core and MetaDefender Kiosk are properly licensed.

MetaDefender Core:

MetaDefender Kiosk:

How to activate Kiosk offline: [Managing License Information](https://www.opswat.com/docs/mdkiosk/installation/managing-license-information)

4. **Network connectivity issue between MetaDefender Core and MetaDefender Kiosk**

Check for network issues that might prevent communication between the Kiosk and Core. Consult with your networking team if necessary. Example: Firewall, proxy, low bandwidth

5. **Expired Certificate** If the certificate on the MetaDefender Core machine is expired, update and install it correctly on the Kiosk's Windows OS inside the Local Machines Trusted Root Certificate Store.

*

Open the MetaDefender Core website from the Kiosk machine after performing the change

6. **MetaDefender Core service is not running**

Verify that the MD Core services are running properly. Restart them if necessary.

7. **MetaDefender Core Modules inactive/permanently failed**

If required engines are still updating, please wait until they are complete.

If they are missing dependencies, check our “[Third Party Dependencies](/docs/mdcore/v5.22.0/installation/recommended-system-configuration)” to resolve

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
