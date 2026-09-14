<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/auto-sync-using-metadefender-kiosk -->

# Auto-Sync Using MetaDefender Kiosk

MetaDefender Kiosk, v4.8.0 and above, supports direct integration with MetaDefender Drive. When a MetaDefender Drive is connected to a Kiosk, it automatically uploads stored scan reports to the enrolled My OPSWAT Central Management. This feature removes the need for separate SDK installation and configuration, and can be enabled from the Configuration page of a MetaDefender Kiosk.

Follow the steps to get the integration work.

1. In MetaDefender Kiosk, go to server **Config page --> Configuration --> Integrations**
2. Set the **Enable Drive Integration** to be **ON**

For more info, please refer to the MetaDefender Kiosk documentation ([*Windows*](https://www.opswat.com/docs/mdkiosk)) ([*Linux*](https://www.opswat.com/docs/mdkiosk-linux)).

3. On a running Kiosk (that has the integration enabled), insert MetaDefender Drive (that has been enrolled)
4. Wait for it to be detected and wait until the sync progress start then finish

5. Safely remove the MetaDefender Drive
