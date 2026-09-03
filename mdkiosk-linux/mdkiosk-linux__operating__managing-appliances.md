<!-- source: https://www.opswat.com/docs/mdkiosk-linux/operating/managing-appliances -->

# Managing Appliances

Managing Kiosks can solely be done from the connected management server.

This guide will explain similar data displayed between the management server options and provide access to the management server user guide for more information.

---

## [Dashboard](/docs/mdkiosk-linux/operating/managing-appliances#dashboard)

- [My OPSWAT - Kiosk Dashboard](https://docs.opswat.com/product-management/operating/kiosk-dashboard)
- [Central Management - Kiosk Dashboard](https://docs.opswat.com/ocm/integrations/metadefender-kiosk-linux-dashboard)

**Processing Overview** displays the total number of Sessions, Files Processed, Threats/Files with Issues, and files where active content was detected by Zero-Day Protection & Proactive DLP across all Kiosk appliances connected.

This section also includes graphs showing processed file numbers over time, as well as a graph showing average session time and files per session.

**Resource Overview** allows administrators to get a quick visual of the status of Kiosks.

In **My OPSWAT**, status is shown as an aggregate of Kiosks:

- **Kiosk Health**

  - *Operational* - instances with no current issues
  - *Critical Issues* - instances with an error that prevents their usability

    - Engines are not ready (e.g. engine failure, engine package missing...)
    - License issue (e.g. expired, missing...)
    - Managed File Transfer connection error (e.g. MFT misconfiguration, connection error...)
  - *Unknown* - instances that have not reported in a long time and counted as Disconnected
- **Kiosk Last Seen**

  - Time since Kiosks were last seen
- **Kiosk Version**

  - Versions of Kiosks connected

Hovering the mouse cursor over each bar will display the number of Kiosks within the selected bar.

In **Central Management**, status is shown per instance:

- **Last seen**

  - *Warning* is shown when the instance was last seen for 10 minutes or more
  - *Error* is shown when the instance was last seen for an hour or more
- **Version**

  - The current version of the instance
- **System**

  - *Stable* - instance is up and ready for use
  - *Not Good* - there is an error with the instance that prevents its usability

    - Engines are not ready (e.g. engine failure, engine package missing...)
    - License issue (e.g. expired, missing...)
    - Managed File Transfer connection error (e.g. MFT misconfiguration, connection error...)
- **Engines**

  - The current status of engines

---

## [Inventory](/docs/mdkiosk-linux/operating/managing-appliances#inventory)

- [My OPSWAT - Instance Dashboard](https://docs.opswat.com/product-management/configuration/instance-dashboard)
- [Central Management - Inventory](https://docs.opswat.com/ocm/integrations/changing-metadefender-kiosk-linux-configuration)

### [Instances](/docs/mdkiosk-linux/operating/managing-appliances#instances)

Viewing the list of instances shows high level status of all the Kiosks connected:

**Status** - `Connected` if Kiosk has been seen within 24 hours, `Disconnected` if Kiosk has not been seen within 24 hours

**Health Status** - health status of the Kiosk appliance, status types and potential messages for each status:

- `Operational / Stable` - Kiosk is in a `Healthy` state and ready for use
- `Warning` - Kiosk is in a state that prevents sessions from completing successfully:

  - `Failed to connect to Managed File Transfer`
- `Critical` - Kiosk is considered to be down and needs immediate attention to allow use:

  - `Engines are not ready`
  - `Failed to download license`
  - `Volume license expired/revoked`

**Instance Name** - name of the Kiosk set during onboarding. The instance can be renamed by clicking on `Rename Instances` in My OPSWAT or the edit icon next to the name in Central Management.

**Version** - Kiosk version of the instance

**Configuration** - version of group config settings the Kiosk has in My OPSWAT

**IP** - IP address of the Kiosk identified by My OPSWAT

**Group / Set Name** - name of the `Group` (in My OPSWAT) or `Set` (in Central Management) this instance belongs to

**License** - expiration date of the Volume license

**Last Report Name** - name of the last scan report uploaded to Central Management

**Last Seen** - amount of time since the Kiosk last checked in

**Last Report** - amount of time since the last scan report was uploaded

### [Deleting Instances](/docs/mdkiosk-linux/operating/managing-appliances#deleting-instances)

Click on the checkbox to the left of an instance’s name to select the instance. After one or more instances are selected you can use the `ACTIONS` dropdown to delete the selected instances.

---

## [Combining Kiosks in a Group or Set](/docs/mdkiosk-linux/operating/managing-appliances#combining-kiosks-in-a-group-or-set)

Kiosks can be combined into a Group (in My OPSWAT) or a Set (in Central Management) to provide easier management for multiple Kiosks. Configuration can be edited once for a Group/Set and then applied to all instances within.

Refer to the specific product management user guide for details on how to use Groups and Sets:

- [My OPSWAT - Product Groups](https://docs.opswat.com/product-management/configuration/add-a-product-group)
- [Central Management - Product Sets](https://docs.opswat.com/ocm/operating/product-set)
