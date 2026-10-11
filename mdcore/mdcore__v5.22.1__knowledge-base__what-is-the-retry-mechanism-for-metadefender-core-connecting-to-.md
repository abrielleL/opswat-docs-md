<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-is-the-retry-mechanism-for-metadefender-core-connecting-to- -->

# What is the retry mechanism for MetaDefender Core connecting to the remote Postgres Database?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

MetaDefender Core will automatically attempt to reconnect to the remote PostgreSQL database server in the event of a failure. The retry mechanism is configured to initiate a new attempt every 500 milliseconds, continuing until either a 180,000 millisecond timeout is reached or a maximum of 120 retries is completed.

Support:

If **Further Assistance** is required then please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
