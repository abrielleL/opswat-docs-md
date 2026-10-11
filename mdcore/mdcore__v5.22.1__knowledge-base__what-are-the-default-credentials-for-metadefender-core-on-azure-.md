<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-are-the-default-credentials-for-metadefender-core-on-azure- -->

# What Are the Default Credentials for MetaDefender Core on Azure Marketplace VM?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to OPSWAT MetaDefender Core instances deployed on Azure virtual machines using the MetaDefender Core image available in the Azure Marketplace.

### **Issue:**

After deploying a test virtual machine in Azure using the OPSWAT MetaDefender Core image, you are unable to access the MetaDefender Core web console because you do not know the default username and password.

### **Resolution:**

The default login credentials for the OPSWAT MetaDefender Core Azure Marketplace image are:

- **Username:** `admin`
- **Password:** `instance-id` of the deployed Azure VM

### **How to Retrieve the Instance ID**

You can obtain the instance ID (used as the password) using either of the following methods:

#### **Option 1: PowerShell Script in Azure Cloud Shell**

HtmlCopy$GetVM = Get-AzVM
Foreach ($vm in $GetVM)
{
$vmId = ""
$vmId = $vm.VMid
$vmIdList += $vmId + "rn"
}
Write-Output $vmIdList

Make sure to run the script in the same subscription where the MetaDefender Core VM is deployed.

#### **Option 2: Azure Resource Explorer Portal**

In **Azure Resource Explorer** ([Resource Explorer](https://resources.azure.com/)), you can navigate to:

1. **Microsoft.Compute** > **virtualMachines**.
2. Select the specific **VM**.
3. Look for the `"vmId"` under the `"properties"` section.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
