<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-manually-start-the-mft-next-service-if-it-fails-to-start- -->

# How to manually start the MFT Next service if it fails to start automatically?

Summarize Page    Connect to Cursor Connect to VS Code
## [Symptoms](/docs/mdmft/knowledge-base/how-to-manually-start-the-mft-next-service-if-it-fails-to-start-#symptoms)

1. MFT Next service is set to automatic start, but the service isn’t running.
2. Manual start of the service fails with a similar error as below.
3. Windows Event log has error entries that mention, the service failed to start because of missing .NET runtime or ASP.NET runtime.

Manual service start fails

Example event log error

## [Root cause](/docs/mdmft/knowledge-base/how-to-manually-start-the-mft-next-service-if-it-fails-to-start-#root-cause)

Application security solutions may prevent running a .NET runtime version with known vulnerabilities. (e.g. [Microsoft Defender Vulnerability](https://learn.microsoft.com/en-us/defender-vulnerability-management/tvm-block-vuln-apps) )

MFT installation also installs a .NET runtime version that services will try to use. If this version has since been discovered to have vulnerabilities, services will try to use a patched version if installed. When the patched version is also not available, the Next service will fail to start.

## [Resolution](/docs/mdmft/knowledge-base/how-to-manually-start-the-mft-next-service-if-it-fails-to-start-#resolution)

Install the version mentioned in the event log, or the latest available .NET 8 version for

- .NET Runtime
- ASP.NET Core Runtime

[Download .NET 8.0 (Linux, macOS, and Windows) | .NET](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
