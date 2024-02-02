---
sidebar_position: 1
id: excel-to-snowflake
title: Excel to Snowflake
---

# Excel to Snowflake tutorial

This tutorial will walk you through the process of setting up a data workflow
that moves data from an Excel spreadsheet to Snowflake.

## Prerequisites

### Excel

You will need to have a modern version of Excel installed on your system.

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
mkdir excel-demo
cd excel-demo
```

## Create an Excel file

Create a new Excel file and add the following data to the first worksheet:

| Name | Age | Color |
| ---- | --- | ----- |
| John | 25  | Blue  |
| Jane | 30  | Red   |

Rename the worksheet to `people`.

Save the file as `people.xlsx` in the `excel-demo` directory.

## Download, Configure and Start the Mycelial Control Plane and Daemon

Run the following Mycelial CLI command:

```sh
mycelial init --local
```

Running the above command will download both the control plane (control plane) and the
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
highlight `Exit` and press enter.

```sh
? What would you like to do? ›
❯ Add Source ⏎
  Add Destination
  Exit
```

When prompted with `What type of source would you like to add?`, press the down
arrow to highlight `Excel source` and press return.

```sh
? What type of source would you like to add? ›
  Full SQLite replication source
  Append only SQLite source
❯ Excel source ⏎
  Append only Postgres source
  Append only MySQL source
  File source
  Cancel
```

When prompted for the `Display Name` press return to accept the default name.

```sh
? Display name: (Excel Source) › ⏎
```

When prompted for the `Excel Path` enter `people.xlsx` and press return.

```sh
? Excel Path: (data.xlsx) › people.xlsx ⏎
```

When prompted for the `Sheets`, enter `people` and press return.

```sh
? Sheets: (*) › people ⏎
```

When prompted for `Strict`, enter `n` and press return.

```sh
? Strict: (y/n) › no
```

When prompted with `What would you like to do?`, press the down arrow key to
highlight `Add Destination` then press return.

```sh
? What would you like to do? ›
  Add Source
❯ Add Destination ⏎
  Exit
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to hightlight `Snowflake destination` and press return.

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

After exiting the Mycelial CLI, a `config.toml` file will be created in the current
directory. 

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

1. Drag and drop the `Excel Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `Snowflake Destination` node onto the canvas.
4. Connect the `Excel Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Snowflake Destination` node.
5. Lastly, press the `Publish` button to start the workflow.

<img src="/img/tutorial.gif" alt="Workflow creation" width="800"/>

## Verify the data was replicated

At this point, the `people` worksheet from the Excel source should be
synchronized with the `Snowflake` destination database.

## Cleanup

### Stop the Mycelial Control Plane and Daemon

Run the following command to stop the Mycelial Control Plane and Daemon:

```sh
mycelial destroy
```