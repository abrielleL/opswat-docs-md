<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-is-the-meaning-of-action-ran-and-action-failed-in-json-scan -->

# What is the meaning of action_ran and action_failed in JSON scan result?

This article applies to all MD Core from V4.18 releases deployed on Windows and Linux systems.

Understanding `actions_ran` and `actions_failed` in MetaDefender Core Responses

When you submit a file to *MetaDefender Core (MD Core)* for scanning and sanitization, it may return two specific fields in the JSON response:

- *actions_ran*
- *actions_failed*

These fields indicate which actions were performed successfully and which ones encountered issues during the sanitization process.

---

`actions_ran`: Actions Completed Successfully

This field lists all actions that *successfully ran* on the submitted file.

- Values are returned as a string, with multiple actions separated by a vertical bar `|`.
- An *empty string* indicates that *no action was successfully executed*.

Possible Values

***Sanitized*:***Deep CDR__ARC Compression Sanitization*_**Sanitized Partially:**_

This can occur when:

- Some nested files failed sanitization.
- Some file types were excluded from sanitization (based on configuration).
- The archive contains blocked file types. (*Only shown if the "Distinguish Partial Archive Process Result" option is enabled in Archive Sanitization settings.)*

***Sanitization Skipped*** : The file was skipped from sanitization. Common reasons include the file being digitally signed or other policy-based exclusions.

---

`actions_failed`: Actions That Failed or Were Not Completed

This field lists actions that ***failed or were interrupted*** during processing.

- An *empty string* means *no failure occurred* during sanitization.

Possible Values:

***Sanitization Failed:*** Sanitization was attempted but did not succeed.

***Sanitization Timed Out:*** The sanitization process exceeded the *standard timeout limit* set for the action.

***Sanitization Global Timeout Exceeded:*** The entire scan process exceeded the *global timeout* defined in the Workflow configuration:

- *Workflow > [Workflow name] > Timeouts > Enable global timeout*

***Sanitization Canceled:*** The sanitization process was *manually canceled* by a client or user while in progress.

---

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
