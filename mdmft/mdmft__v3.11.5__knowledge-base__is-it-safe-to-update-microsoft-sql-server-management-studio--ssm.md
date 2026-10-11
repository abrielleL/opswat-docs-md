<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/is-it-safe-to-update-microsoft-sql-server-management-studio--ssm -->

# Is It Safe to Update Microsoft SQL Server Management Studio (SSMS) on the SQL Instance for an MFT (e.g., from 19.1 to 22.7.2) to Address a CVE?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Check Your Version:**

This article applies to all MetaDefender Managed File Transfer releases.

Yes. SSMS is a client-side management tool, and updating it (for example, from 19.1 to 22.7.2 to address a CVE) is a safe, low-risk change for your MFT environment. It does not affect MFT's database connectivity or functionality.

## [**Why SSMS Is Independent of MFT**](/docs/mdmft/v3.11.5/knowledge-base/is-it-safe-to-update-microsoft-sql-server-management-studio--ssm#why-ssms-is-independent-of-mft)

SSMS is only an administrative GUI used to connect to and manage SQL Server instances. It does not run as a service on the SQL Server, and MFT does not depend on it at runtime.

MFT connects directly to the SQL Server engine (e.g., SQL Server 2016/2017/2019/2022/2025), not to SSMS.

Because MFT never talks to SSMS, upgrading or removing SSMS has no effect on the database engine, the MFT databases, or the application.

**Support:**

If you have questions, concerns or issues regarding **MetaDefender** **Managed File Transfer**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
