<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-to-use-authorized-devices -->

# How to use Authorized Devices?

This article applies to the current MetaAccess NAC Enforcer, the MetaAccess Web UI, and a range of supported network equipment.

MetaAccess NAC’s **Authorized Devices** feature provides the functionality to define an initial **RADIUS Enforcement Role** to devices when they first join the network.

Following initial authorization, MetaAccess NAC has the functionality to change **RADIUS Enforcement Roles** based on policy decisions as and when you configure them.

To make use of the **Authorized Devices** feature and define an initial **Enforcement Role**, if required, please follow the instructions below.

1. Navigate to the **NAC** **Dashboard>Configuration>RADIUS>Configuration>Roles**, as illustrated below, to ensure that a role is defined.
2. If a role is not defined, you can create one by clicking the **New Enforcement Role** button, selecting the role’s **Name, Attributes**, **Operator** and **Value**, and then clicking **Done**.

3. Once all required roles are defined, navigate **Dashboard>Configuration>RADIUS>Device Authorization**

4. Click “Bulk Upload”, then “Download template”, to download a spreadsheet where **MAC -> Role** mappings an be defined.

5. After populating the spreadsheet with these mappings, save it, then use “Select File” and “Upload” buttons above to import the mappings into the NAC

Support:

If you have further inquiries, concerns or issues **Using Authorized Devices In NAC**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
