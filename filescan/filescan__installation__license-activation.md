<!-- source: https://www.opswat.com/docs/filescan/installation/license-activation -->

# License Activation

## [License restrictions](/docs/filescan/installation/license-activation#license-restrictions)

An activated and valid license deployment is necessary to access the full functionality of the product. Without such license it is not possible to start scan requests.

## [License limitations](/docs/filescan/installation/license-activation#license-limitations)

Scan limit: licenses contain a scan limit which defines the number of scans allowed daily. It is not possible to start new scan processes once the daily limit is depleted.

## [Deployment ID](/docs/filescan/installation/license-activation#deployment-id)

Product deployments are represented by a unique system fingerprint called `Deployment ID.`

Licensing is based on the generated deployment ID and a limited number of activations are possible for each license. Therefore every time your product is deployed with a different deployment ID, it will be captured as a different activation record accumulated into your total activations allowed.

Once the number of active deployments reached the deployment limit, new product activations are not possible.

Notice

The Deployment ID is an automatically generated unique fingerprint identifying the computer the product is deployed on. It might change when you alter the system that the product is installed on.

## [License Actions](/docs/filescan/installation/license-activation#license-actions)

Navigate to *Admin panel > Settings > Integrations* tab and select *Licence Management*. You can find here the main license information and connected transform instances.

### [Online license activation](/docs/filescan/installation/license-activation#online-license-activation)

Click on *Activate all* (or *Activate* for single instances) to open the activation dialog and select *Activate online*.

Fill in the license key text box with your license key and click on *Activate.* On success, the license of the selected instance becomes available, on error you will see a detailed error message.

### [Offline license activation](/docs/filescan/installation/license-activation#offline-license-activation)

In air-gapped environments the product can be activated with the help of another computer that has a working internet connection. The Deployment ID of the target computer and the Activation Key will be required to download an offline license file (.yml) via your [My OPSWAT](https://my.opswat.com/portal/products) portal. Follow the displayed instructions for details.

#### [Steps to activate offline](/docs/filescan/installation/license-activation#steps-to-activate-offline)

- Generate Deployment ID by executing the fsDeploymentID script, which can be found in the release package.
- Use your Activation Key and Deployment ID to download an offline license file from your My OPSWAT portal.
- Navigate to the *License Management* page, open the activation dialog and select *Activate offline* . Upload your license file and click on *Activate.*

On success, the license of the selected instance becomes available, on error you will see a detailed error message.

## [Deactivation](/docs/filescan/installation/license-activation#deactivation)

Click on *Deactivate all* (or *Deactivate* for single instances) to open the deactivation dialog and review the instances to deactivate.

Click on *Deactivate.* On success, the license of the selected instance becomes unavailable, on error you will see a detailed error message.

## [Troubleshooting](/docs/filescan/installation/license-activation#troubleshooting)

For online activation, make sure that there is a working internet connection and the OPSWAT Activation Server is reachable (<https://activation.dl.opswat.com>)

Test if Activation Server is network reachableCopywget -S --spider https://activation.dl.opswat.com 2>&1

In case of expired license status ask for support on your My OPSWAT portal.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
