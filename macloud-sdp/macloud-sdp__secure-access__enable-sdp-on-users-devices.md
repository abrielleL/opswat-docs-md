<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/enable-sdp-on-users-devices -->

# Enable SDP on end-user devices

Administrators can enable SDP on end-user devices by following one of two methods.

## [Solution 1: Enabling SDP globally](/docs/macloud-sdp/secure-access/enable-sdp-on-users-devices#solution-1-enabling-sdp-globally)

Administrators have the option to turn on SDP for all devices within their MetaDefender IT-OT Access account.

To enable SDP globally:

1. Log into MetaDefender IT-OT Access console
2. Navigate to **Settings > Global > Device Agents**
3. Check off **Enable SDP for all devices**.
4. Save the changes and enter your PIN to confirm.

Within a few minutes after your change, the MetaDefender Endpoint will check in with the MetaDefender IT-OT Access backend servers, note the change, and begin installing SDP for the client devices.

## [Solution 2: Enabling SDP per device group](/docs/macloud-sdp/secure-access/enable-sdp-on-users-devices#solution-2-enabling-sdp-per-device-group)

Administrators can gradually turn on SDP on your organization by utilizing group overrides.

To enable SDP on a device group:

1. Log into MetaDefender IT-OT Access console
2. Navigate to **Inventory > Device Groups**
3. Select a group you would like to enable SDP, and select the **Settings** tab.
4. Toggle on the **SDP** section, and check off **Enable SDP for this group**.

Within a few minutes after your change, the MetaDefender Endpoint will check in with the MetaDefender IT-OT Access backend servers, note the change, and begin installing SDP for the client devices.
