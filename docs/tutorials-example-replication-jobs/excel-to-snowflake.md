---
sidebar_position: 1
id: excel-to-snowflake
title: Excel to Snowflake
---

# Excel to Snowflake tutorial

This tutorial will walk you through the process of setting up a data pipeline
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
mkdir excel-demo
cd excel-demo
```

## Create an Excel file

Create a new Excel file and add the following data to the first worksheet:

| Name | Age | Favorite Color |
| ---- | --- | -------------- |
| John | 25  | Blue           |
| Jane | 30  | Red            |

Rename the worksheet to `people`.

Save the file as `people.xlsx` in the `excel-demo` directory.

## Download, Configure and Start the Mycelial Control Plane (server) and Daemon (client)

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
highlight `Exit` and press enter.

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit
```

After exiting the Mycelial CLI, a `config.toml` file will be created in the current
directory. 

### Add Excel as a source and Snowflake as a destination

Open the `config.toml` file in your favorite text editor and append the
following configuration to the file:

```toml
[[sources]]
type = "excel_connector"
display_name = "Excel People Source"
path = "people.xlsx" 
strict = false
sheets = "poeple"

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

Now navigate to the Mycelial Control Plane in your browser at `http://localhost:7777`.

When prompted for a username and password, enter `token` for for the username
and leave the password field blank.

### Create a data pipeline

Now you'll need to create a data pipeline by doing the following steps:

1. Drag and drop the `Source: My Client - Excel People Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `Destination: My Client - Snowflake Destination` node onto the canvas.
4. Connect the `Excel People Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Snowflake Destination` node.
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