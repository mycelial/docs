---
sidebar_position: 2
id: sqlite
title: SQLite
---

# SQLite

The SQLite destination allows you to write data from various data sources.

To use the SQLite destination, you will need to install the Mycelial Daemon on
the computer that has the SQLite database. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add SQLite as a data destination,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[destinations]]
type = "sqlite_connector"
display_name = "Sqlite Destination"
path = "destination.db"
```

**NOTE**: You can manually add the above table to the `config.toml` file or you
can use the `mycelial add --destination` command to add the destination to an
existing config file.

### type

The `type` field specifies the type of data destination, in this case it is
`sqlite_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### path

The `path` field is the path to the SQLite database file.


## Usage

After you have added the SQLite destination to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the SQLite destination listed in
the destinations section.