<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/validation-endpoint/how-do-i-disable-usb-read-only-mode-in-metadefender-endpoint-val -->

# How do I disable USB Read-Only Mode in MetaDefender Endpoint Validation if it was enabled in the deployment configuration?

> **Check Your Version:**
>
> This article applies to MetaDefender Endpoint Validation 3.1.2510 and later (Windows)

USB read-only mode is disabled by default. If it was enabled in the configuration tool when the deployment package was generated, every endpoint validation installed with that package will enforce read-only access: users can read files from validated USB media but cannot copy, modify, or write anything to the media. The agent status window (About box) shows:

USB Read-Only Mode Status: Enabled

There are two ways to disable the mode. Choose based on whether you need a temporary or a permanent change.

## **Method 1 - Permanent: regenerate the deployment package and reinstall (recommended)**

Because MetaDefender Endpoint Validation is a standalone agent, its settings come from the encrypted configuration file bundled with the installer. The service reads this configuration at every startup, so the only change that reliably persists across reboots is a change to the deployment package itself.

1. Open the MetaDefender Endpoint Validation [configuration tool](https://docs.opswat.com/mdendpoint/validation-endpoint/configuration-tool) included in your deployment package. The tool can also be downloaded from My OPSWAT > Product Downloads > MetaDefender Endpoint.
2. Click Load config and select your current encrypted configuration file. Note that the installer path, certificate path, output folder, and password are not stored in the configuration file and must be re-entered.
3. Uncheck the USB read-only mode option.
4. Select the destination path and click Generate to produce the updated deployment package.
5. Reinstall the agent on the affected endpoints using the regenerated package, and use this package for all future installations.

## **Method 2 - Per endpoint: the Disable USB read-only mode command**

On an individual endpoint, the mode can be turned off without reinstalling:

1. Open MetaDefender Endpoint Validation on the endpoint and select the Disable USB read-only mode option.
2. Authenticate with the agent's admin password. If the admin password is not available at the endpoint, use a challenge and response code instead: the agent generates a challenge string, an administrator enters it in the My OPSWAT Portal to generate a one-time response code, and entering that code on the endpoint executes the command. See: [Challenge and Response - MetaDefender Endpoint](https://docs.opswat.com/mdendpoint/validation-endpoint/challenge-and-response)
3. Verify the About box shows USB Read-Only Mode Status: Disabled. Write access to validated media is restored immediately. All validation and blocking protection remains active.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
