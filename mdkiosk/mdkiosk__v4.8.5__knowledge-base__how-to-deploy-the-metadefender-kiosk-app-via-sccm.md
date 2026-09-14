<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-deploy-the-metadefender-kiosk-app-via-sccm -->

# How to deploy the Metadefender Kiosk App via SCCM

This article applies to all MetaDefender Kiosk releases deployed on Windows Systems

MetaDefender Kiosk does not natively support full command-line installation with initial configuration. This workaround outlines a process of simplifying setup by preconfiguring configuration files on a lab machine and deploying via SCCM.

## [Steps to Configure](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-deploy-the-metadefender-kiosk-app-via-sccm#steps-to-configure)

### [Step 1: Preparation (Lab Environment Setup)](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-deploy-the-metadefender-kiosk-app-via-sccm#step-1-preparation-lab-environment-setup)

1. Install Kiosk manually on a lab computer. This lab computer will be used to gather the desired initial configuration that will be imported.
2. Complete the initial setup, including:

   - Admin account configuration
   - Any custom application settings
3. Uninstall the application once setup is complete.
4. Backup configuration files:

   - Path: `C:\\ProgramData\\OPSWAT\\Metadefender`
   - These contain all the initial setup details required for deployment.

### [Step 2: Deployment via SCCM](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-deploy-the-metadefender-kiosk-app-via-sccm#step-2-deployment-via-sccm)

1. **Preload configuration:**

   - Copy the backed-up folder to: `C:\\ProgramData\\OPSWAT\\Metadefender`
   - **Tip:** Use SCCM’s pre-deployment script or task sequence.
2. **Silent Installation via Command Line:** Use the documented CLI parameters from <https://www.opswat.com/docs/mdkiosk/installation/installing-metadefender-kiosk-from-the-command-line>
3. **License Activation Using REST API (via cURL):**

curl -X GET "<https://activation.dl.opswat.com/activation?key=<activation-key>>&deployment=<deployment-unique-ID>&quantity=1" > activation.yml

- Proceed to activate the Kiosk offline.

## [Prerequisites](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-deploy-the-metadefender-kiosk-app-via-sccm#prerequisites)

- SCCM
- Metadefender Kiosk App

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
