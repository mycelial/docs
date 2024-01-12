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

## Usage

After you have added the Postgres destination to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the Postgres destination listed in
the destinations section.