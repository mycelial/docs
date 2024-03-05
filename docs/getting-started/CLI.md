---
sidebar_position: 3
id: CLI
title: Command Line Interface (CLI)
---

# Mycelial Command Line Interface (CLI)

The CLI application is designed to ease the process of setting up and using
Mycelial, the edge data movement platform. 

At it's core, the CLI application enables users to:
* Download and configure the daemon
* Download and configure the control-plane
* Start, destroy and clean the daemons and control plane
* Install the daemon as a service.

## Installation

Install the Mycelial CLI for your system.

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

## Initialization

Run the following command to download and configure Mycelial.

To download both the daemon (daemon) and the control plane, run the following command:

```sh
mycelial init --local
```

or to download just the daemon or the control plane (server), use the
corresponding options:

```sh
mycelial init --daemon
# mycelial init --control-plane
```

After downloading the binaries, you will be prompted with a series of
configuration questions. For demo purposes, you should accept the default values
when available.

Upon exiting, the `init` step will create a `config.toml` file, which will be
used by the Mycelial daemon (myceliald).

If you would like to name the daemon configuration file something other than the
default (`config.toml`), you can pass the `--config` flag with your desired file
name:

```sh
mycelial init --config my_config.toml
```

Note: if you use a custom config file name (ex. `my_config.toml`), you'll need
to pass the `--config` flag along with your custom config file name to
subsequent CLI commands.

## Starting

Run the following command to start the control plane and daemon.

```sh
mycelial start
```

Or, use the `--daemon` or `--control-plane` options to start them individually.

If you wish to use a custom config file (ex. `my_config.toml`), you should pass
it to the start command like this: `mycelial start --config ./my_config.toml`

When prompted for a token, use the one you used in the `init` step.

After completing this step, you should be able to open the web interface 
`http://localhost:7777`.

## Shutdown

Run the following command to terminate the control plane and daemon.

```sh
mycelial destroy
```

Or, use the `--daemon` or `--control-plane` options to terminate them individually.

## Reset

If you wish to reset the local environment (ie, delete the daemon and/or control
plane SQLite databases), you can run the reset command:

```sh
mycelial reset
```

If you use the `--daemon` or `--control-plane` options, the corresponding database will
be deleted.

If you setup the daemon with a custom config file (ex `my_config.toml`), you
will need to pass the file name with the `--config` flag.

## Adding new sources/destinations

If you've already configured the daemon (ie, created a `config.toml` file), you
can add additional sources and/or destinations by running the following command:

```sh
mycelial add --source 
# or mycelial add --destination
```

As with most other commands, you can specify a custom config file name (ex
`my_config.toml`) with the `--daemon <config_file_name>` flag.

After running this command, you'll be prompted with a series of questions that
will assist you in creating the new source/destination.

## Add daemon as a service

If you wish to run the daemon (Myceliald) as a background service, run the
following command:

```sh
sudo mycelial service add --daemon
```

This will download the latest release of the Mycelial daemon (Myceliald) and 
save it into `/usr/local/bin/myceliald`. Next, it will prompt you with a series
of questions, and upon exiting the command, it will save a configuration file to 
`/etc/mycelial/config.toml`. Lastly, the daemon (Myceliald) will be setup
as a service (systemd etc) and automatically started. 

The location of the daemon (Myceliald) SQLite database is
`/var/lib/mycelial/daemon.db`

If you already have a configuration file that you would like to use with the
daemon service, you can pass the `--config <config_file_name>` flag.

## Remove the daemon service

If you have previously installed the daemon (Myceliald) as a service, you can 
run the following command to remove the service:

```sh
sudo mycelial service remove --daemon
```

By default, the daemon configuration file `/etc/mycelial/config.toml` and the 
associated SQLite file `/var/lib/mycelial/daemon.db` will be left untouched. If
you wish to remove these files, you can pass the `--purge` option.

## Service subcommands

### Status

If you would like to check the status of the daemon (Myceliald) service, you
can run the following command:

```sh
sudo mycelial service status --daemon
```

### Stop

If you would like to stop the daemon (Mycelaild) service, you can run the
following command:

```sh
sudo mycelial service stop --daemon
```

### Start

If you have stopped the daemon (Myceliald) service and you would like to start
it you can run the following command:

```sh
sudo mycelial service start --daemon
```

### Restart

If you need to restart the daemon (Myceliald) service, you can run the following
command:

```sh
sudo mycelial service restart --daemon
```