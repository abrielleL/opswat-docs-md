<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/release-notes/sbom-release-notes -->

# SBOM release notes

## [v4.9.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v491)

Release date: 8/27/2026

- Complete transitive dependency inventory - dependency results now include non-vulnerable packages found in your dependencies' dependencies.
- SPDX packages without a purl reference are now detected.
- Validation failures now report a reason.

## [v4.9.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v490)

Release date: 8/6/2026

- Add criticality and end-of-life (EOL) detection when scanning CycloneDX and SPDX reports.
- Improve component detection accuracy for CycloneDX reports missing a bom-ref or purl field.
- Add package description for PHP, Ruby, JavaScript, Python, Java, and NuGet packages.

## [v4.8.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v481)

Release date: 7/9/2026

- Fixed an issue where SBOM failed when scanning files with dependency detection enabled.

## [v4.8.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v480)

Release date: 6/30/2026

- Add support for Julia and R programming languages in source code scanning.
- Improve scanning speed by up to 20% for container mode.
- Improve accuracy of OS package version reporting.
- Provide more complete vulnerability results when scanning SPDX 3.0.1 reports.

## [v4.7.2](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v472)

Release date: 4/23/2026

- Support scanning of SPDX 3.0.1 reports.
- Support scanning of CycloneDX 1.4 reports.
- Add support for Kotlin.
- Add support for frequent update
- Add support for structured property

## [v4.7.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v471)

Release date: 3/12/2026

- Support scanning of CycloneDX 1.7 reports.
- Add support for TypeScript, CoffeeScript, Scala, Groovy, and Clojure.

## [v4.7.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v470)

Release date: 2/10/2026

- Support European Union Vulnerability Database (EUVD).

## [v4.6.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v460)

Release date: 1/29/2026

- Add support for EPSS scoring.
- Support multiple severity sources.
- Preserve report metadata when scanning CycloneDX and SPDX reports.

## [v4.5.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v450)

Release date: 12/22/2025

- Add support for scanning .csproj files.
- Integrate GHSA as a source for malicious package detection.
- Enhance CVSS scoring logic to accept scores from multiple sources.
- Introduce Database v6 with a reduced size and improved efficiency.

## [v4.4.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v440)

Release date: 11/4/2025

- Support CIS Level 2 for Windows Server 2022.
- Enhance dependency detection of package.json (npm).
- Return CVSS Score.
- Enhance detection for application files.
- Add support recent malicious NPM packages.
- Reduce database file size.

## [v4.3.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v430)

Release date: 9/2/2025

- A faster way to detect package information for Python.
- Improve the UI to display more details.
- Return the latest version information.
- Add support for several CVEs.
- Support Ubuntu 24.04 and Windows Server 2025.

## [v4.2.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v420)

Release date: 7/8/2025

- Provide more license information: license URL, category, permissions, conditions, limitations.
- Return unique identifier, checksum, property (archive, executable) for a package.
- Add support for composer.json (PHP).
- Support Amazon Linux 2023, Ubuntu 22.04 CIS level 2.

## [v4.1.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v410)

Release date: 5/22/2025

- Return "Authors" and "Release date" info for packages.
- Support processing SPDX file format.
- Support parsing composer.lock file (for PHP).

## [v4.0.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v401)

Release date 3/27/2025

- Fixed an initialization issue on RH8 and Debian 11.

## [v4.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v40)

Release date 3/20/2025

- Improvements for C/C++ libraries

  - Utilize PE information to detect DLL/EXE libraries.
  - Add more signatures for C/C++ libraries.
- Support processing CycloneDX file format.
- Improve Python detection methods.

## [v3.1.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v310)

Release date 1/14/2025

- Improve license detection.
- Better way to handle internal databases.

## [v3.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v30)

Release date: 11/4/2024

- Detect vulnerability for binary C# files.
- Support more file types for the other programing languages.
- Improve Maven license detection.
- Improve engine initialization time.
- Improve JAR file detection.

## [v2.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v21)

Release date: 8/28/2024

- Support SPDX and CycloneDX reports (requires MetaDefender Core V5.11.1+).
- Fix several issues when running multiple threads.

## [v2.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v20)

Release date: 7/8/2024

- Support license risk detection (requires MetaDefender Core V5.10.1+).
- Improve the method to compare package versions.

## [v1.2.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v121)

Release date: 4/15/2024

- Fix initialization failure in non-English environments.

## [v1.2](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v12)

Release date: 4/1/2024

- Support recursive dependency checks for source code.
- Return CWE info.
- Detect vulnerabilities in version ranges.
- Fix detection issues in case of CRLF line endings.

## [v1.1.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v111)

Release date: 1/9/2024

- Return fixed versions for CVEs.
- Support more file names: C/C++ package manager file (`conan.lock`)
- Add package detection for`pom.properties` and `[package_name]-[package-version].jar`.

## [v1.1](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v11)

Release date: 12/06/2023

- Release Linux version
- Support log configuration
- Improve Node, Python detection

## [V1.0.6](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v106)

Release date: 10/25/2023

- Improve processing speed.
- Enhance tar extraction to get layer ids properly.

## [V1.0](/docs/mdcore/v5.22.0/release-notes/sbom-release-notes#v10)

Release date: 10/9/2023

- SBOM engine for MetaDefender Core Windows
- Support source code and container scan
- Support 11 programming languages
