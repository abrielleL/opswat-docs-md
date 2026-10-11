<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-must-each-metadefender-core-installation-have-a-unique-insta -->

# Why Must Each MetaDefender Core Installation Have a Unique Instance Name?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

#### [Overview](/docs/mdcore/v5.22.1/knowledge-base/why-must-each-metadefender-core-installation-have-a-unique-insta#overview)

The instance name is a key configuration parameter in MetaDefender Core that identifies each installation uniquely — especially in environments where multiple Core instances share the same database.

This article explains what the instance name is, how it is used, and why it must be unique for each Core installation.

#### [What Is the Instance Name and When Is It Used?](/docs/mdcore/v5.22.1/knowledge-base/why-must-each-metadefender-core-installation-have-a-unique-insta#what-is-the-instance-name-and-when-is-it-used)

The instance name is a unique identifier assigned to each MetaDefender Core installation. It is primarily used in shared database environments where multiple MetaDefender Core servers operate together, typically for scalability or redundancy.

When multiple Core installations share a single database:

- The instance name distinguishes between individual Core servers.
- It allows each instance to maintain its own local configuration settings, such as:

  - Application configuration (e.g., queue size, parallel count, etc)
  - Module configuration (e.g., enabled engines, module parameters)
- Meanwhile, global components such as workflows and user accounts are shared across all instances in the shared database.

#### [Why the Instance Name Must Be Unique](/docs/mdcore/v5.22.1/knowledge-base/why-must-each-metadefender-core-installation-have-a-unique-insta#why-the-instance-name-must-be-unique)

Each MetaDefender Core instance must have a unique instance name when sharing the same database. If two or more Core installations use the same instance name:

- Configuration data between those instances will overlap.
- Changes made in one installation may overwrite or conflict with those in another.
- This can result in abnormal or unstable functionality, including:

  - Module misconfiguration
  - Database connection issues

In short, duplicate instance names in a shared database environment are not supported and will cause operational conflicts.

Support:

If further assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
