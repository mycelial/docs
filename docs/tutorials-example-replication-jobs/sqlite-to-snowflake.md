---
sidebar_position: 2
id: sqlite-to-snowflake
title: SQLite to Snowflake
---

# SQLite to Snowflake tutorial

This tutorial will walk you through the process of setting up a data workflow
that moves data from a SQLite database to Snowflake.

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

## Download, Configure and Start the Mycelial Control Plane (server) and Daemon

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
? Control Plane: (http://localhost:7777) › ⏎
```

When prompted for the token, enter `token`:

```sh
? Security Token: › token ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Source` and press enter.

```sh
? What would you like to do? ›
❯ Add Source ⏎
  Add Destination
  Exit
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Append only SQLite source` and press enter.

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
❯ Append only SQLite source ⏎
  Excel source
  Append only Postgres source
  Append only MySQL source
  File source
  Cancel
```

When prompted for the `Display Name` press enter to accept the default name.

```sh
? Display name: (SQLite Append Only Source) › ⏎
```

When prompted for the `Tables` press enter to accept the default value.

```sh
? Tables: (*) › ⏎
```

When prompted for the `Database Path`, enter `source.db`.

```sh
? Database Path: (data.db) › source.db ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
hightlight `Add Destination` and press enter.

```sh
? What would you like to do? ›
  Add Source
❯ Add Destination ⏎
  Exit 
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to hightlight `Snowflake destination` and press enter.

```sh
? What type of destination would you like to add? ›
  Full SQLite replication destination
  Append only SQLite destination
  Append only Postgres destination
  Append only MySQL destination
  Kafka destination
❯ Snowflake destination ⏎
  File destination
  Cancel
```

When prompted for the `Display Name` press return to accept the default name.

```sh
? Display name: (Snowflake Destination) › ⏎
```

When prompted for the `Snowflake username`, enter your Snowflake username and
press return.

```sh
? Snowflake username: › [username] ⏎
```

When prompted for the `Snowflake password`, enter your Snowflake password and
press return.

```sh
? Snowflake password: › [password] ⏎
```

When prompted for the `Snowflake role`, enter your Snowflake role and press
return.

```sh
? Snowflake role: › [role] ⏎
```

When prompted for the `Snowflake account name`, enter your Snowflake account
name and press return.

```sh
? Snowflake account name: › [account123] ⏎
```

When prompted for the `Snowflake organization name`, enter your Snowflake
organization name and press return.

```sh
? Snowflake organization name: › [myorg] ⏎
```

When prompted for the `Snowflake warehouse`, enter your Snowflake warehouse and

```sh
? Snowflake warehouse: › [warehouse] ⏎
```

When prompted for the `Database name`, enter your Snowflake database name and
press return.

```sh
? Database name: › [database] ⏎
```

When prompted for the `Schema`, enter your Snowflake schema name and press return.

```sh
? Schema: › [schema] ⏎
```

When prompted with `What would you like to do?`, press the down arrow key to
highlight `Exit` then press return.

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit ⏎
```

After Exiting the mycelial `CLI`, a `config.toml` file is created.

### Start the Mycelial Control Plane and Daemon

Run the following command to start the Mycelial Control Plane and Daemon:

```sh
mycelial start
```

When prompted with `Security Token:`, enter `token`:

```sh
? Security Token: › token ⏎
```

Now navigate to the Mycelial Control Plane in your browser at [`http://localhost:7777`](http://localhost:7777).

When prompted for a username and password, enter `token` for for the username
and leave the password field blank.

### Create a data workflow

Now you'll need to create a data workflow by doing the following steps:

1. Drag and drop the `SQLite Append Only Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `Snowflake Destination` node onto the canvas.
4. Connect the `SQLite Append Only Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Snowflake Destination` node.
5. Lastly, press `Publish` to start the workflow.

<img src="/img/excel_to_snowflake_tutorial.gif" alt="Workflow creation" width="800"/>

## Verify the data was replicated

At this point, the `users` table from the SQLite source should be
synchronized with the `Snowflake` destination database.

## Cleanup

### Stop the Mycelial Control Plane and Daemon

Run the following command to stop the Mycelial Control Plane and Daemon:

```sh
mycelial destroy
```