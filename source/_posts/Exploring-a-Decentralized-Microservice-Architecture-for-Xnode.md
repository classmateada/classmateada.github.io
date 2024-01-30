---
title: Exploring a Decentralized Microservice Architecture for Xnode
lang: en
date: 2024-01-24 18:32:19
categories:
    - Software architecture
tags:
    - Software architecture
    - Research reports
---

## Clarification

This is a research report I wrote for Openmesh in January 2024. I worked as a software architect and designed the whole decentralised architecture for the Xnode overlay network, as well as supporting other research projects and providing some suggestions for the succeeding development process.

Please be aware that this is just the raw version of the initial architectural design, and the content may be outdated, buggy, or not accurate.

Link to the original post: [https://blog.openmesh.network/raw-research-exploring-a-decentralized-microservice-architecture-for-xnode-946600b7d50a](https://blog.openmesh.network/raw-research-exploring-a-decentralized-microservice-architecture-for-xnode-946600b7d50a)

## Initial Project Plan Structure

> **The Decentralized Microservice Architecture of Xnode**
>
> Operating as a microservice, each Xnode contributes to the network by offering computational power and storage, and participating in essential processes like data verification and consensus maintenance

### Short Project Description

This project aims to give a high-level description of the design and structure of Xnode, demonstrate its design philosophy, and also provide instructions and suggestions for its design and development process.

### Overview of the Main Solution

#### The Microservice Architecture

Getting a lot of attention in the tech world, the microservice architecture is one of the most commonly used distributed architectures. In a nutshell, the microservice architecture is a service-oriented software architecture that merges several single-purpose light-weight small back-end services into a large-scale distributed system.

The main benefits of using the microservice architecture include:

- **Minimise design/runtime coupling**. Microservices are independent, flexible, and independently deployable without any runtime dependencies or code dependencies.
- **Fault tolerance and fault isolation**. When one service fails, the others remain unaffected and are still functioning, minimizing the influence of the failure.
- **Highly scalable**. Microservices are loosely coupled, which means that they can be easily scaled up.
- **Easy update**. A single microservice can be updated or replaced without rebuilding and redeploying the whole system.
- **Tech Stack Flexibility**. Different microservices can be developed using different technology stacks, libraries, and frameworks.

#### The Architecture of Xnode

Xnode is based on a microservice-like distributed P2P architecture, which means that it benefits from the advantages of the microservice architecture. By adjusting the traditional microservice architecture into a decentralised one, Xnode also avoids some of the disadvantages of the microservice architecture.

The detailed architecture will be demonstrated in the following sections.

### Project Scope

This project is focused on the Xnode overlay network (or Xnode virtual network). It doesn’t focus on a single Xnode or a single Xnode cluster.

The main outcome and accomplishment of this project is to provide a detailed solution to the architectural design of Xnode, especially the Xnode overlay network. This project is also a prerequisite for the development, testing, and deployment of Xnode, providing instructions for those processes, especially in the infrastructure layer.

### Overview Diagram of the Final Solution

#### Strongly Consistent Data Sharing

<img src="https://miro.medium.com/v2/resize:fit:2000/0*Be_fEKR0A5yz03M6" alt="img" style="zoom:50%;" />

#### Resource Locating and Mapping

<img src="https://miro.medium.com/v2/resize:fit:2000/0*5iXoRY4nMTEnx-ck" alt="img" style="zoom:50%;" />

#### Eventual Consistent Data Sharing

<img src="https://miro.medium.com/v2/resize:fit:2000/0*YiEZJD7rWCXAUvzS" alt="img" style="zoom:50%;" />

### Main Outcomes of the Project

- **Technical Capabilities**:
  - **Global overlay network**. The Xnode overlay network is the basis of the Xnode global virtualized network.
  - **High-level demonstration of Xnode overlay network**. This project shows how the Xnode overlay network forms, giving a high-level demonstration of this complicated distributed system.

- **Functions and Features**:
  - **Supporting the Openmesh protocol**. The Xnode overlay network performs as an infrastructure for the Openmesh protocol, providing virtualized computing and storage for Openmesh services.
  - **Giving instructions for the development and maintenance**. Architectural design is the prerequisite for development and maintenance processes. It provides a high-level overview of the whole project, making it easier to understand how a large-scale distributed system works.

- **Innovations**:
  - **Implementing a large-scale decentralized architecture**. Large-scale decentralized architectures are quite novel and don’t have much successful implementation throughout the world. By implementing the Xnode overlay network, we will provide a successful use case for a large-scale decentralized architecture.
  - **Showing that cloud infrastructure serves real needs**. With the development of cloud computing, a lot of software architects are choosing middleware and infrastructure based on their preferences, regardless of the technical requirements and real needs. The design of the Xnode overlay network will be a good example to emphasise that cloud infrastructure should serve real needs instead of personal preferences.


### Use Cases

- Use Case 1: **Data Redundancy**
  - **Explanation**: The architecture can ensure the redundancy and reliability of data since Openmesh aims to provide highly reliable data services.
  - **Successful Scenario**: With no more than ⅓ nodes failing, the architecture should ensure the system is still functioning with no data loss, and the other nodes remain unaffected.

- Use Case 2: **Handling Massive Data Transfer and Storage**
  - **Explanation**: As a cloud infrastructure, the Xnode overlay network should be able to transfer, find, and store the data collected by Unified API in an efficient and reliable way.
  - **Successful Scenario**: New data should be transferred to the target storage server determined by a resource locating service. The integrity of data will be guaranteed, with no possibility of data loss.

- Use Case 3: **Virtualization Support**
  - **Explanation**: Performing as the basis of Xnode virtualized network, the architecture can provide support to the virtualization layer.
  - **Successful Scenario**: The architecture provides a resource locating service or protocol, supporting the resource mapping and locating needs of the virtualization layer.

- Use Case 4: **Data Verification**
  - **Explanation**: The data stored in the system should be correct with strong consistency.
  - **Successful Scenario**: The architecture provides a kind of verification service based on a failure-tolerant strongly consistent distributed coordination protocol.

- Use Case 5: **Decentralized Data Sharing**
  - **Explanation**: One of the most important design philosophies is truly decentralization. The architecture should be completely decentralized and democratic, with no likelihood of middlemen or centralized control.
  - **Successful Scenario**: The system based on the architecture is decentralized. Every node in the network is equally privileged, with the node itself and the data stored in it governed by the community.


### Target Audience/Main Users

- **Cloud Infrastructure Engineers**.
  - **Example**: The developers of Xnode overlay network and Xnode virtualized network.
  - **Use case**: Cloud infrastructure engineers will get instructions in the design and development of detailed functions of Xnode overlay network from this architectural design. They can also get a better understanding of the whole Xnode overlay network.
- **Maintainers**
  - **Example**: The maintainers of Openmesh services.
  - **Use case**: The maintainers will know the architecture of Xnode overlay network from this project, which means they will quickly pinpoint the reliability issues within the services based on it.
- **Openmesh Service Developers**.
  - **Example**: The developers of Unified API, Pythia, and other Openmesh services.
  - **Use case**: This project can help those developers get a better understanding of the infrastructure that supports those services and make more appropriate designs of those services that benefit from the Xnode overlay network.

## Initial Suggestions and Planning

### High-Level Breakdown of Project Development

1. **Conceptualization**: Define the Xnode overlay network and the services or components within it.
2. **Design**: Design an appropriate architecture for the Xnode overlay network and the services inside it.
3. **Development**:
   1. Implement the architecture of each service using the suggested technology stack, or alter the technology stack based on the real need.
   2. Implement whole Xnode overlay network.

4. **Testing**: Test a small scale Xnode network, ensuring it meets the functional and non-functional requirements.
5. **Deployment**: Deploy the Xnode overlay network.

### System Architecture

Obviously, the Xnode overlay network is:

1. **A distributed system**. The Xnode overlay network is naturally a highly distributed system because Xnodes in the network will be separated globally and governed by community.
2. **P2P and based on the microservice architecture**. When forming the overlay network, each Xnode is equally privileged, contributes to the network independently, and performs as a microservice.
3. **Decentralized**. Decentralization is one of the most important design philosophies of Xnode and should always be considered during the whole design and development process.

A single Xnode is similar to a traditional microservice, and it contributes to the network by donating computational power and storage. However, the architecture of the Xnode overlay network is not really similar to the (traditional) microservice architecture. The architecture of the Xnode overlay network can be divided into three parts:

#### Consensus and Strongly Consistent Data Sharing Services

Architecture: **BFT-based Proof-of-Stake (PoS)**.

In order to share some data that requires strong consistency, a decentralized, strongly consistent data sharing method must be implemented.

This can be implemented via the data verification part of Xnode, the BFT-based proof-of-stake one. When the Xnodes need to achieve some kind of consensus, they can vote for it using the BFT algorithm, then add it to the blockchain. After that, the data will be immutable, and every node can retrieve the data.

This procedure complies with CP in the CAP theorem.

#### Resource Locating and Mapping Services

Architecture: **structured P2P**.

The whole network must be structured to help the virtualization layer locate resources accurately in the network. There must be a lookup table, like a distributed hash table, holding the structure and mapping of the resources throughout the whole network. To ensure the integrity and reliability of the virtualization layer, the resources must be backed up into replicas.

Though this part of the network is structured, it must be done in a decentralized way to maintain democratic control over the data.

#### Eventual Consistent Data Sharing Services

Architecture: **unstructured P2P**.

Thinking about the reliability of the system and the efficiency of data sharing, it’s not necessary to share all the data through the BFT protocol. Most of the data, like the membership management data and metadata, doesn’t need to be completely accurate and real-time. Their delay and intermediate inconsistency will not influence the functionality of the whole Xnode overlay network.

In order to share that data in a bandwidth-efficient way, eventually data sharing can be implemented via unstructured P2P protocols, like the Gossip protocol. This kind of data sharing is inaccurate, randomised, and unstructured, but it provides better performance and availability.

This complies with AP in the CAP theorem.

### Suggested Technology Stack

- **High Performance Programming Language:** C, C++ or Go
  - The Xnode virtual network heavily relies on distributed coordination and virtualization, which require high performance.
  - By using high performance programming languages:
  - The likelihood of bottlenecks will be inherently reduced.
  - The performance and resource consumption of Xnode on low-level hardware will also be highly optimised.
- **Structured P2P Coordination Protocol**: DHT and Rendezvous Hashing
  - DHT is the most commonly used technology for locating a resource in a structured P2P network. Successful use cases include BitTorrent, IPFS, and I2P.
  - Rendezvous hashing is one of the most commonly used DHT implementations. It’s an optimised version of consistent hashing. It’s much easier to understand and performs better in load balancing, capacity, and flexibility.
- **Unstructured P2P Coordination Protocol**: The Gossip Protocol
  - The Gossip protocol is one of the most commonly used unstructured P2P coordination protocols.
  - It has a lot of successful use cases, like Apache Cassandra, Redis Cluster, and Serf.
  - Gossip is high-performance and low-cost. A message can be shared throughout the whole network with N nodes in a time complexity of $O(logN)$.
- **BFT Implementation**: CometBFT
  - This is the BFT library that Xnode is currently using.
  - It’s sufficient for building the consensus part of the Xnode overlay network, so we can continue using it.

### Ideal Skills and Teams Required

- **Skills**
  - Software design (especially distributed system design).
  - Cloud infrastructure development (using the suggested technology stack).
  - Project management.

- **Teams**
- Software design: `1-2 Software Architects.
- Cloud infrastructure development: 3-4 Cloud Infrastructure Developers.

### Primary Goals

- Design an appropriate architecture for the Xnode overlay network.
- Take the whole Xnode overlay network apart into smaller components and design a detailed architecture for those components.
- Suggest the technology stack for implementing the Xnode overlay network.

### Success Criteria

- **Data Redundancy**: With no more than ⅓ nodes failing, the architecture should ensure the system is still functioning with no data loss, and the other nodes remain unaffected.
- **Handling Massive Data Transfer and Storage**: New data should be transferred to the target storage server determined by a resource locating service. The integrity of data will be guaranteed, with no possibility of data loss.
- **Virtualization Support**: The architecture provides a resource locating service or protocol, supporting the resource mapping and locating needs of the virtualization layer.
- **Data Verification**: The architecture provides a kind of verification service based on a failure-tolerant strongly consistent distributed coordination protocol.
- **Decentralized Data Sharing**: The system based on the architecture is decentralized. Every node in the network is equally privileged, with the node itself and the data stored in it governed by the community.

### Objectives

- **Confirm the services of the Xnode overlay network**.
  - Take the whole Xnode overlay network apart into small components or services.
  - Find out how they coordinate with each other.

- **Complete the architectural design of each service**.
  - Confirm the functionality and restrictions of each service.
  - Design an appropriate architecture for each service.

- **Confirm the suggested technologies used in development**.
  - Suggest an appropriate technology stack for implementing the Xnode overlay network.


## Resources and Research

### Alternative Solutions

#### Traditional Microservice Architecture

Traditional microservice architecture is a large-scale distributed architecture that takes a monolithic back-end web application apart into several small, lightweight, loose-coupled services. It’s getting more and more popular in back-end web development and is becoming one of the most popular distributed architectures in the world.

Compared with the P2P architecture of the Xnode overlay network:

- Strengths of traditional microservice architecture:
  - **Structured**. A typical system based on the traditional microservice architecture is highly structured, making it easy to locate the resources in the system.
  - **Data isolations**. A single microservice only has access to its own database. It will be much easier to update the schema and manage the data.

- Weaknesses of traditional microservice architecture:
  - **Highly rely on SDKs**. Though the services are loose-coupled, the business logic of the services is tightly-coupled with the SDKs that provide the runtime management of the whole system. There will be a likelihood of failures when the SDKs are updated and no longer compliant with the business logic.
  - **Non-Democratic**. Services and middleware are not equally privileged in a traditional-microservice based network because most of the services are highly dependent on the middleware, and the middleware has centralized control of the whole system. This breaks the decentralised and democratic design philosophy of Xnode.


In conclusion, though the traditional microservice architecture is not quite suitable for the Xnode overlay network, we can still apply some of its design philosophy to Xnode, like:

- Scalable
- Flexibility
- Data Isolation
- Fault Isolation

#### The Service Mesh Architecture

**Reference**: [What is Service Mesh?](https://aws.amazon.com/what-is/service-mesh)

The service mesh architecture is a highly optimized version of traditional microservice architecture and a popular solution to reduce the complexity of microservice development. Within a service mesh, every microservice will be attached to a process called sidecar, which intercepts all the traffic into or out of the service and forwards it to the service mesh, and the service mesh will provide support based on the traffic and the configuration. A single Xnode is really similar to a sidecar in the service mesh architecture that integrates multiple basic functionalities, performs as a cloud infrastructure, and provides support for the services based on it.

A typical service mesh consists of two parts: the data plane (all the sidecars and the services deployed to the service mesh) and the control plane (the centralized control services of the service mesh).

Compared with the P2P architecture of the Xnode overlay network:

- Strengths of service mesh:
  - **Transparency**. The service mesh is transparent to both the user and the microservices based on it. All the basic functionalities in microservices management are integrated within the service mesh, reducing the complexity of both the development and maintenance of microservices.
  - **Containerisation friendliness**. Most of the service meshes, like Istio and LinkeId, are based on Kubernetes. This means that the containerised services are easily integrated with the service mesh without making any changes to the service itself.

- Weaknesses of service mesh:
  - **Centralization**. The service mesh is naturally centralized because the data plane relies on the control plane to provide pivotal functionalities like service discovery, routing, and resource allocation. This makes the control plane a middleman between the services.
  - **Heavyweight**. The service mesh is one of the most heavyweight architectures in all the distributed architectures, causing a high delay in network traffic. The components and middleware within the service mesh will also consume huge amounts of resources, making it unpractical for low-end hardware.


#### Consistent Hashing

**Reference**: https://en.wikipedia.org/wiki/Consistent_hashing

Consistent hashing is another one of the implementations of DHT. The consistent hashing algorithm maps servers and data to a unique circle, then determines where to store the data based on the hash. It’s also a special case of rendezvous hashing.

- Strength of consistent hashing:
  - **Multiple successful user cases**. Consistent hashing is more widely used than rendezvous hashing, especially in Web2. Examples and implementations of consistent hashing are quite easy to find on the internet.

- Weaknesses of consistent hashing:
  - **Scalability**. The scalability of rendezvous hashing is better than that of consistent hashing, making it more suitable for large-scale global networks like the Xnode overlay network.
  - **Load Balancing**. Rendezvous hashing distributes objects uniformly across the whole network, ensuring true decentralization and reducing the likelihood of bottlenecks.


#### Two-Phase Commit Protocol (2PC)

**Reference**: https://en.wikipedia.org/wiki/Two-phase_commit_protocol

2PC is one of the most commonly used and most simple consensus algorithms in distributed systems. It’s quite similar to BFT: both of them consist of two stages: “voting” and “completion”. RSCoin is one of the successful implementations of 2PC, as it uses a customized version of 2PC.

Compared with BFT:

- Strengths of 2PC:
  - **Simplicity**. 2PC is one of the simplest consensus algorithms and is a lot simpler than BFT, making it easier to understand and implement.

- Weaknesses of 2PC:
  - **Reliability**. One of the most important assumptions that 2PC made is that all the nodes do not crash forever, as the coordinator needs to receive a reply from all the other nodes. However, this is not practical in the Xnode overlay network since it’s global, and the network connection is more likely to be unstable.


#### The Raft Consensus Algorithm

**Reference**: https://en.wikipedia.org/wiki/Raft_(algorithm)

Raft is another commonly used consensus algorithm and has some successful use cases, like Etcd, TiDB, ClickHouse, and MongoDB. Raft is an optimized version of 2PC, which means that it’s also strongly consistent and can be treated as an alternative to BFT.

**Compared with BFT**

- Strengths of Raft:
  - **Fault tolerance**. Raft allows more node failures than BFT, which means that the availability of systems based on Raft is better than that of systems based on BFT, especially when the network connection is unstable or the reliability of nodes is not guaranteed.
  - **Efficiency**. The voting progress of Raft is simpler than that of BFT, so the block time in systems based on Raft will be much faster than that of systems based on BFT.

- Weaknesses of Raft:
  - **Non-democratic**. BFT is democratic, but Raft is not. The leader of Raft is always assumed to be honest, making it impossible for followers to ask questions of the leader.
  - **Lack of usage in Web3**. Raft is more commonly used in Web2 and doesn’t have many successful use cases in Web3. This makes it harder to apply in Web3.


### Links to Research Papers

- **Distributed Architecture**
  - Microservices Definitions: [Microservices](https://martinfowler.com/articles/microservices.html)
  - P2P: [Peer-to-peer — Wikipedia](https://en.wikipedia.org/wiki/Peer-to-peer)

- **Distributed Hash Table (DHT)**
  - DHT: [Distributed hash table — Wikipedia](https://en.wikipedia.org/wiki/Distributed_hash_table)
  - CometBFT: [What is CometBFT — v0.38](https://docs.cometbft.com/v0.38/introduction)
  - Consistent Hashing: [Consistent hashing — Wikipedia](https://en.wikipedia.org/wiki/Consistent_hashing)
  - Redezvous Hashing: [Rendezvous hashing — Wikipedia](https://en.wikipedia.org/wiki/Rendezvous_hashing)

- **Proof-of-Stake (PoS)**
  - [Proof of stake — Wikipedia](https://en.wikipedia.org/wiki/Proof_of_stake)

- **Byzantine Fault Tolerance (BFT)**
  - BFT: [Byzantine fault — Wikipedia](https://en.wikipedia.org/wiki/Byzantine_fault)

- **Consensus Algorithm Comparison**
  - [Consensus Algorithms Compared: PoA vs IBFT vs Raft](https://www.kaleido.io/blockchain-blog/consensus-algorithms-poa-ibft-or-raft)
  - [A Taxonomy of Blockchain Consensus Methods](https://www.mdpi.com/2410-387X/4/4/32)


### Glossary

- **Xnode Overlay Network**: The whole virtualized network that all the Xnodes form, supporting the main functionality of the Openmesh network. It’s also the first layer of the global network that all the Xnodes form.

<img src="https://miro.medium.com/v2/resize:fit:3200/0*vgEoj9UdixHlo4Bb" alt="img" style="zoom:50%;" />

- **Microservices**: This word can refer to two similar concepts: 1. A kind of distributed architecture. 2. A lightweight service within that architecture. The precise meaning of this word depends on the context.
- **Resources**: Any data stored into Xnode network or anything needed by virtualization.
