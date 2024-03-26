---
sidebar_position: 6
id: kafka
title: Kafka
---

# Kafka

The Kafka destination allows you to write data to a Kafka topic.

To use the Kafka destination, you will need to install the Mycelial Daemon on
the computer that has access to the Postgres database. Refer to the
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial Daemon.

## Configuration

The Mycelial Daemon uses a TOML configuration file to specify the data sources
and destinations that it has available to it. To add Postgres as a data
destination, you will need to add a section to the TOML file (`config.toml`)
that looks like this:

```toml
[[destinations]]
type = "kafka"
display_name = "Kafka Destination"
brokers = "localhost:9092"
topic = "test"
```

### type

The `type` field specifies the type of data destination, in this case it is
`kafka`.

### display_name

The `display_name` field is the name that will be displayed in the Mycelial user
interface and via the API.

### brokers

The `brokers` field is points to the Kafka brokers. 

### topic

The `topic` field is the Kafka topic that you want to write to.

## Configuration via CLI

You will need to have the Mycelial CLI installed. Refer to the 
[CLI](../getting-started/CLI.md) documentation for instructions on how to
install the Mycelial CLI.

### Create a new `config.toml` file or add to an existing one

If you are creating a new `config.toml` file, you can use the Mycelial CLI [`init`](../getting-started/CLI#initialization) command to generate the file and add the source. 

If you are adding to an existing config file you can use the Mycelial CLI [`add`](../getting-started/CLI#adding-new-sourcesdestinations) command to add the source to the existing config. 

### Choose source config options

When prompted with `What would you like to do?`, press the down arrow to
highlight `Add Destination` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source 
❯ Add Destination ⏎
  Exit
```

When prompted with `What type of destination would you like to add?`, press the
down arrow to highlight `Kafka destination` and press return (⏎).

```sh
? What type of destination would you like to add? ›
  SQLite destination
  Postgres destination 
  MySQL destination
❯ Kafka destination ⏎
  Snowflake destination
  File destination
  Cancel
```

When prompted for the `Display Name` press return (⏎) to accept the default or
enter a name for your destination and press return (⏎).

```sh
? Display name: (Kafka Destination) › ⏎
```

When prompted for the `Brokers:` press return (⏎) to accept the default value or
enter the URL and port number of the Kafka brokers and press return (⏎).

```sh
? Broker: (localhost:9092) › ⏎
```

When prompted for the `Topic:` press return (⏎) to accept the default value or
enter the name of the Kafka topic and press return (⏎).

```sh
? Topic: (test) ›
```

When prompted with `What would you like to do?`, press the down arrow to
highlight `Exit` and press return (⏎).

```sh
? What would you like to do? ›
  Add Source
  Add Destination
❯ Exit
```

After exiting the CLI will generate or save the modified `config.toml`.

## Usage

After you have added the Kafka destination to the `config.toml` file, either
manually or via the CLI, you can [start](../getting-started/CLI.md#starting) the
Mycelial Daemon. Once the daemon is running, you can open the Mycelial control
plane web interface and you should see the Kafka destination listed in the
destinations section.
