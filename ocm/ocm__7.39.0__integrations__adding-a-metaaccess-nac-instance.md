<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/adding-a-metaaccess-nac-instance -->

# Adding a MetaAccess NAC instance

The following guideline describes how to add a MetaAccess NAC instance to OPSWAT Central Management.

Info

The OPSWAT Central Management server must have been registered with a license that provides MetaAccess NAC support in order to manage MetaAccess NAC instances.

1. Follow the [MetaAccess NAC deployment guide](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213483564/VM+Deployment+Guide) up to the **Configure Appliance Network Settings** step.
2. For the **Enter License Key** step, instead of following the aforementioned guide, enter OPSWAT Central Management's OPSWAT Agent recovery key into the **License Key** field and fill out the **OPSWAT Central Management URL (Optional)** field with the correct server address.

OPSWAT Central Management's OPSWAT Agent recovery key is located at **Settings > Global Settings > Account.**

3. Select **Register License Key** and complete the deployment. On success, the MetaAccess NAC instance should then be managed by OPSWAT Central Management.

- **Port**: The unique identification assigned to each MetaAccess NAC instance. An OPSWAT Central Management license with MetaAccess NAC support specifies a limited number of ports that can be assigned to MetaAccess NAC instances.

Info

The status of the MetaAccess NAC instance is **Connected** after fetching its version successfully.
