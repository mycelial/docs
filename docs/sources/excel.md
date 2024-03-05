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
arrow to highlight `Excel source` and press return (⏎).

```sh
? What type of source would you like to add? ›
  SQLite source
❯ Excel source ⏎
  Postgres source
  MySQL source
  File source
  Cancel
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

After exiting the CLI will generate or save the modified `config.toml`.

## Usage

After you have added the Excel source to the `config.toml` file, either manually
or via the CLI, you can [start](../getting-started/CLI.md#starting) the Mycelial
Daemon. Once the daemon is running, you can open the Mycelial control plane web
interface and you should see the Excel source listed in the sources section.
