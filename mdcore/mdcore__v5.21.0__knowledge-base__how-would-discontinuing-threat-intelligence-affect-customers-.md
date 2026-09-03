<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-would-discontinuing-threat-intelligence-affect-customers- -->

# How would discontinuing Threat Intelligence affect customers?

- **Status**: The legacy Threat Intelligence engine in MetaDefender Core has already been deprecated, and its successor is now in development.
- **Legacy functionality**: The former engine functioned as a free utility for on-demand analysis of quarantined files, helping teams validate suspected threats after containment.
- **What’s changing**: The new engine embeds advanced machine-learning threat pattern correlation directly in MetaDefender Core and works in sync with Sandbox to deliver zero-day detection; the discontinued quarantine-analysis workflow will not return.

Upon renewal, you may see this engine become “Unlicensed” when you activate a new license key. This simply happens because the engine is already deployed, but the new activation key doesn’t include it anymore. You can simply ignore this status or just delete the engine package.

Functionality wise, you can still use directly from the quarantine section by leveraging our Adaptive Sandbox integration.

For details on how to deploy locally or how to configure a remote sandbox, see here: [Sandbox](/docs/mdcore/v5.21.0/sandbox/overview)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
