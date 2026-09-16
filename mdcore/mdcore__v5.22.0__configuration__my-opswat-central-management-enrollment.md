<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment -->

# Enrollment and MetaDefender Core Configuration on My OPSWAT Central Management

## [Enrollment](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#enrollment)

To enroll MetaDefender Core (MD Core) into My OPSWAT Central Management (MOCM), follow these steps:

1. Obtain the `Server URL` and `Registration Code`. Please refer to this instruction for more details: [Enroll other Products - My OPSWAT Central Management](https://www.opswat.com/docs/cm/product-management/other-products)
2. Click the `Unmanaged` button, enter the `Server URL` and `Registration Code` then click `Enroll now.`

## [Configuring MetaDefender Core within My OPSWAT Central Management](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#configuring-metadefender-core-within-my-opswat-central-management)

### [Configuring each MetaDefender Core instance](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#configuring-each-metadefender-core-instance)

To access the MD Core configuration in the MOCM console, navigate to **Inventory > Services** and select **<Instance**

**Name> > Configuration**.

For more information about other functionalities in the **Inventory** menu of the MOCM console, please refer to the following link: [Inventory - My OPSWAT Central Management](https://www.opswat.com/docs/cm/product-management/inventory)

### [Configuring a group of MetaDefender Core instances](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#configuring-a-group-of-metadefender-core-instances)

In addition to supporting the configuration of individual MD Core instances, MOCM also supports configuring a group of MD Core instances simultaneously. Please refer to this link for more details about group configuration in MOCM: [Groups - My OPSWAT Central Management](https://www.opswat.com/docs/cm/product-management/groups)

### [What MetaDefender Core configurations are supported on My OPSWAT Central Management?](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#what-metadefender-core-configurations-are-supported-on-my-opswat-central-management)

Legend

✅Supported

🟨Partially supported

#### [General](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#general)

🟨 Security

- Secure Connection

✅ Module Update

✅ Data Retention

✅ Health Check

✅ Central Management

#### [Workflow](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#workflow)

✅ Workflow Rules

✅ Workflow Templates

✅ Security Zones

#### [Inventory](/docs/mdcore/v5.22.0/configuration/my-opswat-central-management-enrollment#inventory)

✅ Modules

- ✅Configuration
- ✅Lock/Unlock engine package
- ✅Disable/Enable engine
- ✅Delete engine

✅ External Scanners

✅ Webhook Authentication

✅ Post Actions
