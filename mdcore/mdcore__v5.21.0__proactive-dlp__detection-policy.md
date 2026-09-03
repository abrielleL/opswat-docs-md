<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/proactive-dlp/detection-policy -->

# Detection Policy

The detection policy allows the users to define complicated rules to decide when files are blocked or allowed. For example, you can define a rule to block files which have more than 10 IP addresses, or even more complicated such as files that have AWS Key ID **and** AWS Secret Key

**1. For predefine sensitive info**: {predefine sensitive info.attribute} > X

Supported pre-defined sensitive info: *ccn, ssn, ipv4, cidr,...* For the full list of supported entities, please visit this [page](https://www.opswat.com/docs/mdcore/proactive-dlp/detection-policy---supported-entities).

Example: {ipv4.count} > 10 will block the files only if the Proactive DLP module detects 10 IP address or more

**2. For Regular expression**: {regex.name.atrribute} > X . The example below shows you how to block a file if it has both AWS Key ID and AWS Secret Key

Create regular expressions to block AWS Access keys and AWS secret key

AWSAccessKey: (?<![A-Z0-9])[A-Z0-9]{20}(?![A-Z0-9])

AWSSecretKey: ([a-zA-Z0-9+/]{40})

Detection Policy: {regex.AWSAccessKey.count} > 0 and {regex.AWSSecretKey.count} > 0

**3. For Metadata:** {metadata.name.count} > X

**Supported attribute:**

- count: Only hits with equal or higher certainty than the CERTAINTY THRESHOLD will be counted

**Supported arithmetic operators:** <, >, =, <=, >=, <>

- Example 1: {ccn.count} >= 5
- Example 2: {ccn.count} <> {ssn.count}

**Supported logical operators:** and, nand, or, nor, xor

- Logical operators must be lower case
- Precedence of the operators are implemented in the following order: **nand**, **and**, **nor**, **or**, **xor**
- Example: {ccn.count} >= 5 or 1 < {metadata.Meta.count}

**Supported** **parentheses :** ()

- Always prioritizes the content to be evaluated first (**Highest precedence**)
- Example: ({ccn.count} >= 5 or {ssn.count} > 2) and {ipv4.count} > 3

**Note**:

- The Predefine Sensitive Types and regex name are case sensitive
- Regex name and metadata name can't have space, dot or curly brackets
- Predefine Sensitive Types should be enabled if they are used in the policy, otherwise the validation during file processing will be failed.
