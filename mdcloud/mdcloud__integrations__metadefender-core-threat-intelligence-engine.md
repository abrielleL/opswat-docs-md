<!-- source: https://www.opswat.com/docs/mdcloud/integrations/metadefender-core-threat-intelligence-engine -->

# MetaDefender Core Threat Intelligence Engine

## [Usage](/docs/mdcloud/integrations/metadefender-core-threat-intelligence-engine#usage)

MetaDefender Core can be configured to communicate with MetaDefender Cloud via the Threat Intelligence Engine. The engine uploads files to MetaDefender Cloud where two actions can be performed:

- Multiscanning with 20+ engines
- Sandbox Dynamic Analysis

Every workflow rule can be configured to send infected files to a special section called quarantine where the malware detected is pinned for future reference and where Threat Intelligence is performed. See [MetaDefender Core's Quarantine documentation](https://www.opswat.com/docs/mdcore/configuration/quarantine) on how to enable sending files to quarantine.

MetaDefender users have the ability to request another analysis report from MetaDefender Cloud for quarantined files by hitting the cloud button on the upper right corner.

The file is automatically uploaded and scanned, and the results are displayed when clicking on the file and selecting the "Threat intelligence results" tab:

For enabling the engine, users need to make sure you have the "Threat Intelligence" module properly configured. It can be found in the "Modules” panel:

## [Use Cases](/docs/mdcloud/integrations/metadefender-core-threat-intelligence-engine#use-cases)

It is often the case that certain files still cannot be trusted even after performing multiscanning. It could be that only a small number of engines detected the file as infected, or the file was detected as “Suspicious”.

In such cases, a second opinion is very valuable. MetaDefender Cloud has a set of engines that is different from MetaDefender packages (see the [licensing page](https://metadefender.opswat.com/licensing) for the full list) and can return more accurate results compared to MetaDefender Core packages with up to 20 engines.

In cases where multiscanning is not enough to detect malware, Sandbox Dynamic Analysis can be used to perform extensive analysis on the file in search of unknown threats.

## [Settings](/docs/mdcloud/integrations/metadefender-core-threat-intelligence-engine#settings)

- Before using the engine, the MetaDefender Cloud apikey needs to be pasted in the settings. The apikey can be found on the OPSWAT [profile page](https://id.opswat.com/profile/licenses)
- Sandbox analysis can also be configured. Users have the ability to select the:

  - Operating system that will be used to scan the files
  - Timeout: short or long analysis
  - Browser
