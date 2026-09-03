<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/can-workflow-settings-be-updated-globally-across-multiple-workfl -->

# Can Workflow Settings Be Updated Globally Across Multiple Workflows?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

**Description**

Customers managing a large number of workflows often encounter scenarios where they need to **update a specific setting across all or selected workflows**. For example, changing the **file size upload limit** from 30 MB to 300 MB in all workflows, without altering any other configuration parameters.

The Workflow templates page is found under **Policy > Workflow templates** after successful login.

When you click on a workflow template, a window appears displaying various tabs that show different properties related to the template.

Click "Save Changes" to confirm and apply your updates.

For more information regarding different kind of properties of the workflow, please refer to this article: [Workflow Configuration Template](/docs/mdcore/v5.21.0/configuration/workflow-configuration-template)

**Current Capabilities**

*✅* ***Workflow Templates*** __

- Workflow templates are designed to standardize configurations.
- Changes made to a template are propagated to all workflows based on that template.
- This is useful when workflows are intended to share an identical configuration.

*⚠️* ***Limitations of Workflow Templates*** __

- Templates apply a **full configuration**, not selective updates.
- If workflows have unique settings, applying a template will **override all existing configurations**, not just the intended setting.
- Templates **cannot apply partial changes** such as updating only one setting (e.g., file size limit) across all workflows without affecting other parameters.

**Is Partial or Global Update Possible?**

Currently, there is **no built-in feature** to:

- Selectively update one or more parameters across all workflows.
- Apply changes to a group of workflows without affecting unrelated settings.
- Track such partial changes centrally across all workflows.

Workflows must be **updated individually** if they do not share a common template.

**Recommendation for Large-Scale Workflow Management**

- For new deployments, consider grouping workflows under a **template-based structure** to streamline future updates.
- If workflows are highly customized, updating them will need to be done individually or via custom automation using available APIs (if supported).
- For large-scale environments with repetitive update needs, feature enhancement discussions may be warranted.

**Feature Enhancement Possibility**

This use case highlights a potential need for:

- A **centralized management tool** that allows applying a specific configuration change across multiple workflows.
- A method to track such changes in the **configuration history** for auditing purposes.

While this is not currently available, feedback is being collected to help prioritize such capabilities in future product iterations.

**Summary**

| **Question** | **Answer** |
| --- | --- |
| Can I update a single setting across all workflows? | Not directly—this requires individual updates unless workflows share a template. |
| Will changing a template update workflows? | Yes, but it will overwrite the full configuration, not just one setting. |
| s there a way to track changes globally? | Changes are tracked per workflow; no centralized history exists for global changes. |
| Is a more flexible update method planned? | This is a known request and under consideration for future development. |

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
