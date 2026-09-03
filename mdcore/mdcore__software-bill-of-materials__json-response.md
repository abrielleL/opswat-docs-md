<!-- source: https://www.opswat.com/docs/mdcore/software-bill-of-materials/json-response -->

# JSON response

Source code:

- If the "Enable dependency check for source code" option is not enabled, please ignore all "dependencies" attributes

JsonCopy{
"final_verdict":{//the aggregated section for both direct and dependent libs
"blocked": "<boolean>", //true: found CVEs that have severities are higher than the configured threshold, otherwise it is false
"verdict": "<string>",
//<"No Vulnerabilities Found" | "Vulnerabilities Found" | "License Risk Found"> //explaination
"verdict_explanation": ["<string>"],
"vulnerable_package_count": "<int>", //total direct and dependent vulnerable libs
"total_package_count": "<int>", //total direct and dependent libs
"vulnerability_counts":{ // total unique direct and dependent vulnerabilities
"critical": "<int>", //total critical CVE
"high": "<int>", //total high CVE
"medium": "<int>", //total medium CVE
"low": "<int>", //total low CVE
"unknown": "<int>" //total unknown CVE, do not know the severity
},
"severity": "<string>", //highest CVE severity from direct and dependent libs
"dependencies_severity": "<string>", //show if enable dependency detection
"licensing_package_counts": {
"allowed": "<int>",
"blocked": "<int>",
"unknown": "<int>",
"unsupported": "<int>"
},
},
"other_report_formats": [ // report types that could be exported
"cyclonedx",
"spdx"
],
"overview_report": {
"author": {
"name": "OPSWAT Inc.",
"tool": "SBOM <version string>" // SBOM version
},
"scan_mode": "source_code", //source code or container
"severity": "<string>", //the highest CVE severity from the direct libs
"is_partial_report": "<boolean>", //if yes, please download the full SBOM report to see all packages info, by default, this JSON only returns 100 package info
"package_count": "<int>", //total direct libs
"vulnerable_package_count": "<int>", //total direct vulnerable libs
"vulnerability_count": "<int>", //total direct vulnerabilities
"vulnerability_counts":{ //direct vulnerabilities
"critical": "<int>",
"high": "<int>",
"medium": "<int>",
"low": "<int>",
"unknown": "<int>"
},
"dependencies_vulnerability_count": "<int>", //total vulnerabilities from the dependent libs
"dependencies_package_count": "<int>", //total dependent libs
"vulnerable_dependencies_package_count": "<int>", //total vulnerability in the dependent libs
"dependencies_severity": "<string>", //highest CVE severity from the dependent libs
"dependencies_vulnerability_counts":{
"critical": "<int>",
"high": "<int>",
"medium": "<int>",
"low": "<int>",
"unknown": "<int>"
},
"packages": [//package details
//the below JSON is the info of one package, including the dependencies info of the package
{
"uid": "<string>",
"ecosystem": "<string>", //e.g. npm, pypi, maven, julia, r, ...
"group": "<string> ['lang_pkg']",
"package_name": "<string>",
"package_version": "<string>",
"release_date": "<string>",
"target": "<string>", //the input file name (e.g. pom.xml, requirements.txt, Project.toml, renv.lock, report.spdx.json)
"vulnerabilities": [
{
"aliases": ["<string>"],
"id": "<string>",
"severity": "<string>",
"source": "<string>", //vulnerability data source; for SPDX 3.0.1 report scans, results are merged from both the report and SBOM database
"cwes": ["<string>"],
"epss": {
"date": "<string>",
"percentile": "<float>",
"score": "<float>"
},
"ratings": [
{
"method": "<string>",
"score": "<float>",
"severity": "<string>",
"source": {
"name": "<string>"
}
}
],
"fixed_versions": "<string>", //all fixed version > installed version
"type": "<string>, ['vuln', 'potential_vuln']" //potential_vuln is returned when the libs in the input is not clearly defined, i.e: http-client: >2.0
}
],
"vulnerability_counts": {
"critical": "<int>",
"high": "<int>",
"low": "<int>",
"medium": "<int>",
"unknown": "<int>"
},
"archive": "<boolean>",
"authors": "<string>",
"latest": {
"release_date": "<string>",
"version": "<string>"
},
"update_frequency": {
"label": "<string>"
},
"url": "<string>",
"dependencies_package_count": "<int>",// all detected dependencies for this package
"dependencies":
[ //empty if disable
{
"package_name": "<string>", // only show if there is a vulnerability
"package_version": "<string>",
"ecosystem": "<string>",
"vulnerabilities": [
{
"id": "<string>",
"severity": "<string>",
"cwes": ["<string>"],
"source": "<string>",
"fixed_versions": "<string>",
"type": "<string>", ["vuln", "potential_vuln"]
}
],
"vulnerability_counts": {
"critical": "<int>",
"high": "<int>",
"medium": "<int>",
"low": "<int>",
"unknown": "<int>"
}
}
],
"dependencies_severity": "<string>",
"dependencies_vulnerability_counts": { // the aggregated result of the vulnerable libs, empty if disable or no dependencies detection
"critical": "<int>",
"high": "<int>",
"low": "<int>",
"medium": "<int>",
"unknown": "<int>"
}
}
]
}
}

Container:

JsonCopy{
"final_verdict":{
"blocked": "<boolean>",
"verdict": "<string>",//<"No Vulnerabilities Found" | "Vulnerabilities Found">
"verdict_explanation": ["<string>"],
"vulnerable_package_count": "<int>",
"total_package_count": "<int>",
"vulnerability_counts":{
"critical": "<int>",
"high": "<int>",
"medium": "<int>",
"low": "<int>",
"unknown": "<int>"
},
"severity": "<string>"
},
"scan_mode": "container",
"os_info": {
"os_name": "<string>",
"os_version": "<string>"
},
"steps": [
{
"step": "<int>",
"command": "<string>",
"sha256": "<string>",
"severity": "<string>",
"vulnerability_count": "<int>",
"packages": [
{
"arch": "<string>",
"ecosystem": "<string>",
"epoch": "<string>",// epoch of the OS package (e.g. "1"); empty string if not applicable
"group": "<string>", // ["os_pkg"]
"os_name": "<string>",
"os_version": "<string>",
"package_name": "<string>",
"package_version": "<string>", // base version (e.g. "3.0.7"); full version is epoch:version-release
"release": "<string>", // release of the OS package (e.g. "18.el9_2"); empty string if not applicable
"vulnerabilities": [
{
"id": "<string>",
"severity": "<string>",
"source": "<string>",
"cwes": ["<string>"],
"fixed_versions": "<string>"
}
],
"vulnerability_counts": {
"critical": "<int>",
"high": "<int>",
"low": "<int>",
"medium": "<int>",
"unknown": "<int>"
}
},
{
"ecosystem": "<string>",
"group": "<string>", // ["lang_pkg"]
"package_name": "<string>",
"package_version": "<string>",
"vulnerabilities": [
{
"id": "<string>",
"severity": "<string>",
"source": "<string>",
"cwes": ["<string>"],
"fixed_versions": "<string>"
}
],
"vulnerability_counts": {
"critical": "<int>",
"high": "<int>",
"low": "<int>",
"medium": "<int>",
"unknown": "<int>"
}
}
]
}
]
}
