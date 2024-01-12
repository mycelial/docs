---
sidebar_position: 2
id: tutorial
title: Tutorial
---

# Mycelial getting started tutorial

In this tutorial you will move data from a SQLite database to a Postgres
database using Mycelial.

## Prerequisites

### Installing SQLite

Install SQLite on your system as described below:

<details>
  <summary>Mac</summary>

  ```sh
  brew install sqlite
  ```
</details>

<details>
  <summary>Linux</summary>
  <h4>Ubuntu/Debian-based systems</h4>

  ```sh
  sudo apt-get install sqlite3
  ```

  <h4>Fedora</h4>

  ```sh
  sudo dnf install sqlite
  ```
  <h4>CentOS/Redhat 7</h4>

  ```sh
  sudo yum install sqlite
  ```

  <h4>CentOS/Redhat 8+</h4>

  ```sh
  sudo dnf install sqlite
  ```
</details>

### Installing Docker

Follow the [instructions here](https://www.docker.com/get-started/) to install docker on your system.

### Install the Mycelial CLI

Follow the below instructions to install the Mycelial CLI:

<details>
  <summary>Mac</summary>

  ```sh
  brew install mycelial/tap/mycelial
  ```

</details>

<details>
  <summary>Linux</summary>

  <h4>Debian Based Linux x86_64</h4>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial_0.5.1_amd64.deb --output mycelial_amd64.deb
  dpkg -i ./mycelial_amd64.deb
  ```

  <h4>Debian Based Linux ARM64</h4>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial_0.5.1_arm64.deb --output mycelial_arm64.deb
  dpkg -i ./mycelial_arm64.deb
  ```

  <h4>Debian Based Linux ARM</h4>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial_0.5.1_armhf.deb --output mycelial_armhf.deb
  dpkg -i ./mycelial_armhf.deb
  ```

  <h4>Redhat Based Linux x86_64</h4>

  ```sh
  yum install https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial-v0.5.1-1.x86_64.rpm 
  ```

  <h4>Redhat Based Linux ARM64</h4>

  ```sh
  yum install https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial-v0.5.1-1.arm64.rpm 
  ```

  <h4>Redhat Based Linux ARM</h4>

  ```sh
  yum install https://github.com/mycelial/cli/releases/download/v0.5.1/mycelial-v0.5.1-1.armhf.rpm
  ```


</details>

## Create a demo directory

```sh
mkdir mycelial-demo
cd mycelial-demo
```

## Creating the source SQLite database

In the command line, open sqlite:

```sh
sqlite3 source.db
```

Create a new users table with the following command:

```sql
CREATE TABLE users(id integer primary key, name text) STRICT;
```

Insert a new row in the `users` table:

```sql
INSERT INTO users(name) VALUES ('James');
```

Exit the SQLite command line program:

```sql
.exit
```

## Setup Postgres

Start Postgres in a docker container with the following command:

```sh
docker run --name postgres-db -e POSTGRES_PASSWORD=secret -p 5432:5432 -d postgres
```

Enter the container and run the `psql` application with the following command:

```sh
docker exec -it postgres-db psql -U postgres
```

Create a new database with the following command:

```sh
CREATE DATABASE tutorial;
```

Exit out of the `psql` application with the following command:

```sh
\q
```

## Download and start the Mycelial Control plane (server) and daemon

Run the following Mycelial CLI command:

```sh
mycelial init --local
```

Running the above command will download both the control plane (server) and the
daemon then you will be prompted with a series of questions. Press enter (⏎) to
accept the default values as shown below:

```sh
? Client Name: (My Client) › ⏎
? Client ID: (client) › ⏎
? Server: (http://localhost:7777) › ⏎
```

When prompted for the token, enter `token`:

```sh
? Security Token: › token ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Source` and press enter.

```sh
? What would you like to do? ›
❯ Add Source
  Add Destination
  Exit
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Append only SQLite source` and press enter.

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
❯ Append only SQLite source
```

When prompted for the `Display Name` press enter to accept the default name.

```sh
? Display name: (SQLite Append Only Source) › ⏎
```

When prompted for the `Database Path`, enter `source.db`.

```sh
? Database Path: (data.db) › source.db ⏎
```

When prompted with `What would you like to do?`, press the down arrow key to 
highlight `Add Destination` then press enter.

```sh
? What would you like to do? ›
  Add Source
❯ Add Destination
  Exit
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to hightlight `Append only Postgres destination` and press enter.

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
  Append only SQLite destination
❯ Append only Postgres destination
  Append only MySQL destination
  Kafka destination
  ...
```

When prompted with `Display name`, press enter to accept the default.

```sh
? Display name: (Postgres Append Only Destination) › ⏎
```

When prompted with `Postgres username`, enter `postgres`

```sh
? Postgres username: (user) > postgres
```

When prompted with `Postgres password`, enter `secret`

```sh
? Postgres password: secret
```

When prompted with `Server address`, press enter to accept the default.

```sh
? Server address: (127.0.0.1) › ⏎
```

When prompted with `Postgres port`, press enter to accept the default.

```sh
? Postgres port: (5432) › ⏎
```

When prompted with `Database name`, enter `tutorial`.

```sh
? Database name: (db) › tutorial
```

When prompted with `What would you like to do?`, press the down arrow to
hightlight `Exit` and press enter.

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit 
```

After Exiting the mycelial `CLI`, a `config.toml` file is created.

Now start both the daemon and control plane by running the command 
`mycelial start`. When prompted for the `Security token` enter `token`.

Next, you'll open up the control plane web interface at `http://localhost:7777`.

When prompted to sign in, enter `token` in the username field and leave the
password field blank, then press enter.

Now you'll need to create pipeline by doing the following steps:

1. Drag and drop the `Source: My Client - SQLite Append Only Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `Destination: My Client - Postgres Append Only Destination` node onto the canvas.
4. Connect the `SQLite Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Postgres Destination` node.
5. Lastly, press `Publish` to start the pipeline.

At this point, the `users` table from the SQLite source database should be
synchronized with the `Postgres` destination database.

You can verify the `users` table exists in the postgres database by running the following commands.


```sh
docker exec -it postgres-db psql -U postgres
```

When you see the `postgres=#` prompt, enter `\c tutorial` to start using the 
tutorial database.

To display the tables enter `\dt`, and you should see the `users` table listed.

To query the users table, enter the following sqlite statement:

```sql
select * from users;
```

After running the above command, you should see user named `James`.

Enter the below command to exit out of the `psql` CLI tool.

```sh
\q
``` 

## Cleanup


Enter the following command to terminate the control plane and the daemon:

```sh
mycelial destroy
```

Run the following commands to stop and remove the Postgres database:

```sh
docker stop postgres-db
docker rm postgres-db
```