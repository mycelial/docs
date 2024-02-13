---
sidebar_position: 1
id: excel
title: Excel
---
# Excel Data Source

You can use Excel as a data source for Mycelial. To do this, you will need to 
install the Mycelial Daemon on a computer that has access to the Excel file. 
Refer to the [CLI](../getting-started/CLI.md) documentation for instructions on
how to install the Mycelial Daemon.

:::danger Note
The Excel connector sends the entire dataset to the destination upon 
every update (save). This can have unintended consequences if used with append-only 
destinations such as SQLite.
:::

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Excel as a data source, you
will need to add a section to the TOML file (`config.toml`) that looks like
this:

```toml
...
[[sources]]
type = "excel_connector"
display_name = "Excel Source"
path = "/path/to/excel/file.xlsx" # or glob "/path/to/excel/files/**/*.xlsx"
strict = false
sheets = "Sheet1,Sheet2" # or "*" for all sheets
```

**NOTE**: You can manually edit the `config.toml` file to include the Excel
source or you can use the Mycelial CLI to add the source. To use the CLI, to 
add the Excel source, refer to the [instructions below](#configuration-via-cli).

### type
The `type` field specifies the type of data source, in this case it is 
`excel_connector`. 

### display_name
The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### path
The `path` field is the path to the Excel file.  You can provide a path to a
specific file or you can use a
[GLOB](https://en.wikipedia.org/wiki/Glob_(programming)) pattern to specify a
set of Excel files. For example, you could use the following path to specify all
Excel files in a directory: `/path/to/excel/files/*.xlsx` or you could use the
following path to specify all Excel files in a directory and all subdirectories:
`/path/to/excel/files/**/*.xlsx`.

### strict

The `strict` field deals with handling mixed data types in a column. If `strict`
is set to `true`, then Mycelial will attempt to maintain the data type of the
cells. 

If `strict` is set to `false`, then Mycelial will attempt to convert all cells
to a string.

### sheets

The `sheets` field is a comma separated list of sheet names that you wish to
sync. If you wish to sync all sheets, then you can use the `*` wildcard.

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
arrow to highlight `Excel source` and press return (⏎).

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
  Append only SQLite source
❯ Excel source ⏎
  Append only Postgres source
  Append only MySQL source
  File source
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (Excel Source) › ⏎
```

When prompted for the `Path` enter the path to the Excel file or a GLOB pattern
to specify a set of Excel files. For example, you could use the following path
to specify a specific Excel file: `/path/to/excel/file.xlsx` or you could use
the following path to specify all Excel files in a directory:
`/path/to/excel/files/*.xlsx` or you could use the following path to specify all
Excel files in a directory and all subdirectories:
`/path/to/excel/files/**/*.xlsx`.

```sh
? Excel Path: (data.xlsx) › /path/to/excel/file.xlsx ⏎
```

When prompted for the `Sheets` press return (⏎) to accept the default (*) for
all sheets or enter a comma separated list of sheet names that you wish to
export.

```sh
? Sheets: (*) › ⏎
```

When prompted for the `Strict` enter `y` or `n`. The `strict` field deals with
handling mixed data types in a column. If `strict` is set to `true`, then
Mycelial will attempt to maintain the data type of the cells in a column. If
`strict` is set to `false`, then Mycelial will attempt to convert all cells to a
string.

```sh
? Strict: (y/n) › no ⏎
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
the Excel source. To do this, run the following command from the same directory
as the `config.toml` file:

```sh
mycelial add --source
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Excel source` and press return (⏎).

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
  Append only SQLite source
❯ Excel source ⏎
  Append only Postgres source
  Append only MySQL source
  File source
  Exit
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a display name and press return (⏎) . The display name is the name that
will be displayed in the Mycelial user interface and via the API.

```sh
? Display name: (Excel Source) ›
```

When prompted for the `Path` enter the path to the Excel file or a GLOB pattern
to specify a set of Excel files. For example, you could use the following path
to specify a specific Excel file: `/path/to/excel/file.xlsx` or you could use
the following path to specify all Excel files in a directory:
`/path/to/excel/files/*.xlsx` or you could use the following path to specify all
Excel files in a directory and all subdirectories:
`/path/to/excel/files/**/*.xlsx`.

```sh
? Excel Path: (data.xlsx) › /path/to/excel/file.xlsx ⏎
```

When prompted for the `Sheets` press return (⏎) to accept the default (*) for
all sheets or enter a comma separated list of sheet names that you wish to
export.

```sh
? Sheets: (*) › ⏎
```

When prompted for the `Strict` enter `y` or `n`. The `strict` field deals with
handling mixed data types in a column. If `strict` is set to `true`, then
Mycelial will attempt to maintain the data type of the cells in a column. If
`strict` is set to `false`, then Mycelial will attempt to convert all cells to a
string.

```sh
? Strict: (y/n) › no ⏎
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

After you have added the Excel source to the `config.toml` file, either manually
or via the CLI, you can [start](../getting-started/CLI.md#starting) the Mycelial
Daemon. Once the daemon is running, you can open the Mycelial control plane web
interface and you should see the Excel source listed in the sources section.
