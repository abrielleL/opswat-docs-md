<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/does-metaaccess-timeout-sessions--if-so--how-long- -->

# Does MetaDefender IT Access timeout sessions? If so, how long?

This article applies to the current MetaDefender IT-OT Access Console.

Yes, the **MetaDefender IT Access** **Console** prompts users to extend their session at the nine minute inactivity mark, before timing out at 10 minutes. The session timeout length can be configured on Settings > Account > Account Session Timeout.

OPSWAT always recommends that application builders implement short idle session timeouts for applications that handle high-risk data.

For this reason, OPSWAT has included this additional proactive security measure to the MetaDefender IT Access Console.

- MetaDefender IT Access Console users will be prompted to extend their session after **9 minutes** of idle session time.
- If there is still no activity after **10 minutes**, MetaDefender IT Access will log the user out and force them to initiate a fresh session when they wish to continue.

Support:

If you have further queries, concerns or issues regarding **MetaDefender IT Access** **Session Timeout And Period**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
