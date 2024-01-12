---
sidebar_position: 1
id: snowflake
title: Snowflake
---

# Snowflake

The Snowflake destination allows you to write data to a Snowflake data-warehouse.

To use the Snowflake destination, you will need to install the Mycelial Daemon on
the computer that has access to the Snowflake data-warehouse. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Snowflake as a data destination,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[destinations]]
type = "snowflake"
display_name = "snowflake destination"
username = "username"
password = "password"
role = "role"
account_identifier = "myorg-account123"
warehouse = "warehouse"
database = "database"
schema = "schema"
```

### type

The `type` field specifies the type of data source, in this case it is
`snowflake`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### username

The `username` field is the username for Snowflake authentication.

### password

The `password` field is the password for the specified username.

### role

The `role` field is the Snowflake role you wish to assume.

### account_identifier

The `account_identifier` field is the Snowflake account identifier. The account
identifier includes the name of the account along with its organization (e.g.
myorg-account123).

### warehouse

The `warehouse` field is the Snowflake data warehouse you wish to use.

### database

The `database` field is the Snowflake database you wish to use.

### schema

The `schema` field is the Snowflake schema in the given database you wish to use.

## Usage

After you have added the Snowflake destination to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the Snowflake destination listed in
the destinations section.