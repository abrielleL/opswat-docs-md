<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors- -->

# Where can I find sample logs for quarantine errors?

This article applies to all MetaDefender Core v5 releases deployed on Windows and Linux systems.

## [Overview](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#overview)

When configuring a SIEM solution to parse specific logs, administrators may need to reference the exact error lines associated with quarantine errors. These errors are often difficult to reproduce intentionally. To assist with this, sample log outputs are provided for common quarantine-related error codes.

Reference: Error Message Description Table – OPSWAT Documentation

---

## [Sample Logs by Error ID](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#sample-logs-by-error-id)

### [Error ID 1182: Error occurred quarantining file](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#error-id-1182-error-occurred-quarantining-file)

HtmlCopy10.40.50.231 May 27 10:22:44 daemon err 2025-05-27T03:22:44Z LE11-D1R5KLN3 MSCW[15604] Error adding new file to quarantine, file_id='e12ccfae3d58cbf874b122e4bbe8bf96bfd0b8d4874e56b6ed0d8823d3e2e79e', data_id='05c793857bea467e9b206060a9573c85', reason='Force exception path' [msgid: 1182]
### [Error ID 1185: Error reading file in quarantine](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#error-id-1185-error-reading-file-in-quarantine)

HtmlCopy10.40.50.231 May 27 11:07:14 daemon err 2025-05-27T04:07:14Z LE11-D1R5KLN3 MSCW[26524] Can't open quarantined file, fileId='09f414597c14cbfbfc2689a32e135b4dec11882d8d8ec7ebcfd73edd58cff0af', owner='transferquarantinedfile__2171213cb80', path='/non/existent/path/to/force/failure' [msgid: 1185]
### [Error ID 1186: Error writing data to quarantined file](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#error-id-1186-error-writing-data-to-quarantined-file)

HtmlCopy10.40.50.231 May 27 10:39:03 daemon err 2025-05-27T03:39:03Z LE11-D1R5KLN3 MSCW[21584] Error adding data to quarantined file, fileId='09f414597c14cbfbfc2689a32e135b4dec11882d8d8ec7ebcfd73edd58cff0af', owner='1898921464864', reason='Forced error for testing' [msgid: 1186]
### [Error ID 1188: Could not finalize quarantined file](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#error-id-1188-could-not-finalize-quarantined-file)

HtmlCopy10.40.50.231 May 27 10:54:00 daemon err 2025-05-27T03:54:00Z LE11-D1R5KLN3 MSCW[6400] Error finalizing file, fileId='e12ccfae3d58cbf874b122e4bbe8bf96bfd0b8d4874e56b6ed0d8823d3e2e79e', owner='1841321109408' [msgid: 1188]

---

## [Usage](/docs/mdcore/knowledge-base/where-can-i-find-sample-logs-for-quarantine-errors-#usage)

- Use these samples to test SIEM parsing configurations.
- Map `msgid` values to error IDs for correlation.
- Validate log ingestion, alerting, and reporting workflows without reproducing real error conditions.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
