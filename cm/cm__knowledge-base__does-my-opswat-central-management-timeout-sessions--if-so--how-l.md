<!-- source: https://www.opswat.com/docs/cm/knowledge-base/does-my-opswat-central-management-timeout-sessions--if-so--how-l -->

# Does My OPSWAT Central Management timeout sessions? If so, how long?

Yes, the **My OPSWAT Central Management** **Console** prompts users to extend their session at the nine minute inactivity mark, before timing out at 10 minutes. The session timeout length can be configured on Settings >  Global > Account > Inactivity Timeout.

![](https://uploads.developerhub.io/prod/97qW/4zlu6qnoy74htxl7zbgnt4w9ujlgw066bsj6abir5m6og0psxtmrtbd4evnj4r0t.png)

OPSWAT always recommends that application builders implement short idle session timeouts for applications that handle high-risk data.

For this reason, OPSWAT has included this additional proactive security measure to the My OPSWAT Central Management Console.

- My OPSWAT Central Management Console users will be prompted to extend their session after **9 minutes** of idle session time.
- If there is still no activity after **10 minutes**, My OPSWAT Central Management will log the user out and force them to initiate a fresh session when they wish to continue.

> **Support:**
>
> If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
