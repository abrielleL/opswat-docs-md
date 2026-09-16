<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/scripted-license-management -->

# Scripted license management

Using REST API calls, there is an option for scripted activation and deactivation for MetaDefender Core servers with **no Internet connection or if your infrastructure is using automation to create/destroy MetaDefender Core instances**. In this chapter, the steps of these two scenarios are described.

## [Requirements](/docs/mdcore/v5.22.0/installation/scripted-license-management#requirements)

- An installed MetaDefender Core instance without an Internet connection
- another computer that has an Internet connection and can run your activation scripts
- a manual or automated way to transfer data between the two computers

## [Activation steps](/docs/mdcore/v5.22.0/installation/scripted-license-management#activation-steps)

1. In order to activate MetaDefender Core, the deployment ID and activation key are needed to generate the license file.

   1. The activation key should be purchased from OPSWAT.
   2. MetaDefender Core deployment ID can be queried by using the REST API (for details, see [GET Get Current License Information](/docs/mdcore/v5.22.0/metadefender-core#licenseget) page)

Info

Save this deployment ID in your system, you might need this ID when the instance is unavailable at the time of deactivation.

2. Activate the license and get the license file using the following URL, where <quantity> is 1.

activation callCopycurl -X GET https://activation.dl.opswat.com/activation?key=<activation-key>&deployment=<deployment unique-ID>&quantity=<quantity>

If the activation is successful, a license file is downloaded. Save this file.

HTTP status codes can be:

| HTTP Response | Body | Comment |
| --- | --- | --- |
| 200 Ok | license file | Activation was successful. |
| 200 Activation failed | error: '<user conform error message>' | Failed activation |
| 200 Invalid parameter | error: 'Could not activate your product because the Activation Key you provided is invalid. Check if you typed it correctly or open a support ticket if problem persist.' | Invalid key format |
| 200 Invalid parameter | error: 'Could not activate your product because the Deployment ID you provided is invalid. Check if you typed it correctly or open a support ticket if problem persist.' | Invalid deployment format |
| 200 Invalid parameter | error: 'Could not activate your product because the quantity you provided is invalid. Check if you typed it correctly or open a support ticket if problem persist.' | Invalid deployment format |
| 400 Bad request |  | Missing key, quantity or deployment |
| 500 Internal server error | error: 'Internal server error (<error ID>). Please contact support' |  |

Info

In case of any activation issue, contact OPSWAT support for help

3. Upload license file to MetaDefender Core: The license file should be uploaded to the MetaDefender Core v4 to activate the product. For details, see page: [POST Upload license key](/docs/mdcore/v5.22.0/metadefender-core#licenseupload)

## [Deactivation steps](/docs/mdcore/v5.22.0/installation/scripted-license-management#deactivation-steps)

1. For deactivation, the following information is required:

   1. Activation key
   2. MetaDefender Core deployment ID: can be queried by using the REST API (for details, see [GET Get Current License Information](/docs/mdcore/v5.22.0/metadefender-core#licenseget) page)
2. Deactivate license using the following URL:

deactivation callCopycurl -X GET https://activation.dl.opswat.com/deactivation?key=<activation-key>&deployment=<deployment unique-ID>

Response HTTP status codes can be:

| HTTP Response | Body | Comment |
| --- | --- | --- |
| 200 Ok | result: ok | Successful deactivation |
| 200 No active license found | error: 'Could not found any active license with the given parameters' | The license has not been activated yet or it has been deactivated already. |
| 200 Invalid parameter | error: 'Could not deactivate your product because the Activation Key you provided is invalid. Check if you typed it correctly or open a support ticket if problem persist.' | Invalid key format |
| 200 Invalid parameter | error: 'Could not deactivate your product because the Deployment ID you provided is invalid. Check if you typed it correctly or open a support ticket if problem persist.' | Invalid deployment format |
| 400 Bad request |  | Missing key or deployment |
| 500 Internal server error | error: 'Internal server error (<error ID>). Please contact support' |  |

## [Important notes](/docs/mdcore/v5.22.0/installation/scripted-license-management#important-notes)

Warning

Product activation is tied to several hardware, operating system, and software parameters. In the event of one or more major hardware or software parameter changes, the product may become deactivated. Operating system updates and other software updates should not affect the activation status.

If the product is online-activated and has a live Internet connection, then in the event of a deployment ID change, the product reactivates itself. If the product doesn't have an Internet connection, then the administrator is responsible for reactivating the product.

Because of the above, the administrator should consider licensing restrictions of the offline deployments if using any virtualization and/or containerization technologies.
