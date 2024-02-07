---
sidebar_position: 4
---

# Frequently Asked Questions

<details>
  <summary>What do I need to get started using Mycelial?</summary>

  You can use Mycelial today and you don't even need to create an account.
  Follow this [tutorial](./tutorial.md) to start using Mycelial right now.

</details>

<details>
  <summary>What data sources/destinations does Mycelial offer connectors for?</summary>

  You can see the sources and destinations that Mycelial supports 
  here in the documentation under sources and destinations.

</details>

<details>
  <summary>What if I don't see a data source/destination that I need?</summary>

  Please connect with us on [Discord](https://discord.gg/mycelial) and ask about
  the source/destination that you need.

</details>

<details>
  <summary>Which data warehouse should I use?</summary>

  Mycelial supports multiple warehouses including: Snowflake, MySQL, PostgreSQL 
  and Redshift. More data warehouses are in the process of being added, reach 
  out to us on [Discord](https://discord.gg/mycelial) to learn more.
</details>

<details>
  <summary>What is the Mycelial daemon?</summary>

The Mycelial daemon is a small binary, written in Rust, that is responsible for
pulling data from sources and/or pushing data to destinations. You typically
install the daemon near the source/destination, using our CLI.

</details>

<details>
  <summary>What is the Mycelial control plane?</summary>

The Mycelial control plane is a server that orchestrates data workflow jobs.
You can either install the control plane on one of your servers, using our CLI
or you can use our cloud-based control plane (coming soon). 

</details>

<details>
  <summary>How do you configure data sources and destinations?</summary>

Each daemon has a corresponding `config.toml` file. The config file contains 
information about:
1. The daemon, such as it's name and unique id, the associated.
2. The control plane, such as it's address and security token.
3. The sources and/or destinations available to the daemon.

You can create the `config.toml` file manually, but it's easier to 
create the config by using the Mycelial CLI.

</details>

<details>
  <summary>How do you connect data sources to destinations?</summary>

After you have configured and started your daemons, the daemons will connect
with the control plane and publish their available sources and destinations.
Next, you'll open the web interface to the control plane and then you'll drag 
and drop the sources and destinations you wish to connect onto the canvas, then
you'll connect the nodes to create a data workflow and finally you'll publish
your workflow.

</details>

<details>
  <summary>What's the best way to try out Mycelial?</summary>

We've got a full [tutorial](./tutorial.md) that demonstrates connecting a SQLite
data source to a postgres destination.

</details>

<details>
  <summary>Can I connect different types of sources and destinations?</summary>

  Yes, Mycelial is designed to move data between disparate data systems.

</details>
