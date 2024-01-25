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
path = "/path/to/sqlite/destination.db"
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

## Configuration via CLI

### Prerequisites

You will need to have the Mycelial CLI installed. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Creating a new `config.toml` file

If you are creating a new `config.toml` file, you can use the Mycelial CLI to
generate the file and add the SQLite destination to it. To do this, run the
following command:

```sh
mycelial init --local
```

Running the above command will download both the [Control
plane](../core-concepts/Control-Plane.md) and the
[Daemon](../core-concepts/Daemon.md) and it will ask you a series of questions
to generate the `config.toml` file.

When prompted for the `Client Name:` press return (⏎) to accept the default
value or enter a name for your client and press return (⏎).

```sh
? Daemon Name: (My Daemon)› ⏎
```

When prompted for the `Client ID:` press return (⏎) to accept the default value
or enter a client ID and press return (⏎).

```sh
? Daemon ID: (daemon)› ⏎
```

When prompted for the `Server:` press return (⏎) to accept the default value or
enter the URL of the control plane and press return (⏎). If you are just trying
out Mycelial, you should press return (⏎) to accept the default value.

```sh
? Server: (http://localhost:7777) › ⏎
```

When prompted for the `Security Token:` enter a token and press return (⏎). If 
you are just trying out Mycelial, enter `token` and press return (⏎).

```sh
? Security Token: › token ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Destination` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source 
❯ Add Destination ⏎
  Exit
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Append only SQLite destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
❯ Append only SQLite destination ⏎
  Append only Postgres destination
  Append only MySQL destination
  Kafka destination
  Snowflake destination
  File destination
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎). The display name is the
name that will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (SQLite Append Only Destination) › ⏎
```

When prompted for the `Database Path`, enter the destination database name.

```sh
? Database Path: (destination.db) › /path/to/sqlite/destination.db ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit ⏎
```

After exiting the CLI will generate a `config.toml`.

### Appending to an existing `config.toml` file

If you already have a `config.toml` file, you can use the Mycelial CLI to add
the SQLite destination. To do this, run the following command from the same
directory as the `config.toml` file:

```sh
mycelial add --destination
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Append only SQLite destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
❯ Append only SQLite destination ⏎
  Append only Postgres destination
  Append only MySQL destination
  Kafka destination
  Snowflake destination
  File destination
  Exit
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎). The display name is the
name that will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (SQLite Append Only Destination) › ⏎
```

When prompted for the `Database Path`, enter the destination database name.

```sh
? Database Path: (destination.db) › /path/to/sqlite/destination.db ⏎
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Exit` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
  Append only SQLite destination
  Append only Postgres destination
  Append only MySQL destination
  Kafka destination
  Snowflake destination
  File destination
❯ Exit
```

## Usage

After you have added the SQLite destination to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the SQLite source listed in the sources
section.