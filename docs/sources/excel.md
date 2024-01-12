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

**NOTE**: The Excel connector sends the entire dataset to the destination upon 
every update (save). This can have unintended consequences if used with append-only 
destinations such as SQLite.

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

## Usage

After you have added the Excel source to the `config.toml` file, you can
start the Mycelial Daemon. Once the daemon is running, you can open the Mycelial
control plane web interface and you should see the SQLite source listed in the
sources section.