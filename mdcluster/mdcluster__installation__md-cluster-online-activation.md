<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-online-activation -->

# Online Activation

MetaDefender Cluster (MD Cluster) supports seamless license activation for every deployed **MetaDefender** **Core** instance. The license key must be provided to MD Cluster **Control Center** and will be manually activated on each individual **MetaDefender Core** instance. If necessary, multiple license keys may also be supplied.

## [Adding License](/docs/mdcluster/installation/md-cluster-online-activation#adding-license)

1. Sign in to MD Cluster **Control Center** console.
2. Go to `Inventory` > `Licenses` and select `Add license`.
3. Input your license key and click `Add`.

## [License Activation](/docs/mdcluster/installation/md-cluster-online-activation#license-activation)

1. Sign in to MD Cluster **Control Center** console.
2. From the left side bar, go to `Inventory` > `Licenses`.
3. From the list of available licenses, choose the key you wish to use for activation.
4. Click `Activate` to apply the license key to the appropriate instance(s).

Info

Once `Activate` is clicked, the license key will be applied to all unlicensed **MetaDefender** **Core** instances. Ensure that your license quota is sufficient to cover all unlicensed instances.

You can view the number of activated instances and available slots by selecting **Details** on the license key. At the moment, **Details** can only be viewed after activation is successful.

## [License Deactivation](/docs/mdcluster/installation/md-cluster-online-activation#license-deactivation)

Follow these steps to deactivate your license:

1. Sign in to MD Cluster **Control Center** console.
2. From the left side bar, select `Inventory` > `Licenses`.
3. From the list of available licenses, choose the key you wish to use for deactivation.
4. Click Deactivate to remove the license from all **MetaDefender** **Core** instances currently activated with the license key.

Info

Once deactivated, the license slots will become available and can be reassigned when necessary.

When **MetaDefender** **Core** instances are undeployed through MD Cluster **Control Center**, their associated licenses are automatically deactivated.
