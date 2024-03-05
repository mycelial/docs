---
sidebar_position: 3
id: postgres
title: Postgres
---

# Postgres

The Postgres destination allows you to write data to a Postgres database. 

To use the Postgres destination, you will need to install the Mycelial Daemon on
the computer that has access to the Postgres database. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Postgres as a data destination,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[destinations]]
type = "postgres_connector"
display_name = "postgres destination"
url = "postgres://user:password@127.0.0.1:5432/test"
```

### type

The `type` field specifies the type of data destination, in this case it is
`postgres_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### url

The `url` field is the connection string to the Postgres database.  The format
of the PostgreSQL connection string is:

`postgres://user:password@localhost:5432/test`

Where:

1. **Protocol**: `postgres://`
   - Indicates the database type (PostgreSQL) and connection protocol.

2. **User**: `user`
   - The username for database authentication.

3. **Password**: `password`
   - The password for the specified username.

4. **Host**: `localhost`
   - The host where the database server is running. `localhost` means the server is on the same machine as the daemon.

5. **Port**: `5432`
   - The port number where the PostgreSQL server is listening. The default is `5432`.

6. **Database Name**: `test`
   - The name of the database to connect to, here it is `test`.

This string instructs the daemon to connect to the `test` database on the local machine (`localhost`) using port `5432`, with the username `user` and password `password`.

## Configuration via CLI

You will need to have the Mycelial CLI installed. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Create a new `config.toml` file or add to an existing one

If you are creating a new `config.toml` file, you can use the Mycelial CLI [`init`](../getting-started/CLI#initialization) command to generate the file and add the source. 

If you are adding to an existing config file you can use the Mycelial CLI [`add`](../getting-started/CLI#adding-new-sourcesdestinations) command to add the source to the existing config. 

### Choose source config options

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Destination` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source 
❯ Add Destination ⏎
  Exit
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Postgres destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  SQLite destination
❯ Postgres destination ⏎
  MySQL destination
  Kafka destination
  Snowflake destination
  File destination
  Cancel
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎).

```sh
? Display name: (Postgres Destination) › ⏎
```

When prompted for the `Postgres username`, enter the username for the Posgres 
user and press return (⏎).

```sh
? Postgres username: (user) › postgres ⏎
```

When prompted for the `Postgres password`, enter the password for the Posgres
user and press return (⏎).

```sh
? Postgres password: › password ⏎
```

When prompted for the `Server address`, enter the host name or IP address for
the Posgres database.

```sh
? Server address: (localhost) › mypostgreshost.com ⏎
```

When prompted for the `Postgres port`, press return (⏎) to accept the default 
port or enter the port number for the Posgres database and press return (⏎).

```sh
? Postgres port: (5432) › ⏎
```

When prompted for the `Database name`, enter the name of the Posgres database
and press return (⏎).

```sh
? Database name: (test) › my_db ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit
```

After exiting the CLI will generate or save the modified `config.toml`.

## Usage

After you have added the Postgres destination to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the Postgres destination listed in the
destination section.
