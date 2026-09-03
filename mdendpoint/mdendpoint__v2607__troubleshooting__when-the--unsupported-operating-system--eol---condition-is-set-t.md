<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/when-the--unsupported-operating-system--eol---condition-is-set-t -->

# When the "Unsupported Operating System (EOL)" condition is set to Warning, does MetaDefender IT Access account for ESU licenses when determining EOL status?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows systems.

No. OPSWAT does **not check** if a device has an ESU license. EOL detection is based **only on Microsoft’s official end-of-support list**, not on extended servicing agreements like ESU.

> **Support:**
>
> If you have any further questions, concerns or issues regarding **MetaDefender** **Endpoint** , please open a [**Support Case**](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s/).
