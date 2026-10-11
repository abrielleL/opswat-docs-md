<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/is-metadefender-core-fully-selinux-compliant- -->

# Is MetaDefender Core Fully SELinux Compliant?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on RHEL 9.

> **Issue:**

MetaDefender Core is not currently SELinux compliant, although it functions on systems where SELinux is enabled. It does not adhere to full SELinux confinement policies or provide officially supported SELinux policy modules.

**Resolution:**

At this time, OPSWAT does not provide or recommend SELinux confinement policies for MetaDefender Core. For full functionality, Core services should remain unconfined.

**Workarounds:**

Most Linux customers operate MetaDefender Core on RHEL systems with SELinux enabled without any issues, even when services run unconfined.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
