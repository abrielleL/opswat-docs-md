<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr -->

# How to check whether AV engines are running the latest update from the OPSWAT update server?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**ℹ️ Check Your Version:** This article applies to all MetaDefender Core versions. The Health Check outdated threshold mentioned in the Recommendation section requires MetaDefender Core 5.21.0 or later.

## [Overview](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#overview)

This article explains how to confirm that the antivirus (AV) engines on MetaDefender Core are running the latest engine and definition (database) packages published on the OPSWAT update server. Use it when you need to verify update status beyond the engine status shown in the web console, for example after a failed update or when building monitoring and alerting.

The check has two parts:

1. Read what is installed on MetaDefender Core using the Engines Status API.
2. Compare it against the latest packages published by OPSWAT in the MetaDescriptor file.

## [Prerequisites](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#prerequisites)

- A MetaDefender Core API key (or session ID) with permission to call `GET /stat/engines`.
- Network access to `update.dl.opswat.com` from the machine where you download the MetaDescriptor file. In offline environments, download the file on an internet-connected machine.

## [Steps](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#steps)

### [Step 1: Check the installed packages with GET /stat/engines](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#step-1-check-the-installed-packages-with-get-statengines)

1. Call `GET /stat/engines` on MetaDefender Core (see the [Engines Status API documentation](https://www.opswat.com/docs/mdcore/metadefender-core#enginesstatus)). For example:

curl -H "apikey: <YOUR_API_KEY>" http://<CORE_HOST>:8008/stat/engines

2. For each engine, note these fields:

   - `def_time` — the timestamp of the definition (database) package currently installed.
   - `download_time` — the time MetaDefender Core downloaded the **engine** package. This is not the download time of the definition package, which is updated more often than the engine itself.
   - `eng_ver` — the version of the engine package currently installed.
3. Compare `def_time` with your expected update frequency. If it is older than expected, continue to Step 2 to confirm whether a newer package is available.

**Note:** When an update check completes successfully but no newer package is available, neither `def_time` nor `download_time` changes. Both fields describe the package currently installed, not the result of the most recent update check. On their own, they cannot confirm that the installed packages are the latest published by OPSWAT.

### [Step 2: Compare against the latest packages published by OPSWAT](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#step-2-compare-against-the-latest-packages-published-by-opswat)

1. Download the MetaDescriptor file from `http://update.dl.opswat.com/metadescriptor`.
2. Find the entry for the engine using its `engine_id`. Example (values are for illustration only):

engine_id: bitdefender_1_linux
engine_type: av
engine_package_version: 3.0.1.399-2537
engine_url: package/bitdefender_1_linux/bitdefender_1_linux-engine-1784748762-1784748769.yml
database_package_version: 7.101529
database_url: package/bitdefender_1_linux/bitdefender_1_linux-database-1789740974-1789741035.yml

3. Identify the latest packages:

   - `engine_package_version` — the latest engine package.
   - `database_package_version` — the latest definition (database) package.
4. To find when a package was released on the OPSWAT update server, read the first Unix timestamp in its URL. In the example above, `1789740974` in `database_url` corresponds to 2026-09-18 14:16:14 UTC.
5. Compare the published values with the values installed on MetaDefender Core (from Step 1).

### [Interpret the results](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#interpret-the-results)

| Result | Meaning |
| --- | --- |
| `def_time` is the same as or later than the release time of the latest database package | The engine is running the latest definitions. |
| `def_time` is earlier than the release time of the latest database package | A definition (signature) update is pending. |
| Installed engine version differs from `engine_package_version` | An engine update is pending. |

If an update is pending for longer than your update frequency, check the update source and frequency settings, network or proxy access to the OPSWAT update server, and whether the engine is pinned to a specific version.

## [Recommendation](/docs/mdcore/knowledge-base/how-to-check-whether-av-engines-are-running-the-latest-update-fr#recommendation)

For monitoring and alerting, combine all three signals:

- **Health Check outdated threshold** ([Health Check API](https://www.opswat.com/docs/mdcore/v5.21.0/metadefender-core#healthcheck), version 5.21.0 or later) as a coarse alarm for outdated engines.
- `def_time` from [Engines Status](https://www.opswat.com/docs/mdcore/metadefender-core#enginesstatus) (`GET /stat/engines`) to track the age of installed definitions.
- **MetaDescriptor comparison** to confirm the installed packages match the latest versions published by OPSWAT.

**ℹ️ Support:** If you need further assistance, please [log a support case or chat with our support engineers](https://my.opswat.com/support).
