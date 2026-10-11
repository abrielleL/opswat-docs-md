<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-install-multiple-managed-file-transfers-servers-on-the-sa -->

# How to install multiple Managed File Transfer servers on the same Remote SQL server?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

MetaDefender Managed File Transfer supports the configuration of multiple servers using the same Remote SQL server.

1. Install an additional SQL instance on the SQL Server or SQL Cluster
2. Ensure that the new instance supports TCP/IP and has a unique port (Failing to set a unique port will prevent the process from starting)
3. In MetaDefender Managed File Transfer, when prompted to enter the path to the SQL server, use the following format: Server name: <IP address>,<Port for the instance><Instance name>
