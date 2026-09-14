<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/maintaining-sdp-gateways -->

# Maintaining SDP Gateways

After deploying private gateways, Administrators are able to monitor and update their gateways within the My OPSWAT Central Management console. Administrators are able to review health statistics of their individual private gateways, review networking details of those gateways, and update gateway information. In addition, they are also able to request version updates for their private gateways so that the gateways are always up-to-date.

Maintenance activities can be done by navigating to **Secure Access > Access Methods**, selecting a gateway pool, and drilling down to a specific gateway.

![](https://uploads.developerhub.io/prod/97qW/ik7b6vjupzq1stqtbkphgpgpzi7bx8liu9yd7w5umydm1nsygh2mak9cuxigr4rr.png)

## Reviewing gateway health statistics

Using My OPSWAT Central Management Gateway statistics under the **Overview** tab of a particular gateway, Administrators are able to see visual reporting on the health of that gateway. All graphs report in user's local time zone. The page contains three fixed graphs on the following record types:

- CPU Usage (Last 7 Days)
- Memory Usage (Last 7 Days)
- Disk Usage (Last 7 Days)

The page also contains a graph toward the bottom that is customizable. Administrators are able to select the type of record (from the provided list) they want to see reporting on. The graph will transition in real-time, and can be further drilled down using the reporting tool by defining values in fields such as metric, unit, time range, and interval.

All of the graphs mentioned above are also interactive with the customizable graph. By selecting one of the three fixed graphs, the customizable graph will transition to that record type.

## Reviewing networking and gateway information

Under the **Details** tab, Administrators are able to review and update private gateway information such as:

- Name
- Public IP Address
- Private IP Address
- External Tunnel Port
- External Security Port
- Primary and Secondary DNS servers*
- DNS Suffix

![](https://uploads.developerhub.io/prod/97qW/1qir6y525sj5p57n66rdix4rqdqe7jkch6tk3hq0dx7l76gykzebos80ld8lpjcd.png)

This provides Administrators with the ability to change the gateway to a friendly name, customize IP addresses, and provide alternative external ports. When changes are made, the updates are then sent to the Controller to deliver to the gateways affected.

**With Custom DNS, DNS is queried from the Private Gateway's network using the DNS servers specified in the* ***Primary*** *and* ***Secondary DNS server*** *fields. When disabled, the DNS is done from the client device using the device's DNS configuration.*

## Updating gateways

> **Info**
>
> For gateways to update, they are required to be version 1.6.0 or above, must be an approved gateway, and must be reporting healthy in My OPSWAT Central Management.

To perform an update on your Secure IT Access Gateway, please perform the following steps:

- Navigate to **Secure Access > Access Methods > Gateways**
- Select the gateway pool that contains the gateway you wish to update.
- Select the (**⋮**) in the row of the gateway.
- Select **Update**.

This will send an update request from the My OPSWAT Central Management console to the Secure IT Access gateway and attempt to perform the update. You will receive a notification in the admin console if the update is successful.

You can also track the gateway updating process through **Gateway Events** and **Notification Groups**. For more information, please refer to [Audit Gateway Events](https://www.opswat.com/docs/cm/secure-access-solution/audit-gateway-events).
