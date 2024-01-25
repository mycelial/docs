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

The `type` field specifies the type of data source, in this case it is
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
   - The host where the database server is running. `localhost` means the server is on the same machine as the client.

5. **Port**: `5432`
   - The port number where the PostgreSQL server is listening. The default is `5432`.

6. **Database Name**: `/test`
   - The name of the database to connect to, here it is `test`.

This string instructs the client to connect to the `test` database on the local machine (`localhost`) using port `5432`, with the username `user` and password `password`.

## Configuration via CLI

You will need to have the Mycelial CLI installed. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Creating a new `config.toml` file

If you are creating a new `config.toml` file, you can use the Mycelial CLI to
generate the file and add the Excel source. To do this, run the following 
command:

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
down arrow to highlight `Append only Postgres destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
  Append only SQLite destination
❯ Append only Postgres destination ⏎
  Append only MySQL destination
  Kafka destination
  Snowflake destination
  File destination
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎).

```sh
? Display name: (Postgres Append Only Destination) › ⏎
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

After exiting the CLI will generate a `config.toml`.

### Appending to an existing `config.toml` file

If you already have a `config.toml` file, you can use the Mycelial CLI to add
the Excel source. To do this, run the following command from the same directory
as the `config.toml` file:

```sh
mycelial add --destination
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Append only Postgres destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
  Append only SQLite destination
❯ Append only Postgres destination ⏎
  Append only MySQL destination
  Kafka destination
  Snowflake destination
  File destination
  Exit
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎).

```sh
? Display name: (Postgres Append Only Destination) › ⏎
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
❯ Exit ⏎
```

After exiting the CLI will save the modified `config.toml`.

## Usage

After you have added the Postgres destination to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the SQLite source listed in the sources
section.
