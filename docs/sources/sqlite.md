---
sidebar_position: 2
id: sqlite
title: SQLite
---

# SQLite Append Only

The SQLite source allows you to read data from a SQLite database. 
Currently, Mycelial only supports SQLite databases that are append only.

To use the SQLite source, you will need to install the Mycelial 
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

### type

The `type` field specifies the type of data source, in this case it is
`sqlite_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### path

The `path` field is the path to the SQLite database file.

## Configuration via CLI

### Prerequisites

You will need to have the Mycelial CLI installed. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Create a new `config.toml` file or add to an existing one

If you are creating a new `config.toml` file, you can use the Mycelial CLI [`init`](../getting-started/CLI#initialization) command to generate the file and add the source. 

If you are adding to an existing config file you can use the Mycelial CLI [`add`](../getting-started/CLI#adding-new-sourcesdestinations) command to add the source to the existing config. 

### Choose source config options

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Source` and press return (⏎).

```sh
? What would you like to do? ›
❯ Add Source ⏎
  Add Destination
  Exit
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `SQLite source` and press return (⏎).

```sh
? What type of source would you like to add? ›
❯ SQLite source ⏎
  Excel source
  Postgres source
  MySQL source
  File source
  Cancel
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (SQLite Source) › ⏎
```

When prompted for the `Database Path`, enter the source database name.

```sh
? Database Path: (data.db) › /path/to/the/source.db ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit ⏎
```

After exiting the CLI will generate or save the modified `config.toml`.

## Usage

After you have added the SQLite source to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the SQLite source listed in the sources
section.

