---
sidebar_position: 3
id: postgres
title: Postgres
---

# Postgres Append Only

The Postgres source allows you to read data from a Postgres database. Currently,
Mycelial only supports Postgres databases that are append only.

To use the Postgres source, you will need to install the Mycelial Daemon on the
computer that has access to the Postgres database. Refer to the [CLI](../getting-started/CLI.md) documentation for instructions on how to install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Postgres as a data source,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[sources]]
type = "postgres_connector"
display_name = "postgres source"
url = "postgres://user:password@localhost:5432/test"
schema = "public"
tables = "*"
poll_interval = 5
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

### schema

The `schema` field is the name of the schema that contains the tables that you
want to read from. 

### tables

The `tables` field is a comma separated list of tables that you want to read
from. If you wish to read from all tables, then you can use the `*` wildcard.

### poll_interval

The `poll_interval` field is the number of seconds between polling the database
for new data. 

## Usage

After you have added the Postgres source to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the SQLite source listed in the
sources section.
