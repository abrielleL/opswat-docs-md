<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-are-some-of-my-devices-disappearing-from-the-my-opswat-centr -->

# Why are some of my devices disappearing from the My OPSWAT Central Management console?

My OPSWAT Central Management can be configured to automatically uninstall OPSWAT Client from devices, and remove them from the device inventory (Console>Inventory>Devices) when they have gone unseen for a configured period.

My OPSWAT Central Management can also uninstall and remove devices when they have had no access to cloud applications, or have been non-compliant for a configured number of days.

> **Please Note:**
>
> When a device is removed in this manner, a license token will be freed up for use on a new endpoint device.
>
> When a device is configured to be removed from the inventory without MetaDefender Endpoint being remotely uninstalled, that device will reappear on the inventory as soon as the device reconnects to the server (this is known as a **Temporary Removal**). In cases where the freed device token gets spent following a temporary removal, and that token was the last available token on the account, the reappearing device will be reported as an **Out Of License Usage**.

Each of these actions (remote Client uninstall and device removal, under various conditions) are independently configurable via **My OPSWAT Central Management** **Console>Settings>Global> Endpoint Data**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/1jexdmu1eggt6pf7fbps7ls9ah87opruve0yh9e9nu4j5lqe2skwaydem4qgsi63.png)

As shown above, users can check the appropriate boxes, adjust the period settings, then click **Save** to apply their changes.

> **Support:**
>
> If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
