---
sidebar_position: 4
id: sqlite-replication
title: SQLite Replication
---

# SQLite Replication

The SQLite Replication source allows you to read data from a SQLite database for
the purpose of fully replicating a SQLite database. 

To use the SQLite Replication source, you will need to install the Mycelial
Daemon on the computer that has the SQLite database. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

Full replication of a SQLite database is accomplished with the help of a SQLite
extension we maintain named [Mycelite](https://github.com/mycelial/mycelite).

You'll need to download and load the Mycelite extension into your SQLite
database sessions. The output of Mycelite is a journal file that is written to
disk. The journal file is used to replicate the SQLite database.

## Configuration


The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add SQLite as a data source,
you will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
[[sources]]
type = "sqlite_physical_replication"
display_name = "Sqlite Physical Replication Source"
journal_path = "/path/to/sqlite/journal"
```

### type

The `type` field specifies the type of data source, in this case it is
`sqlite_physical_replication`.


### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### journal_path

When you load the Mycelite extension into your SQLite database sessions, you'll
see a journal file written to disk, which is a sibling to the SQLite database.
The `journal_path` field is the path to that journal file.

Refer to the below section on [Setting up Mycelite](#setting-up-mycelite) for 
more information on how to download and load the Mycelite extension.

## Configuration via CLI

### Prerequisites

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
highlight `Add Source` and press return (⏎).

```sh
? What would you like to do? ›
❯ Add Source ⏎
  Add Destination
  Exit
```


When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Full SQLite replication source` and press return (⏎).

```sh
? What type of source would you like to add? ›
❯ Full SQLite replication source ⏎
  Append only SQLite source
  Excel source
  Append only Postgres source 
  Append only MySQL source
  File source
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (Postgres Source) › ⏎
```

When prompted for the `Journal Path` enter the path to the journal file and
press return (⏎).

```sh
? Journal Path: (data.db-mycelial) › /path/to/sqlite/journal ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit ⏎
```

After exiting the CLI will generate a `config.toml`.

### Appending to an existing `config.toml` file

If you already have a `config.toml` file, you can use the Mycelial CLI to add
the Full SQLite replication source. To do this, run the following command from
the same directory as the `config.toml` file:

```sh
mycelial add --source
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Full SQLite replication source` and press return (⏎).

```sh
? What type of source would you like to add? ›
❯ Full SQLite replication source ⏎
  Append only SQLite source
  Excel source 
  Append only Postgres source 
  Append only MySQL source
  File source
  Exit
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (Postgres Source) › ⏎
```

When prompted for the `Journal Path` enter the path to the journal file and
press return (⏎).

```sh
? Journal Path: (data.db-mycelial) › /path/to/sqlite/journal ⏎
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Exit` and press return (⏎).

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
  Append only SQLite source
  Excel source 
  Append only Postgres source
  Append only MySQL source
  File source
❯ Exit ⏎
```

After exiting the CLI will save the modified `config.toml`.

## Usage

After you have added the Full SQLite Replication source to your `config.toml`
file, either manually or via the CLI, you can
[start](../getting-started/CLI.md#starting) the Mycelial Daemon.  Once the
daemon is running, you can open the Mycelial control plane web interface and you
should see the SQLite source listed in the sources section.

### Setting up Mycelite

#### Downloading Mycelite

Download and unarchive Mycelite for your system:

<details>
  <summary>Mac</summary>
  <details>
    <summary>Mac Arm64</summary>

  ```sh
  curl -L https://github.com/mycelial/mycelite/releases/latest/download/aarch64-apple-darwin.tgz --output aarch64-apple-darwin.tgz
  tar -xvzf aarch64-apple-darwin.tgz
  ```

  </details>
  <details>
    <summary>Mac x86_64</summary>

  ```sh
  curl -L https://github.com/mycelial/mycelite/releases/latest/download/x86_64-apple-darwin.tgz --output x86_64-apple-darwin.tgz
  tar -xvzf x86_64-apple-darwin.tgz
  ```
  </details>
</details>

<details>
  <summary>Linux</summary>

<details>
  <summary>Linux x86_gnu</summary>

```sh
curl -L https://github.com/mycelial/mycelite/releases/latest/download/x86_64-unknown-linux-gnu.tgz --output x86_64-unknown-linux-gnu.tgz
tar -xvzf x86_64-unknown-linux-gnu.tgz
```
</details>
<details>
  <summary>Linux x86_musl</summary>

```sh
curl -L https://github.com/mycelial/mycelite/releases/latest/download/x86_64-unknown-linux-musl.tgz --output x86_64-unknown-linux-musl.tgz
tar -xvzf x86_64-unknown-linux-musl.tgz
```
</details>

<details>
  <summary>Linux arm_32</summary>

```sh
curl -L https://github.com/mycelial/mycelite/releases/latest/download/arm-unknown-linux-gnueabihf.tgz --output arm-unknown-linux-gnueabihf.tgz
tar -xvzf arm-unknown-linux-gnueabihf.tgz
```
</details>
<details>
  <summary>Linux arm_64</summary>

```sh
curl -L https://github.com/mycelial/mycelite/releases/latest/download/aarch64-unknown-linux-gnu.tgz --output arm-unknown-linux-gnueabihf.tgz
tar -xvzf arm-unknown-linux-gnueabihf.tgz
```
</details>

</details>

### Using Mycelite

After you've downloaded and unarchived the extension, you'll need to load the
extension and open your SQLite database. When the extension is loaded and the
SQLite database is opened, it will create a Mycelite journal file, a sibling
file to the SQLite database file. The journal file is used to synchronize SQLite
databases.

_MacOS users_: The default SQLite that ships with MacOS does not have extensions
enabled. One alternative is to [install
SQLite](https://formulae.brew.sh/formula/sqlite) with
[Homebrew](https://brew.sh/). Be sure to adjust your PATH environmental variable
to point to the SQLite version you installed with Homebrew.

```sh
sqlite3
.load ./libmycelite mycelite_writer
.open data.db
```

**NOTE**: You must load the extension every time you open the source SQLite
database.

After you've loaded the extension and opened the SQLite database, a journal file
will be created. The journal file is used to synchronize SQLite databases.