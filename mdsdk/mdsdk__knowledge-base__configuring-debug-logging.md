<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/configuring-debug-logging -->

# Configuring Debug Logging

## [Overview](/docs/mdsdk/knowledge-base/configuring-debug-logging#overview)

OESIS includes a built-in diagnostic logging facility that can be enabled at initialization time. By default, the SDK does not produce any log output. This keeps runtime overhead minimal for normal operation. When you need to investigate an issue, you can turn on full diagnostic logging by using one of two approaches:

| Approaches | Mechanism | Best for |
| --- | --- | --- |
| `config_debug` | JSON object passed to `wa_api_setup` at initialization | Programmatic integrations where you control SDK startup parameters |
| `v4Debug.dat` | File placed in the SDK deployment directory | Quick enablement without code changes; field troubleshooting |

Both methods share the same configuration parameters and produce the same log output.

## [When to Use This](/docs/mdsdk/knowledge-base/configuring-debug-logging#when-to-use-this)

Enable `config_debug` when:

- You're troubleshooting unexpected SDK behavior
- OESIS Support has asked you to collect diagnostic logs
- You're validating a new integration and want visibility into what the SDK is doing under the hood

You do not need `config_debug` for normal production use, omitting it disables debug logging entirely.

## [How It Works](/docs/mdsdk/knowledge-base/configuring-debug-logging#how-it-works)

### [Approach 1: config_debug (Programmatic)](/docs/mdsdk/knowledge-base/configuring-debug-logging#approach-1-config_debug-programmatic)

Add a `config_debug` object to the JSON payload passed to `wa_api_setup`. Place it at the **top level**, alongside `config`, not nested inside it. For example:

json_configCopy{
"config": { ... },
"config_debug": {
"debug_log_output_path": "C:\\Logs\\OESIS",
"debug_log_file_size": 10,
"debug_log_folder_size": 200,
"debug_log_count": 20,
"debug_log_time": 72
}
}

**Log Output Files**
Depending on the`log_mode`, the SDK generates files with the following prefixes:

- ***Encrypted Mode:***`v4DebugInfo_[epoch]_[tickcount]_P[pid].log`
- ***Plaintext Mode:***`v4PlainTextDebugInfo_[epoch]_[tickcount]_P[pid].log`

Note

Simply including the `config_debug` key, even as an empty object `"config_debug": {}`, automatically activates debug logging using the SDK's defaults.

### [Approach 2: v4Debug.dat (File-Based)](/docs/mdsdk/knowledge-base/configuring-debug-logging#approach-2-v4debugdat-file-based)

Please prefer to: [How do I configure v4Debug.dat for enhanced logging?](/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging)

Important

If `v4Debug.dat` is present, **the SDK uses that configuration instead**, and it overrides whatever is passed in `config_debug` through `wa_api_setup`. If your `config_debug` settings don't seem to be taking effect, check whether `v4Debug.dat` file exists.

## [Recommended Configuration](/docs/mdsdk/knowledge-base/configuring-debug-logging#recommended-configuration)

For most troubleshooting scenarios, we recommend setting only these categories of options and leaving everything else at its default. This ensures the widest possible diagnostic coverage, nothing gets filtered out that might turn out to be relevant.

### [1. Output location](/docs/mdsdk/knowledge-base/configuring-debug-logging#1-output-location)

| Key | Type | Description |
| --- | --- | --- |
| `debug_log_output_path` | string | Directory where log files will be written. If omitted, logs are written in the directory containing SDK binaries (`libwautils.dll`, `libwautils.dylib` or `libwautils.so`) |

### [2. Retention](/docs/mdsdk/knowledge-base/configuring-debug-logging#2-retention)

These settings control how much disk space logging is allowed to consume, so debug logging can safely be left running without filling up storage.

| Key | Type | Unit | Default (omitted) | Min | Description |  |
| --- | --- | --- | --- | --- | --- | --- |
| `debug_log_file_size` **(1)** | number | MB | 5 | 5 | Maximum size of a single log file before it rotates |  |
| `debug_log_folder_size` **(2)** | number | MB | 100 | 100 | Maximum total size of the log directory |  |
| `debug_log_count` | number | files | 0(no limit) | 20 **(3)** | Maximum number of rotated log files to retain |  |
| `debug_log_time` | number | hours | 72 | 72 | Also rotate the log after this many hours, regardless of file size |  |

**Notes:**

- All upper bounds are `INT_MAX`. No explicit upper limit is enforced, values are constrained only by the maximum value supported by the `int` data type.
- Input values below the specified minimums are accepted but automatically clamped to the corresponding minimum values without generating an error or warning.
- **(1)** For `v4PlainTextDebugInfo_*.log` files, the rotation size is **fixed at 5 MB**. Any value provided in `debug_log_file_size` is ignored for plaintext logs.
- **(2)** If `debug_log_folder_size` is set **below** `debug_log_file_size`, it's automatically raised to `debug_log_file_size + 5`.
- **(3)** `debug_log_count` = `0` **means no limit** (count-based deletion is disabled entirely). The minimum of 20 only applies if you set a value between **1 - 19**.

**Note on Cleanup Logic** (`debug_log_folder_size`, `debug_log_count`, `debug_log_time`):

- These three retention conditions are **OR'd**. Whichever threshold is reached first will trigger the deletion of the oldest log files to free up space.

**Warning**

Automatic cleanup policies apply **only to encrypted logs** (`v4DebugInfo_*.log`).
If you enable `log_mode: "plaintext"` or `"all"`, you must monitor the cleanup process to prevent disk space exhaustion.

### [3. Log format](/docs/mdsdk/knowledge-base/configuring-debug-logging#3-log-format)

| Key | Type | Description |
| --- | --- | --- |
| `log_mode` | string | Controls which log file(s) are produced: `encrypted`, `plaintext`, or `all` |

If `log_mode` is omitted (or is set to an unrecognized value), it defaults to `“encrypted"`. Encrypted logs are safe to leave on for extended periods but only OESIS team can decrypt them.

If you need to review the log contents yourself, set `log_mode` to `"plaintext"` or `"all"`.

**Note on Plaintext Mode:**

- When `log_mode` is set to `"plaintext"`, all other configuration fields are **ignored**, **except for** `debug_log_output_path`.
- OESIS automatically redacts sensitive information (such as passwords, auth tokens, and keys) from the logs to ensure compliance with privacy standards for plaintext logs.

Trade-off

Plaintext logs omit some information that encrypted logs capture, which can make it harder to pinpoint the root cause of an issue. If you're sending logs to OPSWAT for investigation, `encrypted` (or `all`, which produces both) gives Support Team the most complete picture.

## [Optional: Narrowing the Scope](/docs/mdsdk/knowledge-base/configuring-debug-logging#optional-narrowing-the-scope)

The following keys let you limit ***what*** gets logged.

Recommendation

Since the goal of debug logging is usually to capture a complete picture of an issue, **we recommend leaving these keys below unset** unless you already know exactly what you're looking for. Narrowing scope risks missing the very entry you need.

| Key | Type | Description |
| --- | --- | --- |
| `debug_log_level` | string | Limits verbosity. Accepts `OFF`, `DEBUG`, `ERROR`, `FATAL`, `INFO`, `WARNING`, `TRACE`, or `ALL`. Leave unset (or use `ALL`) to capture everything. |
| `debug_log_components` | array<string> | Limits logging to specific components: `CORE`, `SETUP`, `TEARDOWN`, `INVOKE`, or `ALL`. |
| `debug_log_signatures` | array<number> | Limits logging to specific signature IDs. |
| `debug_log_methods` | array<number> | Limits logging to specific method IDs. |

## [Example: Minimal Recommended Setup](/docs/mdsdk/knowledge-base/configuring-debug-logging#example-minimal-recommended-setup)

JsonCopy{
"debug_log_output_path": "C:\\Logs\\OESIS",
"debug_log_file_size": 10,
"debug_log_folder_size": 200,
"debug_log_count": 20,
"debug_log_time": 72
}

This configuration:

- Writes logs to `C:\Logs\OESIS`.
- `log_mode` is absent, so mode stays **encrypted**.
- Per-file rotation: Each file rotates just under **10 MB**.
- Cleanup deletes oldest files when total size of all `v4DebugInfo_*` files exceeds **200 MB**, or the count reaches or exceeds **20**.
- Any `v4DebugInfo_*` file whose creation time is more than **72** hours ago is deleted.
- Captures all components, levels, signatures, and methods, since none of the narrowing options are set

## [**How to Verify It's Working**](/docs/mdsdk/knowledge-base/configuring-debug-logging#how-to-verify-its-working)

After calling `wa_api_setup`, follow these steps to confirm logging is active:

1. **Check the Output Directory:** Navigate to your `debug_log_output_path` (if set), or SDK binaries directory. A new file with the prefix `v4DebugInfo_` (or `v4PlainTextDebugInfo_`) should appear within seconds of SDK initialization.
2. **Check File Size:** If the file exists but is 0 KB, ensure the SDK has performed at least one operation (like an `invoke`) to generate content.

### [**Troubleshooting "No Log File"**](/docs/mdsdk/knowledge-base/configuring-debug-logging#troubleshooting-no-log-file)

If no file is generated, verify the following:

- **Permissions:** Ensure the application process has **Write** permissions for the target directory.
- **JSON Structure:** Confirm `config_debug` is at the **top level** of your JSON object, alongside `config`, not nested inside it.
- **Override Check:** Check if a `v4Debug.dat` file exists in the working directory. If it does, the SDK will ignore your programmatic `config_debug` settings in favor of the file.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
