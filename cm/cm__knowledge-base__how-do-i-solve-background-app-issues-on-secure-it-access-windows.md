<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-background-app-issues-on-secure-it-access-windows -->

# How do I solve Background App issues on Secure IT Access Windows devices?

> **Check your product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows 10 or 11 systems.

> **Info:**
>
> If you encounter a Secure IT Access connectivity issue accompanied by the error message below, this troubleshooting guide is designed to assist you in resolving the problem as much as possible.
>
> *1. It looks like no background activity is running. Please try again or follow the* ***Troubleshooting Guide*** *to solve your issues. If the problem persists, contact the OPSWAT Support.*
>
> *2. An unexpected error occurs when setting up a connection. Please try again or follow the* ***Troubleshooting Guide*** *to solve your issues. If the problem persists, contact the OPSWAT Support.*

Users running MetaDefender Endpoint on Windows may occasionally see that **Secure IT Access** cannot connect successfully due to **OPSWAT SDP Background App** issue.

An **OSPWAT SDP background app** is expected to launch to start establishing a connection to the selected gateway. However, the Operation System manages directly when and how it starts, so sometimes it does not work as expected, leading to not be able to connect successfully.

To remediate background app issues on your Windows devices, please follow the relevant instructions below.

1. Go to **Add or Remove Programs**
2. Look up **OPSWAT SDP** > **Advanced options.**
3. Background apps permission: **Power Optimized** / **Always.**

![](https://uploads.developerhub.io/prod/1yda/fltnhp3umszuygwy0l8t0cp13p2ql8xw579f47jnlgq5pr2ssa0zg0h4qnbfrwgr.png)

> **Pro Tip:**
>
> We highly recommend to set Background apps permission to **Always**.

4. Click **Terminate** > **Repair** > **Reset**.

![](https://uploads.developerhub.io/prod/1yda/c0ualf6loync8dufzlzstgzt8cqbiiamboyfcspcsbnhsnih2to8bh8w4uyd9j5o.png)

5. Back to MetaDefender Endpoint, then try to sign in and connect again.

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience OPSWAT SDP background app issues**:
>
> 1. **Reboot** your machine and try again.
> 2. Open a [**Support Case**](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
