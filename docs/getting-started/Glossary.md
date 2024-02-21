---
sidebar_position: 5
---

# Glossary

## Daemon

Daemon's are the workhorses in Mycelial. The Mycelial daemon is a small binary,
written in Rust, that is responsible for pulling data from sources and/or
pushing data to destinations. You typically install the daemon near the
source/destination, using our CLI. 

## Connector

A connector is a specific implementation of a data source or destination. For
example, the Postgres connector is a specific implementation of a Postgres data
source or destination.

## Control Plane

The Mycelial control plane is a server that defines and orchestrates data
workflow jobs. You can either install the control plane on one of your servers,
using our CLI or you can use our cloud-based control plane (coming soon). 

## Workflow

A workflow is a combination of the source and destination data systems. A
workflow is essentially a job that moves data from the source to the destination
data system. The workflow is created either in the control planes Web interface
or via API calls.

## Command Line Interface (CLI) Application

Mycelial maintains a [CLI](./CLI.md) that assists you in setting up and using
Mycelial.  After downloading and installing the CLI, you can run the application
to do things like: Download the daemon and control plane, Configure data sources
and destinations, Start and stop the daemon and control plane, install the
daemon as a service and more.

## Source

A source is a specific database, or file from which you wish to sync your data.
Some examples of sources are: Postgres, MySQL, SQLite and MS Excel.

## Destination

A destination is a specific data sink that receives data without transmitting
it. Some examples of destinations are: Postgres, Snowflake and Redshift.
