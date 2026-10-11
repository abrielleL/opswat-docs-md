<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/sandbox/upgrade-to-java-17 -->

# Upgrade to Java 17

View as Markdown Ask ChatGPT about this page Ask Claude about this page Warning

Support for Java 8 and Java 11 for the embedded Aether (Adaptive Sandbox) engine ends in March 2025. Update the Java version on your system to continue receiving engine updates after this date.

## [Upgrade on Windows](/docs/mdcore/v5.22.1/sandbox/upgrade-to-java-17#upgrade-on-windows)

Install the recommended Java version with the MSI installer which is documented on our [system requirements](https://www.opswat.com/docs/mdcore/sandbox/system-requirements) page and restart your machine.

## [Upgrade on Linux](/docs/mdcore/v5.22.1/sandbox/upgrade-to-java-17#upgrade-on-linux)

Install the recommended java package.

Example for Ubuntu 22.04Copysudo apt install openjdk-17-jre
## [Verify the Java version](/docs/mdcore/v5.22.1/sandbox/upgrade-to-java-17#verify-the-java-version)

Make sure that the Java version is correctly updated:

CommandCopyjava -version
openjdk version "17.0.13" 2024-10-15 LTS
OpenJDK Runtime Environment Corretto-17.0.13.11.1 (build 17.0.13+11-LTS)
OpenJDK 64-Bit Server VM Corretto-17.0.13.11.1 (build 17.0.13+11-LTS, mixed mode, sharing)

After installing the correct Java version, the engine should start without errors and warnings.
