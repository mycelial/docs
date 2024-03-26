---
sidebar_position: 1
id: basic-concepts-and-system-overview
title: Basic Concepts and System Overview
---

# Introduction to Mycelial

Mycelial is engineered to move data. It seamlessly integrates with:
 * Cloud-based systems (Snowflake, Kafka, Redshift, ...)
 * Open-source platforms (Postgres, Mysql, ...)
 * Local data sources (SQLite, Excel, local files, ...)
 
Mycelial distinguishes itself by taking an edge data first approach to data movement. 

# Mycelial Functionality

Mycelial is comprised of two primary software components: 

1. **Control Plane (Server)**
2. **One or More Daemons**

## Daemons

The daemons serve as the primary agents in Mycelial, tasked with extracting data from sources and injecting it into destination systems. 

- **Optimal Performance:** For optimal performance, the placement of the daemon is critical; ideally it should be situated proximal to the data source or destination.
- **Networked Sources/Destinations:** In scenarios involving networked sources or destinations, the daemon can be deployed on an adjacent computer.
- **Cloud-Managed Daemons:** Alternatively, users may utilize the forthcoming cloud-managed daemons.
- **Edge Data Sources:** For edge data sources, such as SQLite, the daemon is installed directly on the device hosting the data source.

## Control Plane

The Control Plane is responsible for creating and managing the data workflows that will be executed by the Daemons. This entails connecting data sources to their respective destinations. 

- **Hosting Flexibility:** Mycelial provides versatility in terms of Control Plane hosting, allowing users the choice between utilizing a Mycelial-provided Control Plane with the [SaaS App](https://app.mycelial.com) or deploying it on their own infrastructure.

### Configuration of Daemons

Daemons are responsible for connecting to sources and destinations and executing data workflows as provided by the Control Plane. 

Configuration of the Daemons involves specifying the Control Plane's address, necessary credentials, and the relevant sources and destinations. Upon activation, the Daemon establishes a connection with the Control Plane and communicates its configured sources and destinations. Alternatively, users may configure the Daemon through the control plane's web interface.

### Creating a Data Movement Job

The process of creating a data movement job, or data workflow, is designed to be user-friendly.

- **Interface Options:** Users have the option to visually link a source to a destination using Mycelial's intuitive drag-and-drop web interface or to perform this linkage through API calls.

Once the data workflow is published, the pertinent Daemons commence the data transfer in accordance with the specifications of the workflow.

## Practical Demonstration

For an applied learning experience, Mycelial offers a beginner's [tutorial](./tutorial.md).
