<!-- source: https://www.opswat.com/docs/mdicap/configuration/basic-workflow -->

# Basic workflows

After installation, successful license activation and basic configuration MetaDefender ICAP Server is ready to be used.

However, MetaDefender ICAP Server blocks all requests by default. To allow web traffic some basic security rule configuration is needed.

Warning

The basic workflows created in this chapter may be too permissive and may not be suitable for production deployments.

## [Prerequisites](/docs/mdicap/configuration/basic-workflow#prerequisites)

The following information is needed to create the basic security rules:

1. MetaDefender Core type server profile containing the Core (see [1.3 Creating MetaDefender Core server profile](/docs/mdicap/configuration/creating-metadefender-core-server-profile))

## [Configuration](/docs/mdicap/configuration/basic-workflow#configuration)

To allow web traffic go to **Policy > Security** rules and create the following basic workflows.

Info

In the examples below we assume that the Core server is configured in the MetaDefender Core server profile CoreProfile.

Note

Properties not listed in the table below may be left on their default values (if they have, e.g. settings on ACTIONS or ADVANCED tabs) or filled according to the organizational policies (e.g. USE TLS).

| Tab | SCAN |
| --- | --- |
| Field | MetaDefender CORE |
| Value | MetaDefender Core type server profile containing the Core |
| Examples | CoreProfile |

For details about security rules in MetaDefender ICAP Server see [4.2 Security Rules Policy](/docs/mdicap/operating/security-rules-policy).
