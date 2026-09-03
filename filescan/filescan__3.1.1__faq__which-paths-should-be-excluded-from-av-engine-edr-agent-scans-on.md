<!-- source: https://www.opswat.com/docs/filescan/3.1.1/faq/which-paths-should-be-excluded-from-av-engine-edr-agent-scans-on -->

# Which paths should be excluded from AV engine/EDR agent scans on the sandbox server?

It is not recommended to install an AV engine or EDR agent on the sandbox server, unless it is a strict policy requirement within an organization.

If an EDR agent or AV engine is installed without proper configuration, then the MetaDefender Aether system simply cannot receive and analyze files that are flagged by the EDR agent or AV engine.

The following folders **must be excluded** in the EDR agent or AV engine:

- The MetaDefender Aether installation folder ( `/home/sandbox/sandbox` by default)
- `/var/lib/docker`
- `/data/db`
- `/data/graphdb`

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
