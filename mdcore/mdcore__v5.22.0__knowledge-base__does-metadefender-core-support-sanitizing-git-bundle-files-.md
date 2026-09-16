<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/does-metadefender-core-support-sanitizing-git-bundle-files- -->

# Does MetaDefender Core support sanitizing GIT-BUNDLE files?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**No,** Deep CDR does **not** support sanitization of Git object formats.

**Explanation:**

GIT-BUNDLE files have a rigid, immutable format with SHA-1/SHA-256 integrity checks and a directed acyclic graph (DAG) structure that cannot be altered without invalidating the bundle.

A git bundle is not just an archive. It’s a serialized pack file containing:

- Git commit objects
- Trees
- Blobs
- Tags
- Objects within a packfile format with SHA-1/SHA-256 integrity
- Protocol metadata

This format is binary, integrity-checked, and extremely rigid. If any object inside changes even a single byte, the checksums break, and Git will reject the bundle.

Even if OPSWAT added Deep CDR support, the output would fail, and a “sanitized” Git bundle would not be a functioning Git bundle anymore.

**Recommendations:**

While Deep CDR sanitization is not supported, the format can still be extracted using Archive Extraction engine, and all the child files should be scanned with Metascan’s AV engines.

After extraction and scanning, if no malware is detected, the original GIT-BUNDLE file can be allowed.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
