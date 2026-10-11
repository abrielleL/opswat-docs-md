<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-i-can-t-push-configuration-due-to-password-storage- -->

# Why I can't push configuration due to password storage?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to versions OCM 7.x, Core 5.11 and above on both Windows and Linux platforms.

**Introduction**:

This knowledge base article provides details regarding Core Versions in OCM

Details:

If you have older versions of MD Core connected to OCM that do not have the Password Storage feature and you upgrade to a version that has the feature, you must remove the Core from OCM and re-add the core for the settings to take effect. Otherwise, you will receive the following error when you try to push the set settings:

""err": "Invalid item for type: rule", "err_details": {"errors": [{"error":"Contains none-existing item","key":"archive.archive_ handling.password_storage.storage","value":[1737987671157]}], "name": "Email Policy - Default"}"

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
