<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi -->

# What is the difference between "Engine Current Status" and "Engine Advanced Configuration" export options?

This article applies to all MetaDefender Core v5.15.1 releases deployed on Windows and Linux systems.

## [Overview](/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi#overview)

In the 5.15.1 version of MetaDefender Core, a new option for exporting called "Engine advanced configuration" was introduced

Unlike the older Engine Current Status export, which only provided the basic operational state of engines (such as enabled or disabled), the new Engine Advanced Configuration export gives you full visibility into all engine-level parameters, including custom detection rules, logging levels, and module configurations.

---

## [Export Options Explained](/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi#export-options-explained)

### [1. Engine Current Status](/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi#1-engine-current-status)

- Purpose: Exports the basic operational state of each engine (enabled/disabled).

Example Export Config:

HtmlCopy{
"engine": {
"engine_status": {
"name": "Engine status",
"status_list": [
{
"engine_id": "emsisoft_1_windows",
"status": 1
},
{
"engine_id": "ikarus_1_windows",
"status": 0
}
]
}
}
}

Emsisoft Engine Enabled Example:

Ikarus Engine Disabled Example:

---

### [2. Engine Advanced Configuration](/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi#2-engine-advanced-configuration)

- Purpose: Exports all custom and detailed settings per engine.

Avira Engine Export Config:

HtmlCopy{
"engine":{
"engine_config":{
"full_name":"engine.engine",
"name":"EngineConfiguration",
"schema":"engine",
"table": "engine",
"values": {
"3": {
"configuration": "{\"config\":{\"engine.avira_1_windows.config\":{\"values\":{\"detect_all_types\":true,\"enable_pup_scan\":true,\"enable_pup_scan.enable_pup_infected\":false,\"extract_archive\":true,\"extract_archive.max_extract_archive_file_size\":1073741824,\"extract_archive.max_extract_archive_recursion_depth\":200,\"heuristic_scan\":3,\"log_level\":2}}},\"config-serial\":1,\"schema-version\":6}",
"engine_prototype": "avira_windows",
"engine_type": "av",
"instance_id": "1",
"pin_database": "0",
"pin_engine": "0",
"schema": "{\\"product\":{\n\"display_name\":\"Avira\",\n\"id\":\"avira_1_windows\"\n},\n\"schema\":[\n{\n\"default_value\":true,\n\"display_name\":\"Alltypesdetection\",\n\"id\":\"detect_all_types\",\n\"info\":\"Scanallmalwaretypes\",\n\"type\":\"bool\"\n},\n{\n\"default_value\":true,\n\"display_name\":\"DetectPUP/PUA\",\n\"fields\":[\n{\n\"default_value\":false,\n\"display_name\":\"ReturnInfectedresultforPUP/PUA\",\n\"id\":\"enable_pup_infected\",\n\"info\":\"Whenthecheckboxischecked,theresultsofthe\\\"DetectPUP/PUA\\\"shallbemarkedasinfected.\",\n\"type\":\"bool\"\n}\n],\n\"id\":\"enable_pup_scan\",\n\"info\":\"Scanforunwantedsoftware\",\n\"type\":\"feature\"\n},\n{\n\"default_value\":false,\n\"display_name\":\"Extractarchivefile\",\n\"fields\":[\n{\n\"default_value\":1073741824,\n\"display_name\":\"Maxscansize(byte)\",\n\"id\":\"max_extract_archive_file_size\",\n\"info\":\"Themaximumsizeforanyfilewithinanarchive(0meansunlimited)\",\n\"max\":9223372036854775807,\n\"min\":0,\n\"type\":\"number\"\n},\n{\n\"default_value\":200,\n\"display_name\":\"Maxrecursiveextraction\",\n\"id\":\"max_extract_archive_recursion_depth\",\n\"info\":\"Themaximumnumberofarchivesinsidethearchivetobeextracted\",\n\"max\":1000,\n\"min\":0,\n\"type\":\"number\"\n}\n],\n\"id\":\"extract_archive\",\n\"info\":\"Extractarchivefilewhenscanning\",\n\"type\":\"feature\"\n},\n{\n\"default_value\":1,\n\"display_name\":\"Heuristicscan\",\n\"id\":\"heuristic_scan\",\n\"info\":\"Analyzefileusingtheheuristicmethod\",\n\"infos\":[\n\"Disable\",\n\"Lazy\",\n\"Normal\",\n\"High\"\n],\n\"labels\":[\n\"Disable\",\n\"Lazy\",\n\"Normal\",\n\"High\"\n],\n\"type\":\"select\",\n\"values\":[\n0,\n1,\n2,\n3\n]\n},\n{\n\"default_value\":3,\n\"display_name\":\"Loglevel\",\n\"id\":\"log_level\",\n\"info\":\"Therecommendedsettingisinfo.Onlyusedebugandtracefortroubleshooting.\",\n\"infos\":[\n\"Trace\",\n\"Debug\",\n\"Info\",\n\"Warning\",\n\"Error\",\n\"Critical\",\n\"Disable\"\n],\n\"labels\":[\n\"Trace\",\n\"Debug\",\n\"Info\",\n\"Warning\",\n\"Error\",\n\"Critical\",\n\"Disable\"\n],\n\"type\":\"select\",\n\"values\":[\n1,\n2,\n3,\n4,\n5,\n6,\n7\n]\n}\n],\n\"version\":6\n}\n"
}
}
}
}
}

Avira Engine Advanced Configuration UI:

---

### [Can I Export Both?](/docs/mdcore/v5.21.0/knowledge-base/what-is-the-difference-between--engine-current-status--and--engi#can-i-export-both)

Yes, both options can be exported individually or together, depending on your needs. This provides flexibility to retain the engine’s operational status and advanced configuration for backup/restoring purposes.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
