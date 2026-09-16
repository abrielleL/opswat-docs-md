<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/does-opswat-use-security-checks-on-our-code--libraries--credenti -->

# Does OPSWAT Use Security Checks on Our Code, Libraries, Credentials, etc?

Yes, we implement comprehensive security checks throughout our development lifecycle to ensure the safety and integrity of our products.

Please refer to the following security checks that we conduct:

1. **Static Application Security Testing (SAST)**

   - **SonarQube**: Integrated into the development process to analyze code quality and security. All issues are resolved before release.
2. **Dynamic Application Security Testing (DAST)**

   - **Tenable**: Conducts weekly scans on live applications to identify vulnerabilities. All findings are addressed prior to release.
3. **Software Composition Analysis (SCA)**

   - **Blackduck**: Scans dependencies daily to detect known vulnerabilities. Any issues are resolved before deployment.
4. **Secret Scanning**

   - **Gitleaks**: Monitors each code commit for exposed credentials or sensitive information.

We also leverage open-source tools to enhance our security posture:

- **Trivy**: Scans containers for vulnerabilities and misconfigurations.
- **OWASP ZAP**: Conducts dynamic security testing for web applications.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
