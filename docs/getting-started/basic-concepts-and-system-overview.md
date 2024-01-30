---
sidebar_position: 1
id: basic-concepts-and-system-overview
title: Basic Concepts and System Overview
---

# Introduction to Mycelial

Mycelial is engineered to address the requirements of data transfer, offering seamless integration with both cloud-based systems, such as Snowflake, and open-source platforms, including Postgres. A distinguishing feature of Mycelial is its capacity to manage edge data, a capability previously unavailable in the market.

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

The control plane's role encompasses the creation and management of data workflows. This entails connecting data sources to their respective destinations. 

- **Hosting Flexibility:** Mycelial provides versatility in terms of control plane hosting, allowing users the choice between utilizing a Mycelial-provided control plane (coming soon) or deploying it on their own infrastructure.

### Configuration of Daemons

Configuration of daemons involves specifying the control plane's address, necessary credentials, and the relevant sources and destinations. Upon activation, the daemon establishes a connection with the control plane and communicates its configured sources and destinations. Alternatively, users may configure the daemon through the control plane's web interface.

### Creating a Data Movement Job

The process of creating a data movement job, or data workflow, is designed to be user-friendly.

- **Interface Options:** Users have the option to visually link a source to a destination using Mycelial's intuitive drag-and-drop web interface or to perform this linkage through API calls.

Once the data workflow is published, the pertinent daemons commence the data transfer in accordance with the specifications of the workflow.

## Practical Demonstration

For an applied learning experience, Mycelial offers a beginner's [tutorial](./tutorial.md).
