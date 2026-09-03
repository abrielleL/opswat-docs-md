<!-- source: https://www.opswat.com/docs/mddrive/advanced-usages/offline-activation -->

# Offline Activation

MetaDefender Drive is fully functional offline, enabling license activation within air-gapped environments.

## [Obtain Deployment ID](/docs/mddrive/advanced-usages/offline-activation#obtain-deployment-id)

1. Boot MetaDefender Drive for the first time until this screen shows up

2. Shutdown then plug MetaDefender Drive into a running computer.
3. In the file browser, navigate to the MetaDefender Drive NTFS partition
4. Under the root of the NTFS partition, locate a file named *deployment_id.txt*, which contains your MetaDefender Drive deployment ID
5. Find the OPSWAT invoice provided with the **activation key** for MetaDefender Drive

#### [Request a License File for Offline Activation](/docs/mddrive/advanced-usages/offline-activation#request-a-license-file-for-offline-activation)

1. Navigate to "<https://my.opswat.com/portal/license-management/organization-licenses>", and log in using the credentials you set up during the sales process
2. Select "**License Activation**"
3. Ensure **Products** reads "**MetaDefender Drive**"
4. Enter your **Activation Key** in the given field
5. Enter your **Deployment ID** in the given field
6. Click **Activate**

7. Click **Download** when activation is successful. You should receive a file called **"<Deployment ID>.yml"**

## [Copy License File to MetaDefender Drive](/docs/mddrive/advanced-usages/offline-activation#copy-license-file-to-metadefender-drive)

1. Move the *<Deployment ID>.yml* file into the air-gapped area where the MetaDefender Drive you want to license is located
2. Insert MetaDefender Drive into the system
3. Copy *<Deployment ID>.yml* to the *license* folder on the MetaDefender Drive NTFS partition
4. Rename the *<Deployment ID>.yml* to *license.yml*
5. Eject MetaDefender Drive

## [Boot MetaDefender Drive](/docs/mddrive/advanced-usages/offline-activation#boot-metadefender-drive)

If MetaDefender Drive loads into the Update process, the license has been accepted!
