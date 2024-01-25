---
sidebar_position: 3
id: postgres-to-snowflake
title: Postgres to Snowflake
---

# Postgres to Snowflake tutorial

In this tutorial you will move data from a Postgres database to Snowflake using Mycelial.

## Prerequisites

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

  <details>
  <summary>Debian Based Linux x86_64</summary>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.x86_64.deb --output mycelial_amd64.deb
  dpkg -i ./mycelial_amd64.deb
  ```

  </details>

  <details>
  <summary>Debian Based Linux ARM64</summary>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.arm64.deb --output mycelial_arm64.deb
  dpkg -i ./mycelial_arm64.deb
  ```

  </details>

  <details>
  <summary>Debian Based Linux ARM</summary>

  ```sh
  curl -L https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.armhf.deb --output mycelial_armhf.deb
  dpkg -i ./mycelial_armhf.deb
  ```

  </details>

  <details>
  <summary>Redhat Based Linux x86_64</summary>

  ```sh
  yum install https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.x86_64.rpm 
  ```

  </details>

  <details>
  <summary>Redhat Based Linux ARM64</summary>

  ```sh
  yum install https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.arm64.rpm 
  ```

  </details>

  <details>
  <summary>Redhat Based Linux ARM</summary>

  ```sh
  yum install https://github.com/mycelial/cli/releases/latest/download/mycelial-v-1.armhf.rpm
  ```

  </details>

</details>


## Create a demo directory

```sh
mkdir postgres-to-snowflake
cd postgres-to-snowflake
```

## Create the source Postgres database

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

Connect to the new database with the following command:

```sh
\c tutorial
```

Create a new users table with the following command:

```sql
CREATE TABLE users(id serial primary key, name text);
```

Insert a new row in the `users` table:

```sql
INSERT INTO users(name) VALUES ('James');
```

Exit out of the `psql` application with the following command:

```sh
\q
```

## Download, Configure and Start the Mycelial Control Plane (server) and Daemon (client)

Run the following Mycelial CLI command:

```sh
mycelial init --local
```

Running the above command will download both the control plane (server) and the
daemon then you will be prompted with a series of questions. Press enter (⏎) to
accept the default values as shown below:

```sh
? Daemon Name: (My Daemon)› ⏎
? Daemon ID: (daemon)› ⏎
? Server: (http://localhost:7777) › ⏎
```

When prompted for the token, enter `token`:

```sh
? Security Token: › token ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press enter.

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit
```

After exiting the Mycelial CLI, a `config.toml` file will be created in the current
directory. 

### Add Postgres as a source and Snowflake as a destination

Open the `config.toml` file in your favorite text editor and append the
following configuration to the file:

```toml
[[sources]]
type = "postgres_connector"
display_name = "postgres source"
url = "postgres://postgres:secret@localhost:5432/tutorial"
schema = "public"
tables = "*"
poll_interval = 5

[[destinations]]
type = "snowflake"
display_name = "snowflake destination"
username = "[username]"
password = "[password]"
role = "[role]"
account_identifier = "[myorg-account123]"
warehouse = "[warehouse]"
database = "[database]"
schema = "[schema]"
```

**NOTE:** Replace the bracked values ([]) with the appropriate values for your
Snowflake account.

### Start the Mycelial Control Plane and Daemon

Run the following command to start the Mycelial Control Plane and Daemon:

```sh
mycelial start
```

When prompted with `Security Token:`, enter `token`:

```sh
? Security Token: › token ⏎
```

Now navigate to the Mycelial Control Plane in your browser at [http://localhost:7777](http://localhost:7777).

When prompted for a username and password, enter `token` for for the username

When prompted for a username and password, enter `token` for for the username
and leave the password field blank.

### Create a data pipeline

Now you'll need to create a data pipeline by doing the following steps:

1. Drag and drop the `Source: My Client - Postgres Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `Destination: My Client - Snowflake Destination` node onto the canvas.
4. Connect the `Postgres Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Snowflake Destination` node.
5. Lastly, press `Publish` to start the pipeline.

## Verify the data was replicated

At this point, the `people` worksheet from the Excel source should be
synchronized with the `Snowflake` destination database.

## Cleanup

### Stop the Mycelial Control Plane and Daemon

Run the following command to stop the Mycelial Control Plane and Daemon:

```sh
mycelial destroy
```

### Stop the Postgres database

Run the following commands to stop and remove the Postgres database:

```sh
docker stop postgres-db
docker rm postgres-db
```