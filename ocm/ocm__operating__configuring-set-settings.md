<!-- source: https://www.opswat.com/docs/ocm/operating/configuring-set-settings -->

# Configuring Set settings

Set settings allow users to unify all OPSWAT Product instances in the same Set under the same settings for their product type. The Set settings are derived from a specific instance's settings.

The following guideline describes how to create Set settings and apply it to a Set of OPSWAT Product instances in OPSWAT Central Management.

1. In **Set View,** click on the Set that needs to be configured.
2. Choose the product instance that Set settings should be derived from by clicking on the gear icon and select **Choose as Set settings** from the drop-down menu.

Confirm before choosing this instance as your set settings

3. Select **VIEW SET SETTINGS** to view and modify the current Set settings. In the newly opened page, select **APPLY SET SETTINGS** to apply it to all currently connected product instances in the Set.

Warning

Set settings will overwrite the individual settings of the OPSWAT Product instances in the set. You can choose which instance to apply set's settings.

Warning

Set settings are only applied to valid instance (for both Disconnected and Connected status)with the same version with this set. The users will need to reapply set settings for Set members that were disconnected when Set settings are applied or are newly added.

Warning

Certain set settings such as MetaDefender Core's **Restrict access to following roles** require that the selected objects- such as the user roles in this case- are available in all instances belonging to the set. If one or more instances do not have the selected objects, the set settings application process may fail.

Please refer to [Set settings could not be applied to product instances, such as MetaDefender Core](/docs/ocm/troubleshooting/failed-to-apply-core-set-settings) for more information.
