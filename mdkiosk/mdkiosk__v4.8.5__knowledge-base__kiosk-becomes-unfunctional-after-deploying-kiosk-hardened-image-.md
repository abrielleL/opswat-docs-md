<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/kiosk-becomes-unfunctional-after-deploying-kiosk-hardened-image- -->

# Kiosk becomes unfunctional after deploying Kiosk Hardened Image 25.06.0 (or later)

### [**Issue**](/docs/mdkiosk/v4.8.5/knowledge-base/kiosk-becomes-unfunctional-after-deploying-kiosk-hardened-image-#issue)

After deploying the Kiosk Hardened Image version 25.06.0 (or later), the device loses all drivers and becomes unfunctional.

### [**Cause**](/docs/mdkiosk/v4.8.5/knowledge-base/kiosk-becomes-unfunctional-after-deploying-kiosk-hardened-image-#cause)

This issue occurs if the hardened image was deployed using an outdated deployment tool. Starting from version 25.06.0, the Kiosk Hardened Image requires a new deployment tool to ensure successful and complete deployment of Kiosk Hardened Image.

### [**Resolution**](/docs/mdkiosk/v4.8.5/knowledge-base/kiosk-becomes-unfunctional-after-deploying-kiosk-hardened-image-#resolution)

To resolve this issue:

1. Download the latest deployment tool [link](https://kiosk-hardened-image.s3.dualstack.us-west-1.amazonaws.com/kiosk-hardened-image/official-releases/deployment-tool/2506/WINPEBootable.vhd)
2. Re-create Kiosk deployment flash drive with the latest deployment tool by following this [KB](https://www.opswat.com/docs/mdkiosk/hardened-image/guideline---deploying-kiosk-hardened-image#step-2-creating-the-kiosk-deployment-flash-drive)
3. Re-deploy the Kiosk device using the new Kiosk deployment flash drive
