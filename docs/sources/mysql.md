---
sidebar_position: 5
id: mysql
title: MySQL
---

# MySQL Append Only

The MySQL source allows you to read data from a MySQL database. Currently,
Mycelial only supports MySQL databases that are append only.

To use the MySQL source, you will need to install the Mycelial Daemon on the
computer that has access to the MySQL database. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add MySQL as a data source,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[sources]]
type = "mysql_connector"
display_name = "Mysql Source"
url = "mysql://user:password@localhost:3306/test"
schema = "public"
tables = "*"
poll_interval = 5
```

### type

The `type` field specifies the type of data source, in this case it is
`mysql_connector`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### url

The `url` field is the connection string to the MySQL database.  The format
of the MySQL connection string is:

`mysql://user:password@localhost:3306/test`

Where:

1. **Protocol**: `mysql://`
   - Indicates the database type (MySQL) and connection protocol.

2. **User**: `user`
   - The username for database authentication.

3. **Password**: `password`
  - The password for the specified username.

4. **Host**: `localhost`
   - The host where the database server is running. `localhost` means the server is on the same machine as the daemon.

5. **Port**: `3306`
  - The port number where the MySQL server is listening. The default is `3306`.

6. **Database**: `test`
  - The name of the database to connect to, here it is `test`.

This string instructs the daemon to connect to the `test` database on the local
machine (`localhost`) using port `3306`, with the username `user` and password
`password`.

### schema

The `schema` field is the name of the schema that contains the tables that you
want to read from.

### tables

The `tables` field is a comma separated list of tables that you want to read
from. If you wish to read from all tables, then you can use the `*` wildcard.

### poll_interval

The `poll_interval` field is the number of seconds between polling the database
for new data. 

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
arrow to highlight `Append only MySQL source` and press return (⏎).

```sh
? What type of source would you like to add? ›
  Append only SQLite source
  Excel source
  Append only Postgres source 
❯ Append only MySQL source ⏎
  File source
  Cancel
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (Mysql Source) › ⏎
```

When prompted for the `Mysql username`, enter the username for the Mysql 
user and press return (⏎).

```sh
? Mysql username: (user) › root ⏎
```

When prompted for the `Mysql password`, enter the password for the Posgres
user and press return (⏎).

```sh
? Mysql password: › password ⏎
```

When prompted for the `Server address`, enter the host name or IP address for
the Posgres database.

```sh
? Server address: (localhost) › mymysqlhost.com ⏎
```

When prompted for the `Mysql port`, press return (⏎) to accept the default 
port or enter the port number for the Posgres database and press return (⏎).

```sh
? Mysql port: (3306) › ⏎
```

When prompted for the `Database name`, enter the name of the Posgres database
and press return (⏎).

```sh
? Database name: (test) › my_db ⏎
```

When prompted for the `Schema`, press return (⏎) to accept the default schema
or enter the name of the schema and press return (⏎).

```sh
? Schema: (public) › my_schema ⏎
```

When prompted for the `Tables`, press return (⏎) to accept the default (*) for 
all tables or enter a comma separated list of tables and press return (⏎).

```sh
? Tables: (*) › table1,table2 ⏎
```

When prompted for the `Poll interval (seconds)`, press return (⏎) to accept the
default value or enter the number of seconds between polling the database for
new data and press return (⏎).

```sh
? Poll interval (seconds): (5) › ⏎
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

After you have added the MySQL source to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the MySQL source listed in the sources
section.

