<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/archive-compression-engine-permanently-failed-on-metadefender-co -->

# Archive Compression Engine Permanently Failed on MetaDefender Core v4

Starting from MetaDefender Core version 5.0.0, we have a new archive compression engine to handle archive sanitization feature on MetaDefender Core v5 whenever you have Deep CDR licensed, and in order to support customers not to use another product license when upgrading to v5, so we had to make a change on all existing MetaDefender Core v4 license keys to include this engine.

As a result, in MetaDefender Core v4 instances, when you have Deep CDR licensed, then you will have archive compression engine downloaded but that engine is not supported on Core v4, so it will become permanently failed (which is expected). However, that behavior does not cause any impact to MetaDefender Core v4 processing flow nor impact to performance.

For whom has implemented your own health-check mechanism for engine status check, to avoid being alerted for archive compression engine failure on Node, then please do following to disable that engine on MetaDefender Core v4:

#### [Retrieve exact engine ID of archive compression engine](/docs/mdcore/troubleshooting/archive-compression-engine-permanently-failed-on-metadefender-co#retrieve-exact-engine-id-of-archive-compression-engine)

- `GET /stat/nodes`
- `apikey` header is required
- No payload in request

For example:

#### [Disable archive compression engine based on retrieved engine ID](/docs/mdcore/troubleshooting/archive-compression-engine-permanently-failed-on-metadefender-co#disable-archive-compression-engine-based-on-retrieved-engine-id)

- `POST /admin/engine/<compression_engine_id>/disable`
- `apikey` header is required
- `<compression engine id>` should be the actual retrieved value above
- No payload in request

For example:

After that, the Node on MetaDefender Core v4 will no longer report issue with this engine, and using `GET /stat/nodes` will no longer include archive compression engine in the JSON repsonse.

Note

When you later upgrade to MetaDefender Core v5 from v4, then you might need to manually re-enable "Archive Compression" engine on the product UI to make it active and running on MetaDefender Core v5.
