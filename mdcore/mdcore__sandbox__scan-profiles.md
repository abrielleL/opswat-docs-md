<!-- source: https://www.opswat.com/docs/mdcore/sandbox/scan-profiles -->

# Scan Profiles

Scan Profiles are available from Adaptive Sandbox 2.3.0.

When using **MetaDefender Aether for Core (Adaptive Sandbox) Remote** Engine, make sure the connected Standalone Instance is also at least version 2.2.0 for the best results.

## [Analysis Profile](/docs/mdcore/sandbox/scan-profiles#analysis-profile)

This is the default profile for **Remote Aether engines**, designed to perform a comprehensive analysis. It executes an extensive set of tasks to extract the maximum number of Indicators of Compromise (IOCs), ensuring deep visibility into potential threats.

## [Speed Profile](/docs/mdcore/sandbox/scan-profiles#speed-profile)

Optimized for **Embedded Aether engines**, this profile prioritizes rapid verdict delivery. It runs a streamlined set of essential scan tasks to minimize analysis time while still providing reliable threat detection.

## [Feature Comparison](/docs/mdcore/sandbox/scan-profiles#feature-comparison)

| **Scan Task** | **Speed** | **Analysis** |
| --- | --- | --- |
| Early Termination | Yes | No |
| Yara (Basic) | Yes | Yes |
| Yara (All) | No | Yes |
| File visualization | No | Yes |
| File downloads | No | Yes |
| OCR QR | Yes | Yes |
| Extract strings | Yes | Yes |
| Certificates | Yes | Yes |
| OSINT Lookups | Yes | Yes |
| OSINT Lookups (Basic) | Yes | Yes |
| OSINT Lookups (All) | Yes | Yes |
| URL Analysis | No | Yes |
| Phishing detection | No | Yes |
