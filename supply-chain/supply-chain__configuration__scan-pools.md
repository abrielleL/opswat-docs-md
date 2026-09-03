<!-- source: https://www.opswat.com/docs/supply-chain/configuration/scan-pools -->

# Scan Pools

In order to create a workflow, that can be used to run scans and checks on various integrations, it is necessary to first configure a valid scan pool that can be used as a scan service provider.

Scan Pools can be added from "Settings" menu under the 'Scan Pools' tab:

![](https://uploads.developerhub.io/prod/jdK6/hythc9dyd09cdp54zt8kw9a6ivip9r01itdb3n93hxvmuikrrxclshgjwzutt4rm.png)

Different types of scan pools can be registered, and for each type it is possible to register multiple service providers.

---

### Default MD Core Scan Pool

This Scan Pool type allows registration of a MetaDefender Core URL that MetaDefender Software Supply Chain service can use to scan the integrated Supply Chain.

![](https://uploads.developerhub.io/prod/jdK6/imopfciq2j3di1azhazpexqt7hu9rb88brzlgkoehsncmxirn6g4u7ty3a8w2arb.png)

As seen in the above image, this page provides a "+ Add Scan Instance" button. To add the first or any additional scan instances, the user can press this button which will open a "Add New Scan Instance" popup window that provides 3 input fields:

- **URL :** in this field the user can provide the ip address and the port of the REST service, in the following format: "[http://10.30.160.84:8008/"](http://10.30.160.84:8008/%22)
- **API Key :** for specific MetaDefender Core configurations it is necessary to provide this value. Please contact the MetaDefender Core instance administrator to check if the instance requires this value or not.
- **Timeout :** is used to configure the time that MetaDefender Software Supply Chain framework will wait before it will time out a connection attempt to this scan instance.

An existing entry can be modified by clicking on the "..." button at the end of each listing and choosing "Edit" form the dropdown menu. This will result in a "Edit Scan Instance" popup window, that will present the same field as the "Add New Scan Instance" described above.

An existing entry can be deleted, by clicking on the same "..." button at the end of each listing and choosing "Delete" this will display a confirmation dialog:

![](https://uploads.developerhub.io/prod/jdK6/8sbwfdhnjv8wz0fxmas2ciacufnoqao7qayjxnt5ev9qrgmugrgk23fby2rozlmn.png)

> **Warning**
>
> An existing scan instance can only be deleted if it is not used in any workflow.

If the scan instance is in use, the Delete operation will fail and an error message is printed beside the "Delete" button. The user should close this dialog, and proceed to remove the usage of this scan instance from all workflows.

After removing from all existing workflows, the delete operation should succeed.

---

### Default MD Cloud Scan Pool

This type of Scan Pool allows registering MetaDefender Cloud Scanning Services the interface is identical with the interface of adding a Default MD Core Scan Pool, described above.
