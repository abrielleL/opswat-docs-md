<!-- source: https://www.opswat.com/docs/mdcore/predictive-alin-ai/engine-response-structure -->

# Engine Response Structure

#### [**Engine Verdicts**](/docs/mdcore/predictive-alin-ai/engine-response-structure#engine-verdicts)

**Predictive Alin AI** returns standardized verdict codes upon file analysis. These verdicts are consistent across all integrated OPSWAT products and indicate the outcome of the scanning process.

The following verdict values may be returned:

- **0: No Threat Detected -***The file was successfully analyzed and no malicious characteristics were identified.*
- **1: Infected -***The file was analyzed and determined to be malicious.*
- **10: Not Scanned -***The file was not analyzed. This may occur if the file exceeds the supported size limit or if an internal processing error prevents completion of the scan.*
- **23: Unsupported File Format -***The submitted file type is not currently supported by the engine.*

#### [Threat Naming Convention](/docs/mdcore/predictive-alin-ai/engine-response-structure#threat-naming-convention)

When a file is classified as malicious, **Predictive Alin AI** returns a standardized detection name in the following format: **<platform>/malicious*<*threat_confidence>**

**platform:**

- indicates the execution ecosystem associated with the file type. Windows is used for PE-based executables, Linux for ELF-based binaries, and Darwin for Mach-O-based binaries. Generic is used for non-platform-specific formats such as PDF.

**threat********_**confidence :**

- represents the model’s threat confidence level for the analyzed file. Higher values indicate higher malicious confidence. For example, **malicious_99** indicates very high confidence that the file is malicious.

**Examples:**

- PE file: `Windows/malicious_99`
- ELF file: `Linux/malicious_99`
- Mach-O file: `Darwin/malicious_99`
- PDF file: `Generic/malicious_99`
