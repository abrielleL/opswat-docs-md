<!-- source: https://www.opswat.com/docs/product-management/configuration/configuration -->

# Instance Configuration

For the configuration management feature, My OPSWAT does not have support for all OPSWAT products yet.

Please refer to [Products Dashboard](/docs/product-management/operating/product-dashboard) for a list of supported OPSWAT products. Support for the configuration management feature is indicated in the **Configuration** column.

Each product type has different configuration settings available. Please refer to their respective documentations on docs.opswat.com.

## [Update configuration for a specific Instance](/docs/product-management/configuration/configuration#update-configuration-for-a-specific-instance)

You can view and update an instance configuration by selecting a specific instance in the [instance dashboard](/docs/product-management/configuration/instance-dashboard) to navigate to the instance details then select the **Configuration** tab.

Click **Edit** to enable editing. After making changes, click **Save** to confirm changes. Please note that the changes will be applied to the instance when the instance fetches a new configuration.

## [Elevate an instance configuration to Group Configuration](/docs/product-management/configuration/configuration#elevate-an-instance-configuration-to-group-configuration)

In the instance details view, click **Set As Group Configuration** to set this instance's configuration as the group configuration for the product group that the instance belongs to. Please refer to [Product Group](group-dashboard) for more information.

## [Instance configuration Version](/docs/product-management/configuration/configuration#instance-configuration-version)

**Instance Configuration Version** is used to indicate the configuration status of an instance.

- Version, for example 1.0.1: indicate what group configuration version applied to the instance.

  - If the configuration version is 0.0.0, the instance has not been applied the group configuration from the time it was moved to the group
  - If there is an icon followed by the version, it means the instance configuration is customized based on that group configuration version. There are 2 possible use cases

    - a star icon (*): an admin updated the instance configuration directly on My OPSWAT console.
    - a sync icon: the instance synchronized its configuration back to My OPSWAT when its configuration was modified on the instance in one of the below situations:

      - the instance upgrades to a new version;
      - the instance updates its engines
      - an admin modified some settings directly on the instance console
- Status:

  - <blank>: the instance fetched the current instance configuration.
  - Pending: the configuration has not applied to the instance yet. It's waiting for the instance to fetch that configuration
  - Out of Date: the current group configuration has not applied to the instance yet.

Below is a list of all possible configuration versions and their meanings.

| Use case |  | Instance configuration |
| --- | --- | --- |
| An admin applied the group configuration 1.0.3 to the instance. |  | 1.0.3 |
| An admin applied the group configuration 1.0.3 to the instance .  However, the instance's configuration may be modified on the instance itself since the instance upgrades to a new version; OR it updates its engines; OR an admin modified some settings directly on the instance console. In this case, the instance synchronizes its configuration back to My OPSWAT |  | 1.0.3 |
| An admin applied the group configuration 1.0.3 to the instance .  However, an administrator updated the instance configuration directly. |  | 1.0.3 * |
| The last version of the group configuration was applied to the instance is 1.0.2. However, the current group configuration version is 1.0.3 or above. |  | 1.0.2 Out of Date |
| An instance has not been applied the group configuration (such as just enrolled, moved from other group to this group). |  | 0.0.0 |

Note that all changes on instances' configuration can be tracked in the Event Log.
