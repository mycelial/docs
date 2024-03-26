---
sidebar_position: 5
id: mysql
title: Mysql
---

# Mysql

The Mysql destination allows you to write data to a Mysql database.

To use the Mysql destination, you will need to install the Mycelial Daemon on
the computer that has access to the Mysql database. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Mysql as a data destination,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[destinations]]
type = "mysql_connector"
display_name = "mysql destination"
url = "mysql://username:password@127.0.0.1:3306/test"
```

### type

The `type` field specifies the type of data destination, in this case it is
`mysql_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### url

The `url` field is the connection string to the Mysql database.  The format
of the Mysql connection string is:

`mysql://username:password@localhost:3306/test`

Where:

1. **Protocol**: `mysql://`
  - Indicates the database type (Mysql) and connection protocol.

2. **User**: `username`
  - The username for database authentication.

3. **Password**: `password`
  - The password for the specified username.

4. **Host**: `localhost`
  - The host where the database server is running. `localhost` means the server is on the same machine as the daemon.

5. **Port**: `3306`
  - The port where the database server is listening for connections. The default port for Mysql is `3306`.

6. **Database**: `test`
  -- The name of the database to connect to, here it is `test`.

This string instructs the Mysql connector to connect to the database `test` on
the local machine (`localhost`) using port `3306`, with the username `username`
and password `password`.

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
down arrow to highlight `MySql destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  SQLite destination
  Postgres destination 
❯ MySQL destination ⏎
  Kafka destination
  Snowflake destination
  File destination
  Cancel
```

When prompted for the `Display Name` press return (⏎) to accept the default or 
enter a name for your destination and press return (⏎).

```sh
? Display name: (Mysql Destination) › ⏎
```

When prompted for the `MySQL username`, enter the username for the MySQL 
user and press return (⏎).

```sh
? MySQL username: (user) › mysql_user ⏎
```

When prompted for the `MySQL password`, enter the password for the MySQL
user and press return (⏎).

```sh
? MySQL password: › mysql_password ⏎
```

When prompted for the `Server address`, enter the host name or IP address for
the MySQL database.

```sh
? Server address: (localhost) › mymysqlhost.com ⏎
```

When prompted for the `MySQL port`, enter the port for the MySQL database.

```sh
? MySQL port: (3306) › 3306 ⏎
```

When prompted for the `Database name`, enter the name of the MySQL database.

```sh
? Database name: (database) › my_db ⏎
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

After you have added the MySQL destination to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the MySQL source listed in the
destination section.
