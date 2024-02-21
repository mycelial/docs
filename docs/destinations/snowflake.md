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

The `type` field specifies the type of data destination, in this case it is
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

## Configuration via CLI

You will need to have the Mycelial CLI installed. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Creating a new `config.toml` file

If you are creating a new `config.toml` file, you can use the Mycelial CLI to
generate the file and add the Postgres destination. To do this, run the
following command:

```sh
mycelial init --local
```

Running the above command will download both the [Control
plane](../core-concepts/Control-Plane) and the
[Daemon](../core-concepts/Daemon.md) and it will ask you a series of questions
to generate the `config.toml` file.

When prompted for the `Daemon Name:` press return (⏎) to accept the default
value or enter a name for your daemon and press return (⏎).

```sh
? Daemon Name: (My Daemon)› ⏎
```

When prompted for the `Daemon ID:` press return (⏎) to accept the default value
or enter a daemon ID and press return (⏎).

```sh
? Daemon ID: (daemon)› ⏎
```

When prompted for the `Control Plane:` press return (⏎) to accept the default value or
enter the URL of the control plane and press return (⏎). If you are just trying
out Mycelial, you should press return (⏎) to accept the default value.

```sh
? Control Plane: (http://localhost:7777) › ⏎
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
  Append only SQLite destination
  Append only Postgres destination 
  Append only MySQL destination
❯ Kafka destination ⏎
  Snowflake destination
  File destination
  Cancel
```

When prompted for the `Display Name:` press return (⏎) to accept the default or
enter a display name for your destination and press return (⏎).

```sh
? Display name: (Snowflake Destination) ›
```

When prompted for the `Snowflake username:` enter the username for the Snowflake
account you wish to use.

```sh
? Snowflake username: › snowflake_user ⏎
```

When prompted for the `Snowflake password:` enter the password for the Snowflake
account you wish to use.

```sh
? Snowflake password: › password ⏎
```

When prompted for the `Snowflake role:` enter the role for the Snowflake account
you wish to use.

```sh
? Snowflake role: ACCOUNTADMIN ⏎
```

When prompted for the `Snowflake account name:` enter the account name for the
Snowflake account you wish to use.

```
? Snowflake account name: › account123 ⏎
```

When prompted for the `Snowflake orgnization name:` enter the organization name
for the Snowflake account you wish to use.

```sh
? Snowflake organization name: › myorg ⏎
```

When prompted for the `Snowflake warehouse:` enter the warehouse you wish to use.

```sh
? Snowflake warehouse: › COMPUTE_WH ⏎
```

When prompted for the `Database name:` enter the database you wish to use.

```sh
? Database name: › mydb ⏎
```

When prompted for the `Schema:` enter the schema you wish to use.

```sh
? Schema: › PUBLIC ⏎
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
the Postgres destination. To do this, run the following command from the same
directory as the `config.toml` file:

```sh
mycelial add --destination
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Append only Postgres destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  Append only SQLite destination
  Append only Postgres destination 
  Append only MySQL destination
  Kafka destination
❯ Snowflake destination ⏎
  File destination
  Exit
```

When prompted for the `Display Name:` press return (⏎) to accept the default or
enter a display name for your destination and press return (⏎).

```sh
? Display name: (Snowflake Destination) ›
```

When prompted for the `Snowflake username:` enter the username for the Snowflake
account you wish to use.

```sh
? Snowflake username: › snowflake_user ⏎
```

When prompted for the `Snowflake password:` enter the password for the Snowflake
account you wish to use.

```sh
? Snowflake password: › password ⏎
```

When prompted for the `Snowflake role:` enter the role for the Snowflake account
you wish to use.

```sh
? Snowflake role: ACCOUNTADMIN ⏎
```

When prompted for the `Snowflake account name:` enter the account name for the
Snowflake account you wish to use.

```
? Snowflake account name: › account123 ⏎
```

When prompted for the `Snowflake orgnization name:` enter the organization name
for the Snowflake account you wish to use.

```sh
? Snowflake organization name: › myorg ⏎
```

When prompted for the `Snowflake warehouse:` enter the warehouse you wish to use.

```sh
? Snowflake warehouse: › COMPUTE_WH ⏎
```

When prompted for the `Database name:` enter the database you wish to use.

```sh
? Database name: › mydb ⏎
```

When prompted for the `Schema:` enter the schema you wish to use.

```sh
? Schema: › PUBLIC ⏎
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Exit` and press return (⏎).

```sh
? What type of destination would you like to add? ›
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

After you have added the Snowflake destination to the `config.toml` file, you
can start the Mycelial Daemon. Once the daemon is running, you can open the
Mycelial control plane web interface and you should see the Snowflake
destination listed in the destinations section.