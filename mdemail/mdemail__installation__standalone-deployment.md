<!-- source: https://www.opswat.com/docs/mdemail/installation/standalone-deployment -->

# Standalone deployment

## [Overview](/docs/mdemail/installation/standalone-deployment#overview)

In a standalone deployment each Email Gateway Security instance work on its own database.

Embedded database performance

The embedded PostgreSQL database is primarily designed for testing and low-volume deployments, and is not recommended for heavy load environments.

For reliable and secure operation, a robust external PostgreSQL database cluster solution is recommended.

## [Installation](/docs/mdemail/installation/standalone-deployment#installation)

In the *Choose Database Setup Type* dialog select the *Standalone* option and complete the setup of the instance.

Port may already be taken

The default database port 5433 in case of a standalone deployment may already be taken by a running PostgreSQL instance (e.g. an other OPSWAT product's standalone database).

This situation can lead to a broken installation. To avoid that, the target database port availability must be checked prior to the installation.
