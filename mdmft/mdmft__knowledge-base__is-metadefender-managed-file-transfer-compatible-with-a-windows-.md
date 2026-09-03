<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows- -->

# Is MetaDefender Managed File Transfer compatible with a Windows Server 2022 system that has been hardened according to CIS Level 2 Benchmarks?

Summarize Page    Connect to Cursor Connect to VS Code

**Yes. OPSWAT has validated MFT on both the AWS-provided Windows Server 2022 CIS Level 2 image** ***and*** **on a manually hardened WS2022 + separate SQL Server 2022 environment. In both cases, MFT runs as expected—provided you observe a few general and environment-specific considerations.**

---

During functional testing, no issues were encountered, and MFT operated as expected.

### [Important Considerations](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#important-considerations)

While testing was successful, it is important to note that:

- Custom policy modifications made beyond the standard CIS Level 1 hardening may affect MFT's behavior.
- Variations in security settings, network configurations, or additional system hardening could introduce compatibility issues depending on your specific environment.

### [Recommendation](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#recommendation)

To ensure optimal performance and compatibility, we recommend performing validation testing with your hardened Windows Server 2021 system before deploying MFT to production. This will help confirm that all MFT functions operate correctly within your customized security environment. If you require support during your PoC or have questions regarding MFT compatibility with hardened systems, please proceed to log a support case or chatting with our support engineer.

## [General Considerations](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#general-considerations)

- **Administrator rights** MFT installer/upgrade must run elevated. After setup, drop back to least-privilege service accounts.
- **Custom hardening** Any deviation from the baseline CIS L2 profile (GPO, firewall, registry tweaks, etc.) may impact MFT’s behavior—always test.
- **Port planning** Reserve your MFT web port (default 8010) and SQL port (static, non-default) up front, then open only those in your host firewall.
- **TLS / Encryption** Configure and validate TLS on SQL (Force Encryption = Yes + server cert) before installing MFT.
- **Validation testing** Run a short PoC on your hardened host to confirm that core workflows (upload, download, share, scan) function normally.

---

## [Environment-Specific Details](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#environment-specific-details)

### [A. AWS-Provided CIS L2 Image](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#a-aws-provided-cis-l2-image)

- **Tested image** Amazon Windows Server 2022 CIS Level 2 (v3.0.0 profile)
- **Results** No functional issues encountered during OPSWAT’s standard test suite.
- **Watch-outs**

  - Any additional security agent or custom GPO may require rule exceptions
  - Confirm that AWS-managed updates don’t override your port or service-account settings

### [B. Manually Hardened WS2022 + SQL Server 2022](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#b-manually-hardened-ws2022--sql-server-2022)

#### [1) Scope, Versions & Assumptions](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#1-scope-versions--assumptions)

- **OS**: Microsoft Windows Server 2022 (member server) — CIS Benchmark v3.0.0, Level 2 profile.
- **DB**: Microsoft SQL Server 2022 — CIS Benchmark v1.2.0, Level 2 (Database Engine).
- **App**: OPSWAT MetaDefender Managed File Transfer (MFT). Defaults: web service port **8010** if free; supports Windows Authentication to SQL; Windows service may require enabling “log on as a service” post‑install when using Windows Auth.

#### [2) Install & Hardening Runbook (order of operations)](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#2-install--hardening-runbook-order-of-operations)

1. **Harden OS first (CIS L2)** — apply WS2022 GPO baselines, with pre‑approved exceptions in §3.1.
2. **Choose and reserve ports** in advance:

- SQL Server **static** non‑default TCP port (e.g., 14xxx) — avoid dynamic ports.
- MFT web port (default 8010 or a designated alternative).
- Create host firewall rules accordingly (program + port).

3. **Configure SQL Server TLS** before app install (server certificate, Force Encryption = Yes).
4. **Install MFT** (as local/domain admin), then complete least‑privilege post‑install steps in §4.
5. **Finalize SQL hardening** (disable/rename SA, hide instance, error log retention, etc.).

#### [3) Exceptions to CIS & Compensating Controls](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#3-exceptions-to-cis--compensating-controls)

#### [3.1 Windows Server 2022 (Member Server)](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#31-windows-server-2022-member-server)

**Finding A:** MFT Service user needs Administrator rights for install / upgrade. **Compensation:** Follow guidelines in §4 to drop to least-privilege baseline after Installation is completed.

#### [3.2 SQL Server 2022](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#32-sql-server-2022)

- **2.11:** Use static non‑default port; configure pre‑install.
- **2.13/2.14/2.16:** Disable/rename SA; ensure no login named sa.
- **3.1:** Windows Auth preferred; SQL Auth acceptable with vaulting and strong password.
- **4.1/4.2:** Password expiration may be exempted for service accounts with compensating controls.
- **5.1:** Set error log file limit (≥12).
- **2.12:** Hide instance.
- **7.4:** Enable TLS for SQL connections.

#### [4) MFT on Windows Auth — Least Privilege Steps](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#4-mft-on-windows-auth--least-privilege-steps)

1. Create a **domain standard user** in AD; map to SQL login.
2. Install MFT as admin; post‑install, run service as standard user with **Log on as a service**.
3. SQL permissions:

- Install: db_creator on MFT DB only.

4. Configure port reservations if needed.
5. Grant NTFS Modify on MFT folders only.
6. Adjust shortcuts for config changes.
7. Firewall: program‑scoped inbound rules for MFT executables; restrict to chosen ports and subnets.

#### [5) Authentication Choices](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#5-authentication-choices)

- **Windows Auth:** CIS‑preferred; no DB secrets; requires SPN care.
- **SQL Auth:** Use long, random password (30–64 chars), vault storage, rotation plan.

#### [6) Network & Porting Plan](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#6-network--porting-plan)

- **SQL Server:** Static TCP port (non‑1433), Hide Instance = Yes; allow inbound only from MFT host.
- **MFT Web:** Default 8010; restrict inbound to reverse proxy/user subnets; prefer TLS.
- **Firewall:** Program + port rules; remote IP scoping; enable logging.

#### [7) **Additional Notes**](/docs/mdmft/knowledge-base/is-metadefender-managed-file-transfer-compatible-with-a-windows-#7-additional-notes)

- During testing, certain local-config firewall rules were relaxed — document any deviations for audit.
- Ensure your patch management process preserves all GPO and firewall baselines.
