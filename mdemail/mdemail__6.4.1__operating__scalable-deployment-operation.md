<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/scalable-deployment-operation -->

# Scalable deployment operation

## [Overview](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#overview)

## [The problem](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#the-problem)

Each Email Gateway Security standalone instances have their own *database*. The database stores the information about configuration, email processing results and quarantine among others.

As a consequence, in standalone deployments, the exact instance that processed a particular email must be known, so that a certain email can be released from the quarantine, for example.

The separate email history databases are not synchronized.

## [Solution](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#solution)

In a scalable deployment Email Gateway Security instances work on a shared database. The database runs either on one the instances

or as a separate database server

and the (other) instances connect to the shared database.

With this solution all instances see the same data. It is irrelevant, on which instance an email history or quarantine operation is performed, all instances will see the same.

Email Gateway Security instances must be installed appropriately so that a scalable deployment can be set up. For details about the scalable mode installation see [Installation/Scalable deployment](/docs/mdemail/6.4.1/installation/standalone-deployment).

### [Limitations](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#limitations)

Eliminate single point of failure

The shared database can be a single point of failure in a scalable deployment. The solution is to set up a PostgreSQL database cluster that provides high availability for the database. For details see <https://www.postgresql.org/docs/current/high-availability.html>.

## [Dashboard](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#dashboard)

In a scalable deployment the **Dashboard** shows information about emails on all connected instances.

For **Dashboard** details see [Operating/Dashboard](/docs/mdemail/6.4.1/operating/dashboard).

## [Email History](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#email-history)

In a scalable deployment the **Audit > Email History** shows emails from all connected instances by default.

For **Audit > Email History** details see [Operating/Email History](/docs/mdemail/6.4.1/operating/email-history).

## [Processing information](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#processing-information)

The *Processing information* view shows the name of the actual instance where the particular email was processed.

Instance naming

For information about how to name instances see [Configuration/Scalable deployment related registry configuration](/docs/mdemail/6.4.1/configuration/scalable-deployment-related-registry-configuration).

## [Filtering](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#filtering)

In a scalable deployment the **Audit > Email History** can be filtered for a particular instance, or multiple instances.

Example

To filter for emails processed by the actual instance only, select the name of this instance from the list of instances in the filter.

## [Quarantine](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#quarantine)

**Quarantine** is a subset of email history. In a scalable deployment –similarly to **Audit > Email History**– quarantined items from all instances can be viewed and operated.

For **Quarantine** details see [Operating/Quarantine](/docs/mdemail/6.4.1/operating/quarantine).

Example

In a scalable deployment an email can be released from the quarantine even if it was quarantined by an other instance.

## [Operations](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#operations)

Quarantine operations in a scalable deployment can be executed on emails irrelevant from on which instance the email was processed.

## [Filtering](/docs/mdemail/6.4.1/operating/scalable-deployment-operation#filtering)

In a scalable deployment the **Quarantine** can be filtered for a particular instance, or multiple instances similarly to **Audit > Email History**.

##
