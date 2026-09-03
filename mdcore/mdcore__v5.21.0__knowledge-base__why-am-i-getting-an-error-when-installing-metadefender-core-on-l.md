<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-am-i-getting-an-error-when-installing-metadefender-core-on-l -->

# Why am I getting an error when installing MetaDefender Core on Linux in an air-gap environment?

This article applies to all MetaDefender Core releases deployed on Linux.

#### [Issue:](/docs/mdcore/v5.21.0/knowledge-base/why-am-i-getting-an-error-when-installing-metadefender-core-on-l#issue)

- When installing the MetaDefender Core package on a Linux machine via the `dnf`, `yum`, or `apt` command in an air-gap environment, you may encounter an error.

#### [Main cause:](/docs/mdcore/v5.21.0/knowledge-base/why-am-i-getting-an-error-when-installing-metadefender-core-on-l#main-cause)

- When performing an installation via a package manager (`dnf`, `yum`, `apt`), the system attempts to reach out to a package repository to obtain information about the package being installed. In an air-gap environment, if a local repository is not configured, the download or upgrade process via the package manager will fail.

#### [Resolution:](/docs/mdcore/v5.21.0/knowledge-base/why-am-i-getting-an-error-when-installing-metadefender-core-on-l#resolution)

- Install the package using a local installation method, such as the native `rpm` or `dpkg` command.

Support:

If the problem still persist, please proceed to [**create a support case or chat with our support engineer.**](https://my.opswat.com/portal/support-services) for futher assistant.
