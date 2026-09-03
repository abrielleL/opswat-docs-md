<!-- source: https://www.opswat.com/docs/mdss/getting-started/overview -->

# Overview

MetaDefender Storage Security offers a robust solution for protecting enterprise data stored in various on-premises, cloud, and hybrid environments. It is designed to prevent data breaches, downtime, and compliance violations by scanning files for malware, vulnerabilities, and sensitive data.

A crucial aspect of MetaDefender Storage Security's operation is its **exclusive bundling and integration with MetaDefender Core and its associated engine packages.**

MetaDefender Storage Security itself does not perform the deep file analysis. Instead, it acts as a component that connects to various storage solutions (Amazon S3, Azure Blob, network-attached storage, etc.) and orchestrates the scanning process by sending files to a MetaDefender Core instance.

MetaDefender Core is the underlying analysis engine that utilizes multiple proprietary OPSWAT technologies, including:

- Multiscanning leverages multiple anti-malware engines to detect a broad range of known threats.
- Deep CDR (Content Disarm and Reconstruction) sanitizes files by removing potentially malicious content and reconstructing safe, usable versions, effectively preventing zero-day attacks.
- Proactive DLP (Data Loss Prevention) identifies and redacts or blocks sensitive information within files to help meet compliance requirements. **NOTE:** MetaDefender Storage Security does not process the redacted file; it only displays the detected sensitive data in a file.
- File-Based Vulnerability Assessment detects known vulnerabilities within software components.

MetaDefender Storage Security functions as the layer that integrates with your storage systems and manages the file processing workflow, while MetaDefender Core, with its various licensed engine packages, performs the actual threat detection, sanitization, and data protection tasks.

This architecture ensures that files are thoroughly inspected before they are stored or accessed, providing a comprehensive security layer for enterprise data. Deployment options may involve a self-hosted MetaDefender Core, a cloud-based MetaDefender Cloud instance (which includes Core functionalities as a service), or MetaDefender Core deployed via AMIs or containers.
