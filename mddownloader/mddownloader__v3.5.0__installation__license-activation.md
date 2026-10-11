<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/installation/license-activation -->

# License activation

View as Markdown Ask ChatGPT about this page Ask Claude about this page Note

Since MetaDefender Update Downloader 2.4.0, the licensing mechanism has been changed.

- No longer need to activate license of Update Downloader itself to make it operational.
- Instead required to add license file (.yml) of offline MetaDefender products

Check [1.2. License activation](/docs/mddownloader/v3.5.0/installation/license-activation) to learn more how to add

## [Clean installation with Update Downloader 2.4.x](/docs/mddownloader/v3.5.0/installation/license-activation#clean-installation-with-update-downloader-24x)

## [Generate a license file (.yml)](/docs/mddownloader/v3.5.0/installation/license-activation#generate-a-license-file-yml)

- Navigate to My OPSWAT Central Management - <https://my.opswat.com> (login required)
- Navigate to “License Management” → Click “Activate License”

- Product: MetaDefender Core
- Type or paste your associated MetaDefender product's license activation key.

  - Double check to ensure no redudant space unintentionally attached into the head or tail of license string
- Type or paste your associated MetaDefender product's deployment ID.

  - Double check to ensure no redudant space unintentionally attached into the head or tail of license string
- (Optional) Write a description to keep track of this particular activation on our system for "Optional Description"
- Hit **Activate** button to generate the license file (<deployment ID>.yml)

- After that, click `Download` to download the yml file

## [Add a new product on Update Downloader](/docs/mddownloader/v3.5.0/installation/license-activation#add-a-new-product-on-update-downloader)

- Ensure you already installed Update Downloader, and setup a local admin user through its wizard
- Navigate to Inventory → Products page under left menu - <http://localhost:8028/#/user/inventory/products>
- Hit **ADD NEW PRODUCT** button to add new product on Update Downloader

- Select the license file (.yml) which was obtained in steps above

- Hit **ADD** button to start downloading offline update packages for associated licensed product

## [Upgrading Update Downloader to version 2.4.x or newer](/docs/mddownloader/v3.5.0/installation/license-activation#upgrading-update-downloader-to-version-24x-or-newer)

Update Downloader will auto create an entry the product will support to automatically migrate the configurations, and keep all licensed engine packages remained. See screenshot below as an example of upgrading from Update Downloader older version to version 2.4.0 and above.
