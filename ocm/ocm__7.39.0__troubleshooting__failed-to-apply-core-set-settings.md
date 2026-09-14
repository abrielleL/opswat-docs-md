<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/failed-to-apply-core-set-settings -->

# Set settings could not be applied to product instances, such as MetaDefender Core

| Type | Detail |
| --- | --- |
| Problem | - You notice that [Set settings](/docs/ocm/7.39.0/operating/configuring-set-settings) were not applied properly to all selected instances. - For certain products such as MetaDefender Core, the affected instance's Config History reports an "import failed" event. |
| Cause | An invalid setting in Set settings, specific to the affected instance, such as:   - For settings related to TLS, the specified TLS certificates do not exist in the affected instances. - For settings related to user roles, the specified user roles do not exists in the affected instances. |
| Troubleshooting | Events such as "import failed" in MetaDefender Core instances' config history. |
| Solution | Correct invalid settings.   - For missing TLS certificates, ensure that they are now present on the affected instances with the correct name. - For missing user roles, ensure that all instances set possess the selected roles. |

After applying [Set settings](/docs/ocm/7.39.0/operating/configuring-set-settings), a MetaDefender Core instance reports "import failed" in its Config History.

This issue may be caused by an invalid Set setting specific to the affected instance, particularly if not all instances are affected. Specifically, possible invalid settings are:

- The Set settings specify a TLS certificate that do not exist on the affected instances, such as in the above example image.

#### [The Set settings specify TLS certificates that do not exist in the affected instances](/docs/ocm/7.39.0/troubleshooting/failed-to-apply-core-set-settings#the-set-settings-specify-tls-certificates-that-do-not-exist-in-the-affected-instances)

This is likely the cause if the "import failed" event mentions an invalid item such as **allow_cert.cert.**

Please check if the certificates specified in the Set settings's **allow_cert.cert** are present in the affected instance with the same name as specified in the Set settings.

In Set settings, allow_cert.cert corresponds to the **Certificate Used for Batch Signing** workflow rule.

In MetaDefender Core dashboard, you can find the available certificates at **Inventory > Certificates** in the left navigation menu. Please rename them to match the Set settings if necessary.

#### [The Set settings specify user roles that do not exist in the affected instances](/docs/ocm/7.39.0/troubleshooting/failed-to-apply-core-set-settings#the-set-settings-specify-user-roles-that-do-not-exist-in-the-affected-instances)

This is likely the cause if the "import failed" event mentions an invalid item such as **scan_allowed .**

Please check if the user roles specified in the Set settings's **scan_allowed** are present in the affected instance with the same name as specified in the Set settings.

In Set settings, **scan_allowed** corresponds to the **Restrict access to following roles** workflow rule.

In MetaDefender Core dashboard, you can find the available user roles in **User Management** **> Roles** tab in the left navigation menu. Please rename them to match the Set settings if necessary.
