<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure -->

# Licensing Automation on Azure

To activate the instances where the MetaDefender products are running, it is needed to activate these products providing the LICENSE_KEY.

There are 2 options to manage the licensing that will automate the activation and deactivation of the products.

## [Azure Function to handle the VMSS events](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#azure-function-to-handle-the-vmss-events)

### [Diagram](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#diagram)

Info

Solution recommended for production as the activation and deactivation does not depend if the VM is gracefully terminated or not

### [Pre-requisites](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#pre-requisites)

This sections presumed that a VMSS has been created with the Azure VM image generated based on the database mode desired. If not please go to [VM Scale Set](/docs/mdcore/v5.22.0/cloud-deployment/vm-scale-set-deployment)

### [Resources Needed](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#resources-needed)

- Azure Function App
- Azure Key Vault
- Azure Event System Topic
- Azure Event Subscription
- Azure Function to run within the Azure Function App

Info

This guidelines are for creating the resources from Azure Portal. To use Terraform please check

### [Azure Function](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#azure-function)

Check the [Deployment Options for Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-technologies?tabs=linux)

This function has 2 different tasks.

- **Activation**: Retrieve the LICENSE_KEY and APIKEY from Azure Secret and activate the VM. Store the deployment ID to Azure Key Vault using VM as key
- **Deactivation**: Retrieve Deployment ID from Azure Secret and deactivate the deployment.

**Steps to create the Azure Function**

1. Create the Azure Function App (Recommended Flex Consumption Plan)
2. Create Azure Key Vault with the following required keys

   1. License Key (licenseKey)
   2. API Key (apiKey)
   3. Core UI User (coreUser)
   4. Core UI Password (corePwd)
3. Create an Access Policy in the Key Vault for the Azure Function to "Get", "Set", "List", "Delete", "Purge" and "Recover"
4. Set Up as environment variables for the Azure Function App

   1. SUBSCRIPTION_ID
   2. KEY_VAULT_NAME
5. Deploy the [Event Licensing Handler Function](https://github.com/OPSWAT/metadefender-csp/tree/main/Azure/function_project/event_licensing_handler)

### [Trigger the Azure Function](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#trigger-the-azure-function)

This Azure Function has to be triggered by an Azure Event Grid System Topic and a Event Grid Subscription to link the topic and trigger the Azure Function based on events that will be specified in the subscription.

#### [Create Event Grid System Topic](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#create-event-grid-system-topic)

This topic will generate events for the resource group linked to it.

**How to create it from Azure portal**

1. Go to Event Grid > Azure Service Event > System Topics
2. Create Topic > Select Azure Subscription or Resource Group
3. Enable system assigned identity and input all the tags

#### [Create Event Grid Subscription to System Topic and Azure Function](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#create-event-grid-subscription-to-system-topic-and-azure-function)

The subscription will link the Azure Event Grid Topic to the Azure Function already created.

**How to create the Event Grid Subscription**

1. Go to Event Topic and create Subscription from within it
2. Indicate name and Event Grid Schema
3. Under Event Types select only Resource Action Success
4. Configure the Endpoint to be the Azure function created in previous section
5. Under filters Enable subject filtering

   1. Subject Begins With: "/subscriptions/{subscription_id}/resourceGroups/{RG_NAME}/providers/Microsoft.Compute/virtualMachines"
6. Under Advanced Filters

   1. Key: data.operationName
   2. Values:

      1. "Microsoft.Compute/virtualMachines/start/action"
      2. "Microsoft.Compute/virtualMachines/deallocate/action"
      3. "Microsoft.Compute/virtualMachines/powerOff/action"

## [Setting Up Environment Variables using user-data (Only POC)](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#setting-up-environment-variables-using-user-data-only-poc)

Info

Only works with OPSWAT Marketplace Images that are prepared to handle user-data

This option is the default and recommended mechanism to automate the licensing management when using the Azure Marketplace Image, as this is the easiest way to activate and deactivate the product when running a single VM of MetaDefender Core

When passing as environment variables to the user-data the LICENSE_KEY it will set up the automation that will activate the product when the instance is started and will deactivate the product when the instance is terminated or stopped.

It is also recommended to indicate the APIKEY environment variables as this will set up the APIKEY to the admin user to be able to make requests to the MetaDefender Core API. In vm scale set deployment types it will help to manage all the instances with the same APIKEY when hitting the Load Balancer.

## [Licensing when running in Kubernetes](/docs/mdcore/v5.22.0/cloud-deployment/licensing-automation-on-azure#licensing-when-running-in-kubernetes)

The licensing automation options when the MetaDefender products are installed in a Kubernetes cluster, are explained in [Licensing in K8S](/docs/mdcore/v5.22.0/container-deployment/licensing-in-k8s)
