<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-offline-activation -->

# Offline Activation

## [Collect Deployment IDs](/docs/mdcluster/installation/md-cluster-offline-activation#collect-deployment-ids)

1. Sign in to MetaDefender Cluster (MD Cluster) **Control Center** console.
2. Go to `Inventory` > `Licenses` and select `Offline License` tab.
3. Select Deployment IDs of MetaDefender Core instances you prefer to activate.
4. Press `Export` at the top right corner and save the exported file to your location of choice.

Info

MetaDefender Cluster **Control Center** only displays the Deployment IDs of MetaDefender Core instances that have not been activated thus far.

Info

The exported file includes a list of chosen Deployment IDs that will be used for activation in the subsequent stage.

Info

To collect the Deployment ID of a **single** MetaDefender Core instance, please:

1. Hover your mouse over the preferred Deployment ID to display the copy button.
2. Press the copy button.
3. Retain the copied Deployment ID and proceed to the next stage.

## [Activate license with Deployment ID](/docs/mdcluster/installation/md-cluster-offline-activation#activate-license-with-deployment-id)

1. Sign in to [MyOPSWAT](https://my.opswat.com/home) with your account.
2. Navigate to `License Management` on the left side panel.
3. Click `Activate License`.
4. Fill out all necessary information, including your Activation Key, Deployment ID and selection of the Package you require.

5. Click `Activate`.
6. Click `Download` and store the license file to your secure location.

Info

The license file is associated with one unique Deployment ID. The users must carry out steps 3 to 6 for every deployment ID on their list.

## [Activate MetaDefender Core instances with license files](/docs/mdcluster/installation/md-cluster-offline-activation#activate-metadefender-core-instances-with-license-files)

1. Sign in to MD Cluster **Control Center** console.
2. Go to `Inventory` > `Licenses` and select `Offline License` tab.
3. Click `Activate`.

4. Drop the license files into the dash area for submission.

5. Click `Confirm` to complete.
6. MD Cluster **Control Center** activates MetaDefender Core instances associated with the provided license files and displays their activation status.

7. Select an activated MetaDefender Core instance and press `Details` to view the license details
