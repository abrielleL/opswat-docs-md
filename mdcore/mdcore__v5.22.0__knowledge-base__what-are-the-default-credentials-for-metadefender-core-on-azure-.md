<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure- -->

# What Are the Default Credentials for MetaDefender Core on Azure Marketplace VM?

This article applies to OPSWAT MetaDefender Core instances deployed on Azure virtual machines using the MetaDefender Core image available in the Azure Marketplace.

### [**Issue:**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure-#issue)

After deploying a test virtual machine in Azure using the OPSWAT MetaDefender Core image, you are unable to access the MetaDefender Core web console because you do not know the default username and password.

### [**Resolution:**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure-#resolution)

The default login credentials for the OPSWAT MetaDefender Core Azure Marketplace image are:

- **Username:** `admin`
- **Password:** `instance-id` of the deployed Azure VM

### [**How to Retrieve the Instance ID**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure-#how-to-retrieve-the-instance-id)

You can obtain the instance ID (used as the password) using either of the following methods:

#### [**Option 1: PowerShell Script in Azure Cloud Shell**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure-#option-1-powershell-script-in-azure-cloud-shell)

HtmlCopy$GetVM = Get-AzVM
Foreach ($vm in $GetVM)
{
$vmId = ""
$vmId = $vm.VMid
$vmIdList += $vmId + "rn"
}
Write-Output $vmIdList

Make sure to run the script in the same subscription where the MetaDefender Core VM is deployed.

#### [**Option 2: Azure Resource Explorer Portal**](/docs/mdcore/v5.22.0/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure-#option-2-azure-resource-explorer-portal)

In **Azure Resource Explorer** ([Resource Explorer](https://resources.azure.com/)), you can navigate to:

1. **Microsoft.Compute** > **virtualMachines**.
2. Select the specific **VM**.
3. Look for the `"vmId"` under the `"properties"` section.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
