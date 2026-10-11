<!-- source: https://www.opswat.com/docs/mdcore/configuration/policy-configuration -->

# Policy Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The MetaDefender Core server can be configured to use different scanning profiles for different clients. The selection is based on the client's source IP address.

In case multiple scanning profiles are configured for the given client, the client can choose which one to use. If a client does not have a scanning profile specified, MetaDefender Core uses the first matching profile from the Workflow rules.

All configuration options related to the policies are found under the **Policy** menu.

## [How Policies Work](/docs/mdcore/configuration/policy-configuration#how-policies-work)

A policy is pairing a *user* with a *workflow template* based on a workflow *rule*.

Users can be grouped into *zones* based on their network address.

Workflow templates can be created/modified to change how file scanning is carried out.

Creating a policy means creating a rule, where a source zone will be paired with a workflow template.

## [How a file scan is processed via the REST API](/docs/mdcore/configuration/policy-configuration#how-a-file-scan-is-processed-via-the-rest-api)

When MetaDefender Core receives a scan request through the REST API it will match the source address through the zones in the list of rules and apply the first matching rule's workflow. The processing request then will then be processed based on this specific workflow.

If a workflow is provided by the REST request it still should be one which has a matching rule. Otherwise the scan request will fail.

## [How a file scan is processed on the web UI](/docs/mdcore/configuration/policy-configuration#how-a-file-scan-is-processed-on-the-web-ui)

When MetaDefender Core receives a scan request through the web UI it will match the source address through the list of rules. The user will be able to select only those workflows with a matching rule. This scan request then will then be processed based on the workflow selected by the user.
