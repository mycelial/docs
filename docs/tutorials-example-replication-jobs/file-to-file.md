---
sidebar_position: 5
id: file-to-file
title: File to File
---

# File to File tutorial

In this tutorial you will move data from a file to another file using Mycelial.

## Prerequisites

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
mkdir file-to-file
cd file-to-file
```

## Download, Configure and Start the Mycelial Control Plane and Daemon 

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
arrow to highlight `File source` and press return.

```sh
? What type of source would you like to add? ›
  Append only SQLite source
  Excel source
  Append only Postgres source 
  Append only MySQL source 
❯ File source ⏎
  Cancel
```

When prompted for the `Display Name` press return to accept the default name.

```sh
? Display name: (file source) › ⏎
```

When prompted for the `Path` enter `input.txt` and press return.

```sh
? Path: (file.txt) › input.txt ⏎
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
  Append only SQLite destination
  Append only Postgres destination
  Append only MySQL destination
  Kafka destination
  Snowflake destination 
❯ File destination ⏎
  Cancel
```

When prompted for the `Display Name` press return to accept the default name.

```sh
? Display name: (file destination) › ⏎
```

When prompted for the `Path` enter `output.txt` and press return.

```sh
? Path: (file.txt) › output.txt ⏎
```

When prompted with `What would you like to do?`, press the down arrow to
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

Create the input file `input.txt` with the following content:

```sh
echo "Hello, World!" > input.txt
```

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
and leave the password field blank.

### Create a data workflow

Now you'll need to create a data workflow by doing the following steps:

1. Drag and drop the `File Source` node onto the canvas.
2. Drag and drop the `Mycelial Server` node onto the canvas.
3. Drag and drop the `File Destination` node onto the canvas.
4. Connect the `Postgres Source` to the `Mycelial Server` and then connect the `Mycelial Server` to the `Snowflake Destination` node.
5. Lastly, press `Publish` to start the workflow.

<img src="/img/file_to_file_tutorial.gif" alt="Workflow creation" width="800"/>

## Verify the data was replicated

At this point the data should have been replicated from the `input.txt` file to the `output.txt` file. You can verify this by running the following command:

```sh
cat output.txt
```

## Cleanup

### Stop the Mycelial Control Plane and Daemon

Run the following command to stop the Mycelial Control Plane and Daemon:

```sh
mycelial destroy
```
