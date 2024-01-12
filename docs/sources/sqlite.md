---
sidebar_position: 2
id: sqlite
title: SQLite
---

# SQLite Append Only

The SQLite append only source allows you to read data from a SQLite database. 
Currently, Mycelial only supports SQLite databases that are append only.

To use the SQLite append only source, you will need to install the Mycelial 
Daemon on the computer that has the SQLite database. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add SQLite as a data source,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
...
[[sources]]
type = "sqlite_connector"
display_name = "Sqlite Source"
path = "/path/to/sqlite/source.db"
```

**NOTE**: You can manually add the above table to the `config.toml` file or you
can use the `mycelial add --source` command to add the source to an existing 
config file.

### type

The `type` field specifies the type of data source, in this case it is
`sqlite_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### path

The `path` field is the path to the SQLite database file.

## Usage

After you have added the SQLite source to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the SQLite source listed in the
sources section.

