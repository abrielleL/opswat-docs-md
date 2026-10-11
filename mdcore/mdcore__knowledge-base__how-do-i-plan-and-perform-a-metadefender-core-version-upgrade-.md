<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade- -->

# How do I plan and perform a MetaDefender Core version upgrade?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Overview**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#overview)

This article is the complete planning reference for upgrading MetaDefender Core. It covers how to choose the right upgrade path based on your current version, what to prepare before any upgrade, what happens to your database during an upgrade, and how to handle special situations such as End-of-Life versions, large version gaps, and limited disk space. The detailed step-by-step upgrade procedure for each deployment type is maintained in a separate dedicated article, linked from the "Upgrade procedure" section below.

### [**Quick answers**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#quick-answers)

| Question | Answer |
| --- | --- |
| Are version upgrades free? | Yes. The latest version is free for all active license holders to download and run. |
| Are version upgrades automatic? | No. Product version upgrades are always manual. Only feature updates within the product (such as engine updates, which are covered separately) can be set to automatic. |
| What is the latest version? | Check the [Release Notes](https://www.opswat.com/docs/mdcore/release-notes/release-notes), or log in to [My OPSWAT](https://my.opswat.com/home/metadefender-core) -> go to Product Downloads → MetaDefender Core -> click on the Download button. |
| Can I downgrade after upgrading? | No. There is no in-place downgrade. The only rollback path is restoring the snapshot or backup taken before the upgrade. |
| Can I jump directly to the latest version? | It depends on the size of the version gap — see "Choosing your upgrade path" below. |

OPSWAT recommends upgrading to the latest version as soon as practical and not waiting until the end of a release's support cycle. Current versions include the latest features, bug fixes, and security patches, and bug fixes are only ever applied to the next release — never backported to the release you are on.

---

## [**Step 1 — Check your support status (End-of-Life policy)**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#step-1--check-your-support-status-end-of-life-policy)

Before planning any upgrade, confirm whether your current version is still supported.

OPSWAT supports each MetaDefender Core release for **18 months after the publication of the following release**. Versions not listed on the support lifecycle page are no longer supported, and **Version 3 and earlier releases are out of support entirely**.

See: [How long is the support lifecycle for a specific version of MetaDefender Core?](https://www.opswat.com/docs/mdcore/knowledge-base/how-long-is-the-support-life-cycle-for-a-specific-version-releas)

If your current version is **End-of-Life (EoL)**:

- Upgrading from an EoL version is **not a supported upgrade path**. It may still succeed, but it is best-effort only and carries a meaningfully higher risk of database migration failure. Architectural differences accumulate over time — database schema changes, altered data relationships, and third-party dependency updates — and very old versions may not be able to upgrade directly at all.
- Running an unsupported version can cause **engine failures at any time**, independently of any upgrade.
- Installers for very old releases may **no longer be available for download** from My OPSWAT. If an intermediate version you were counting on is unavailable, an incremental upgrade path may not be completable — verify installer availability before committing to that path.
- If in doubt, contact OPSWAT Support for assistance planning the upgrade before you start.

---

## [**Step 2 — Prepare (applies to every upgrade)**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#step-2--prepare-applies-to-every-upgrade)

1. **Review the target version's requirements.** Check the [Recommended System Configuration](https://www.opswat.com/docs/mdcore/installation/recommended-system-configuration) for the version you are upgrading **to**, not the one you are on. Note in particular:

   - **Windows:** Microsoft Visual C++ Redistributable for Visual Studio 2015–2022 (x64), **version 14.44 or later**, is required by current releases. An outdated redistributable will cause the installation to fail.
   - **PostgreSQL:** some MetaDefender Core versions are only compatible with certain PostgreSQL versions. Check the release notes and system requirements of the target version.
2. **Take a snapshot or full backup** of the machine(s) hosting the application and the database (for virtual machines, a disk snapshot; for physical systems, a full backup). This is the only reliable rollback path — there is no in-place downgrade.
3. **Export your configuration** from the Management Console using the built-in Config Export/Import feature (see [Import/Export Configuration](https://www.opswat.com/docs/mdcore/operating/import-export-configuration)). Provided no errors occur during the upgrade, this preserves your configuration and licensing information through the process.

   - Note: a configuration package exported from a much older version may not import successfully into a current release, due to accumulated changes in the configuration schema. For large version gaps, also take screenshots or notes of your workflows, settings, and user management as a fallback for manual reconfiguration.
4. **Export your processing history** if you need it for your records: History > Processing > Export History.
5. **Check available disk space.** Major upgrades can require far more temporary space than the product uses day to day — see "Disk space requirements" below. As a rule of thumb, ensure available free space is **larger than your Core database size**.
6. **Plan a maintenance window.** Database migration time scales with the size of your scan history; a large processing history can extend the upgrade considerably.
7. **MetaDefender Core Custom installations** (installations provided by OPSWAT that include custom engines): contact OPSWAT Support before upgrading for guidance on upgrading the custom engines.

---

## [**Step 3 — Choose your upgrade path**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#step-3--choose-your-upgrade-path)

The deciding factor is the **size of the version gap** between your current version and the target. The wider the gap, the more you should break the upgrade into stages. This applies both when crossing major versions (4.x to 5.x) **and** when spanning many releases within the same major version (for example, 5.12.x to 5.21.x).

| Your situation | Recommended path |
| --- | --- |
| 1–2 releases behind the target | **Path A** — direct upgrade |
| 3 or more releases behind, same major version (e.g. 5.12 → 5.21) | **Path B** — incremental upgrade, 2–3 versions per stage |
| Crossing major versions (4.19 or later → 5.x) | **Path B** — incremental upgrade through an early 5.x release |
| Running version 4.18 or older | **Path C** — clean installation (required; see database note below) |
| Current version is End-of-Life | **Path C** recommended; Path B is best-effort only |
| Historical processing data is not required | **Path C** — regardless of gap size, this is the faster and more reliable route |

**Version-specific notes:**

- **Version 4.18 and older** use a SQLite database, whereas newer versions use PostgreSQL. There is no migration plan for these versions: a complete uninstall and fresh installation is required (Path C). Take screenshots and/or notes of your current settings, user management, and workflows before uninstalling, as they will be lost.
- **Version 4.19 and newer** use PostgreSQL and can follow the incremental path (Path B) or, for small gaps, the direct path (Path A).
- **Version 5.11.1:** upgrade directly to 5.14 or newer.

---

## [**Path A — Direct upgrade (small version gap)**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#path-a--direct-upgrade-small-version-gap)

V5 releases support quick manual installation of the new version directly over the existing installation. Follow the steps in the "Upgrade procedure" section below.

## [**Path B — Incremental upgrade (large version gap)**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#path-b--incremental-upgrade-large-version-gap)

Use this when you need to preserve your existing database and processing history across a large gap.

1. Complete all preparation steps above (snapshot, config export, requirements check).
2. Divide the version gap into stages of roughly **2–3 versions** each. For example, starting from 4.19: 4.19 > 5.0 > 5.2 > 5.4 > 5.6 > 5.8, and so on, continuing in similar steps until you reach a supported version — then upgrade to the latest.
3. At each stage, review the [Release Notes](https://www.opswat.com/docs/mdcore/release-notes/release-notes) to confirm the version you plan to land on is a stable, suitable stopping point, and re-check the system requirements — a version in the middle of your ladder may introduce a requirement (such as a PostgreSQL or Visual C++ Redistributable version) that your host does not yet meet.
4. On older versions you may need to stop the "OPSWAT MetaDefender Core" service before running the installer:

   - **Windows:** stop the service via services.msc. *[IMAGE — reuse from "How to upgrade an End-of-Life [EOL] MetaDefender Core?": Windows services screenshot]*
   - **Linux:** `sudo systemctl stop ometascan`
5. Run the installer for that stage and let the database migration complete fully. **Do not interrupt it** — on a large processing history, a long-running migration is expected behavior, not a hang.
6. After each stage, reboot the machine for the changes to take effect, then verify the deployment is healthy: the Management Console loads, services are running, and engines update successfully.
7. Repeat until you reach the target version.

**Understand the trade-offs before choosing this path:**

- It is time-intensive, and every stage requires validation.
- There is no formal, certified ladder of approved intermediate versions. Choosing the stopping points is done from the release notes on a case-by-case basis.
- If the source version is very old, there is no guarantee the path completes cleanly. It is possible to invest several hours and still end with a database error, at which point a clean installation (Path C) becomes the only remaining option.

## [**Path C — Clean installation**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#path-c--clean-installation)

Use this when: the current version is 4.18 or older, the current version is End-of-Life, the gap is very large and historical data is not required, or an incremental attempt has failed.

1. Export the configuration from Settings, and take screenshots and/or notes of your workflows, settings, and user management (for very old versions, the notes are the reliable record — the export may not import into the new release).
2. Export your processing history for your records: History > Processing > Export History.
3. Take a snapshot or backup of the existing instance.
4. Uninstall the current version.
5. Install the latest MetaDefender Core release with a clean database.
6. Import the configuration package, or reconfigure manually from your notes/screenshots.
7. Validate scanning behavior against the previous configuration before decommissioning anything.

**Trade-off:** you lose historical processing data, and settings may need to be rebuilt manually. In exchange, this is by a wide margin the cleaner, faster, and more predictable route for a large version gap.

---

## [**Upgrade procedure**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#upgrade-procedure)

The full step-by-step upgrade procedure — GUI and command line, for Windows and Linux, in both Standalone and Shared Database modes — is maintained in a dedicated article:

[How do I manually upgrade to the latest MetaDefender Core version?](https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-manually-upgrade-to-the-latest-metadefender-core-versio)

The same procedure applies whether you are performing a direct upgrade (Path A) or one stage of an incremental upgrade (Path B).

---

## [**Why the version gap matters (database migration)**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#why-the-version-gap-matters-database-migration)

The installer does not simply overwrite the previous version — it migrates the database schema forward **one version at a time**, from your current schema version through every intermediate revision to the target. For example, a database at schema version 1 (introduced with 4.19.0) upgrading to schema version 53 passes through all fifty-three steps in a single run.

Two consequences follow:

- **Duration.** The migration can take a long time, and it scales with the volume of scan history stored.
- **Risk.** Every additional schema step is another opportunity for the migration to fail. Failures mid-migration are what make very large single jumps unattractive.

Breaking the upgrade into stages reduces the number of schema transitions applied in any single run — which is exactly why the incremental path is more survivable than one large jump.

### [**Disk space requirements**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#disk-space-requirements)

When upgrading to a much newer version, the process may report requiring **well over 150 GB** of available disk space even if the installation itself only occupies a modest amount (for example, 40 GB). This is because major upgrades may:

- Temporarily **duplicate data** for migration or backup — ensure available free space is larger than the Core database size;
- **Extract and stage** large upgrade packages;
- Create **fallback points** in case the upgrade needs to be rolled back.

If disk space is the barrier, options include:

1. Reduce existing data usage — see [How to manage disk space usage in the pg_data\base directory](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta)
2. Adjust Data Retention settings — see [What can I do when MetaDefender Core (Windows) has an insufficient disk space error?](https://www.opswat.com/docs/mdcore/knowledge-base/what-can-i-do-when-metadefender-core--windows--has-an-insufficie)
3. Move the Temp and Quarantine folders to a drive with more space — see [How can the Temp folder be changed?](https://www.opswat.com/docs/mdcore/knowledge-base/how-can-the-temp-folder-be-changed-)
4. Perform a fresh installation on a new machine with sufficient space (Path C).

If an upgrade has already failed on disk space, collect the following before retrying and attach it to your support case: total and available disk space on all drives, a screenshot of the installation folder Properties, a screenshot of the `data` folder Properties, the upgrade log mentioning the space requirement, and a support package.

---

## [**Version-specific checkpoints**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#version-specific-checkpoints)

Always read the release notes for every version in your upgrade range. Known checkpoints:

- **Weak TLS ciphers (5.13.3 and later):** MetaDefender Core's NGINX web server will not start if weak cipher suites are configured for HTTPS. OpenSSL 1.x has been replaced with OpenSSL 3.x, affecting NGINX and PostgreSQL dependencies. Review and update your SSL/TLS configuration to remove unsupported cipher suites **before** upgrading, or the NGINX service will fail to start post-upgrade.
- **Syslog Server Configuration API (5.13.0 and later):** Syslog settings can be configured via API in addition to the GUI. Existing configurations are unaffected, but changes made through the API require a restart of the MetaDefender Core service to take effect.
- **Visual C++ Redistributable (Windows):** current releases require version 14.44 or later of the Microsoft Visual C++ Redistributable 2015–2022 (x64). Verify before upgrading.
- **PostgreSQL compatibility:** some MetaDefender Core versions are only compatible with certain PostgreSQL versions — check the release notes and system requirements of every target version in your ladder.
- **Version 5.11.1:** upgrade directly to 5.14 or newer.

---

## [**References**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#references)

| Item | Detail |
| --- | --- |
| Upgrade cost | Free for all active license holders |
| Upgrade trigger | Always manual — no automatic product upgrades |
| Recommended increment for large gaps | 2–3 versions per stage |
| Gap rule applies to | Major-version crossings (4.x → 5.x) and wide same-major gaps (e.g. 5.12 → 5.21) |
| Database boundary | 4.18 and older: SQLite (fresh install required); 4.19.0 and newer: PostgreSQL (schema migrated sequentially) |
| Support lifecycle | 18 months after the following release is published |
| Unsupported releases | Version 3 and earlier; any version not listed on the support lifecycle page |
| Windows prerequisite | Microsoft Visual C++ Redistributable 2015–2022 (x64), 14.44 or later |
| Mandatory safeguard | Snapshot or full backup of application and database hosts |
| Rollback method | Restore from snapshot or backup — no in-place downgrade exists |
| Disk space rule of thumb | Free space larger than the Core database size; major upgrades may require 150+ GB temporarily |

---

## [**Notes**](/docs/mdcore/knowledge-base/how-do-i-plan-and-perform-a-metadefender-core-version-upgrade-#notes)

- The incremental path is guidance, not a certified upgrade matrix. OPSWAT does not publish a fixed list of approved intermediate versions; the correct landing points are determined from the release notes for the versions in your specific range.
- Confirm that installers for your chosen intermediate versions are still available on My OPSWAT before starting — an unavailable intermediate build will block the ladder partway through.
- Do not interrupt a database migration that appears to be taking a long time. On a large processing history this is expected behavior, not a hang.
- Testing the upgrade in a staging environment before the production rollout is strongly recommended, especially for large gaps.
- If your current version is End-of-Life, or you are unsure which path applies to your deployment, open a support case before starting.

**Support:** If you have questions, concerns or want to report issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
