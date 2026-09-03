<!-- source: https://www.opswat.com/docs/mdcore/sandbox/advanced-configurations -->

# Configuration

The MetaDefender Aether for Core (Adaptive Sandbox) Engine offers two integration modes:

1. **Inline:** working as a part of MetaDefender Core processing workflow (real-time processing). Allowing users to block entire processing based on MetaDefender Aether for Core engine outcome and decision.
2. **Out of band:** working as a part of MetaDefender Core quarantine (post-investigation processing). Providing additional option to analyze quarantined items along with the existing Threat Intelligence technology.

---

## [Global configuration](/docs/mdcore/sandbox/advanced-configurations#global-configuration)

Go to **Inventory > Modules** and select the **MetaDefender Aether for Core (Adaptive Sandbox)** module

Pro Tip

Use your OPSWAT Reputation secret to further enhance your MetaDefender Aether for Core (Adaptive Sandbox) Engine capabilities.

The global configuration is used by the out of band MetaDefender Core quarantine process and also as the default setting for new workflow configurations.

### [Engine details](/docs/mdcore/sandbox/advanced-configurations#engine-details)

See details like engine version and status.

### [Configuration](/docs/mdcore/sandbox/advanced-configurations#configuration)

#### [Log level](/docs/mdcore/sandbox/advanced-configurations#log-level)

Configure the log level of the Sandbox Engine. In case of issues a lower log level (**Debug**) might help the support team.

#### [Remote server address](/docs/mdcore/sandbox/advanced-configurations#remote-server-address)

Configure the address and secret of your standalone MetaDefender Sandbox instance.

Info

Only available for the Remote Sandbox Engine

#### [OPSWAT Reputation configuration](/docs/mdcore/sandbox/advanced-configurations#opswat-reputation-configuration)

Configure your **OPSWAT Reputation** secret to use the OPSWAT Reputation OSINT scan task.

Info

Only available for the Embedded Sandbox Engine. For the Remote Sandbox Engine the secret must be configured for the standalone MetaDefender Sandbox instance.

#### [OpenAI configuration](/docs/mdcore/sandbox/advanced-configurations#openai-configuration)

Info

Only available for the Embedded Sandbox Engine

#### [Offline Mode](/docs/mdcore/sandbox/advanced-configurations#offline-mode)

Disable online services.

Info

Only available for the Embedded Sandbox Engine

### [Default Analysis configuration](/docs/mdcore/sandbox/advanced-configurations#default-analysis-configuration)

---

## [Workflow configuration](/docs/mdcore/sandbox/advanced-configurations#workflow-configuration)

Go to **Workflow Management > Workflows**, select your workflow and select the **MetaDefender Aether for Core (Adaptive Sandbox)** module

Pro Tip

Customize your workflows based on your specific usage scenario to enhance performance. For example turn off *file types* and update *engine results filtering*.

Setup several workflows tailored to different use cases, if required.

Activate `Rapid mode` when there's a need for higher throughput.

Enable the **MetaDefender Aether for Core (Adaptive Sandbox**) Engine in your workflow

### [Filetype filtering](/docs/mdcore/sandbox/advanced-configurations#filetype-filtering)

Configure the **MetaDefender Aether for Core (Adaptive Sandbox)** Engine to run only for the selected file types. All the supported file types are selected by default.

Warning

It's not recommended to choose file types that aren't included in the default configuration.

### [Engine result filtering](/docs/mdcore/sandbox/advanced-configurations#engine-result-filtering)

Configure the Sandbox Engine to run conditionally based on **Reputation** engine results, **Metascan** AV engine results or **Deep CDR** sanitization results.

### [Advanced options](/docs/mdcore/sandbox/advanced-configurations#advanced-options)

#### [Deep CDR filtering](/docs/mdcore/sandbox/advanced-configurations#deep-cdr-filtering)

Configure the Sandbox Engine to run conditionally based on Active Content(s) found with Deep CDR processing.

#### [Scan timeout](/docs/mdcore/sandbox/advanced-configurations#scan-timeout)

Configure a timeout value in seconds which will be applied to each scan.

Warning

A high timeout value might significantly degrade engine performance

#### [Blocked verdicts](/docs/mdcore/sandbox/advanced-configurations#blocked-verdicts)

MetaDefender Core will block files if the Sandbox Engine produces a blocked verdict.

#### [Scan tasks](/docs/mdcore/sandbox/advanced-configurations#scan-tasks)

Configure which tasks should be executed. Different configuration settings available for the Embedded and Remote Sandbox Engine.

#### [Pre-configured analysis options](/docs/mdcore/sandbox/advanced-configurations#pre-configured-analysis-options)

The following profiles are available in both Engines:

- **Speed:** This mode focuses on generating a final Verdict within the shortest time. It is likely that the list of IOCs is only partially complete.
- **Analysis:** This mode prioritizes extracting the most amount of IOCs over scan time.

#### [Custom analysis options](/docs/mdcore/sandbox/advanced-configurations#custom-analysis-options)

**Embedded Engine**

**Remote Engine**

Warning!

The following options shouldn't be modified for the Remote Sandbox Engine if the *filescan.io* community site is used or **Advanced scanning** option is not enabled for the user.

#### [Executive summary](/docs/mdcore/sandbox/advanced-configurations#executive-summary)

Create an executive summary for the selected verdicts, powered by ChatGPT.

---
