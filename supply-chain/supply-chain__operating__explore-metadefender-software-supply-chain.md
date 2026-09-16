<!-- source: https://www.opswat.com/docs/supply-chain/operating/explore-metadefender-software-supply-chain -->

# Explore MetaDefender Software Supply Chain

MetaDefender Software Supply Chain brings repository, container, binary, and file scanning into one place. Connect the services you already use, automate security checks, investigate risks, and take action from a unified view.

[Connect your software ecosystem](/integrations/add-service-units): Scan source code, container registries, and binary repositories through supported service integrations.
[See your security posture](/operating/dashboard): Track risk scores, threats, exposed secrets, critical vulnerabilities, risky packages, and remediation opportunities.
[Scan on your terms](/operating/triggering-a-scan): Run scans on demand, on a recurring schedule, or automatically when a repository changes.
[Investigate every finding](/operating/reports): Review repository, package, vulnerability, malware, secret, and license-risk details in scan reports.

## Detect risks across the software supply chain

Apply multiple security technologies to the files and artifacts in your software supply chain:

- **Malware and other threats:** use MetaScan multiscanning to inspect files with multiple anti-malware engines.
- **Exposed secrets:** detect credentials, tokens, and other sensitive data committed to source code or included in artifacts.
- **Open source vulnerabilities:** generate a Software Bill of Materials (SBOM) and identify known vulnerabilities in dependencies.
- **License risks:** surface open source license information to support policy and compliance reviews.

[Workflows](https://www.opswat.com/docs/supply-chain/configuration/workflow-creation) show which technologies are active for a scan and let you define how results are handled.

## Scan from development to delivery

[Source code](/integrations/add-service-units): Connect GitHub, GitLab, Bitbucket, Gitea, SVN, or Azure DevOps and scan repositories and references.
[Containers](/integrations/add-service-units): Inspect images stored in Amazon ECR, Azure Container Registry, Docker Hub, JFrog, Quay, or Harbor.
[Binary repositories](/integrations/add-service-units): Scan packages and artifacts in JFrog Artifactory and Sonatype Nexus Repository.
[Individual files](/operating/analyze): Upload manifests, installers, archives, and other files for direct analysis without connecting a repository.

You can also use the [CLI Scanner](https://www.opswat.com/docs/supply-chain/operating/cli-scanner) to bring file and directory scanning into command-line workflows and CI/CD pipelines.

## Automate security checks

Choose the scan method that matches each development workflow:

- Start an [on-demand scan](https://www.opswat.com/docs/supply-chain/operating/triggering-a-scan) for one or more repositories and references.
- Create [scheduled scans](https://www.opswat.com/docs/supply-chain/operating/scheduling-automatic-scanning) that run hourly, daily, weekly, or monthly.
- Configure [event-based scanning](https://www.opswat.com/docs/supply-chain/operating/triggering-an-automatic-scan) to respond to repository changes.
- Enable [hash scanning](https://www.opswat.com/docs/supply-chain/operating/scheduling-automatic-scanningqnr) to skip unchanged files and focus repeat scans on new or modified content.
- Use [Jobs](https://www.opswat.com/docs/supply-chain/operating/jobs) to create scans and monitor active, upcoming, and completed work.

## Turn findings into action

The [Dashboard](https://www.opswat.com/docs/supply-chain/operating/dashboard) summarizes risk across all scanned repositories and highlights the packages and repositories that need attention. Security suggestions identify package updates that can resolve vulnerabilities.

Detailed [Reports](https://www.opswat.com/docs/supply-chain/operating/reports) let you move from the overall picture to individual repositories, packages, files, and CVEs. Export results when you need to share findings or continue analysis outside the product.

Custom [workflows](https://www.opswat.com/docs/supply-chain/configuration/workflow-creation) add policy and remediation controls. Depending on the service and artifact type, a workflow can keep, copy, soft-delete, or delete content, promote approved artifacts to a secure zone, and send notifications through email, Jira, or Microsoft Teams.

## Stay informed and accountable

- The [Notification Center](https://www.opswat.com/docs/supply-chain/operating/notification-center) provides real-time status updates and quick links to completed scan results.
- The [Audit log](https://www.opswat.com/docs/supply-chain/operating/audit) records scan, configuration, user, and sign-in activity for operational visibility.
- [User management](https://www.opswat.com/docs/supply-chain/configuration/user-management) helps administrators control who can access the deployment.
- [Syslog](https://www.opswat.com/docs/supply-chain/configuration/syslog) supports centralized monitoring and logging.

## Get started

1. [Add a service connection](https://www.opswat.com/docs/supply-chain/integrations/add-service-units) for a source code, container, or binary platform.
2. Review the built-in Default Workflow or [create a custom workflow](https://www.opswat.com/docs/supply-chain/configuration/workflow-creation) for tailored scan behavior and remediation.
3. [Trigger a scan](https://www.opswat.com/docs/supply-chain/operating/triggering-a-scan), then explore the results in [Reports](https://www.opswat.com/docs/supply-chain/operating/reports) and track your overall posture on the [Dashboard](https://www.opswat.com/docs/supply-chain/operating/dashboard).
