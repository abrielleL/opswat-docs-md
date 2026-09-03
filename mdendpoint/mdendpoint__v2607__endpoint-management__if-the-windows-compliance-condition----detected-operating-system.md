<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/if-the-windows-compliance-condition----detected-operating-system -->

# If the Windows compliance condition “Detected operating system is not supported by the manufacturer (EOL)” is set to treat as Warning in MetaDefender IT Access, will this prevent a compliant system from logging in or accessing resources?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows systems.

**No.** Changing the severity to *Warning* only affects the **compliance result in the dashboard**. It does **not** block login or device access. As long as other enforced policies are compliant, the device can log in normally.

![MetaDefender IT Access console showing where to configure the “Unsupported Operating System (EOL)” warning behavior.](https://uploads.developerhub.io/prod/2x2P/mswd7zb4zlnq2y3p672h3bkkz5o8djqx9dofc96t76w73y97yvo0g4my2jpn0xa0.png)

> **Support:**
>
> If you have any further questions, concerns or issues regarding **MetaDefender** **Endpoint** , please open a [**Support Case**](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s/).
