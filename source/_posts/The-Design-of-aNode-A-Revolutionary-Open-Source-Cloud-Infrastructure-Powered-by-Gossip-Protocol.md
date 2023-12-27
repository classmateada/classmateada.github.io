---
title: >-
  The Design of aNode: A Revolutionary Open-Source Cloud Infrastructure Powered
  by Gossip Protocol
lang: en
date: 2023-12-27 10:11:01
tags:
  - aNode
  - Software Architecture
categories:
  - aNode
---
## Introduction

aNode is initially a solution to challenge 3 of the OpenD/I Hackathon organised by Openmesh. The original requirements of this challenge are as follows (from the original OpenD/H Hackathon documentation):

1. Develop a solution that is able to receive data from multiple sources. It should be scalable to over 100 sources.

2. The solution should process this data in real-time. It should be saved to a database and transmitted to all listeners of a WebSocket.

3. A frontend should be present that gives insight into the current status of all components of your solution.

4. The solution should be able to support both REST API and WebSocket sources.

5. It should be easy to automatically deploy the solution. A containerized application (using for example docker) could be used or a setup script to handle installation could be provided.

Harnessing the power of the Gossip protocol, aNode redefines cloud infrastructure with its decentralised, resilient, and scalable architecture. It not only meets all the requirements above but also moves a step further: it's completely decentralised, P2P, and suitable for both Web2 applications and Web3 dApps.

## Understanding the Gossip Protocol

The Gossip protocol, often likened to the way rumors and gossips spread in social networks, is the basic of aNode. This protocol stands out for its robustness and simplicity in transmitting information across a cluster. Unlike traditional distributed consensus protocols that rely on centralised coordination systems (like Zookeeper and Etcd), the Gossip protocol operates on a more dynamic and decentralised principle, just like members of a community sharing news with their immediate neighbors.

At its core, the Gossip protocol involves nodes (i.e., aNode instances) periodically exchanging data with a randomly selected set of other nodes. This method ensures rapid and efficient transmission of data, which lets the information quickly reach all corners of the network. This approach offers several key advantages, particularly in cloud infrastructure:

1. **High Scalability**: As networks grow, the Gossip protocol naturally adapts, maintaining efficiency regardless of the size of the network. This makes aNode exceptionally scalable, an essential feature for modern cloud infrastructure.
2. **Fault Tolerance**: Unlike centralized systems, there is no single point of control or failure in decentralised systems based on the Gossip protocol. This network is also unstructured, which means the system is high availability and partition tolerance (comply with **AP** in the CAP theorem).
3. **Efficiency in Bandwidth Usage**: The protocol is cost-efficient, as it doesn’t require all nodes to communicate with a central server, reducing the likelihood of bottlenecks and enabling aNode to maintain high performance even under heavy load.
4. **Self-Healing and Maintenance**: The continuous exchange of information allows the network to constantly update and correct itself, ensuring that the system remains in a healthy state, which is crucial for cloud infrastructures that require high availability and reliability.

By integrating the Gossip protocol, aNode addresses key challenges in cloud infrastructure management, particularly in relation to the CAP theorem's constraints. This strategic choice enables aNode to offer a resilient, adaptable, and efficient cloud solution, making it an ideal candidate for handling the dynamic and often unpredictable nature of modern cloud computing environments.

## Features of aNode: Near Real-time Data Transfer

aNode, as an innovative open-source cloud infrastructure, shines in its key functionality - the ability to transfer data pushed to it through WebSockets to other nodes and all subscribers in near real-time. This is also the key requirement of challenge 3.

### Gossip Protocol for Decentralised Data Transfer

- **Rapid and Wide-Spread Data Distribution**: The Gossip protocol ensures that data received by any node is quickly propagated throughout the cluster. This decentralised approach allows for the rapid and efficient spread of information, ensuring all nodes in the network stay updated in near real-time. Typically, a new data is able to received by all nodes in a time complexity of $O(logN)$ (N is the number of nodes in the cluster).
- **Resilience and Reliability**: Leveraging the Gossip protocol, aNode is highly resilient to node failures or network issues. The protocol ensures that the system can continue to operate and transfer data even when some nodes are not functioning.

### Easy Setup and Easy Integration

- **Simple Setup and Configuration**: aNode is designed with user-friendliness in mind, offering straightforward setup and configuration processes via RESTful APIs, making it accessible to both beginners and experienced users. It's also containerised and can be easily set up using Docker without any setup fees.
- **Integration with Existing Systems**: Its compatibility and ease of integration with existing systems and technologies make aNode a good choice in a developer's perspective.

## How we Did It?

The implementation of aNode, is noteworthy for its integration of Apache Cassandra for database and the use of HashiCorp's `memberlist` library to implement the Gossip protocol. These choices play a pivotal role in ensuring aNode's efficiency, scalability, and reliability.

### Apache Cassandra for Database

1. **Scalable and Distributed Database**: Apache Cassandra is renowned for its exceptional scalability and distributed architecture. It perfectly aligns with aNode's need for P2P and decentralised architecture. Cassandra's ability to scale horizontally allows aNode to manage an increasing amount of data seamlessly.
2. **High Availability and Fault Tolerance**: Cassandra's decentralised model ensures high availability and fault tolerance, which are crucial for cloud infrastructures. This means that aNode can continue operating effectively even in the event of node failures, maintaining continuous service for its users.
3. **Efficient Data Storage and Retrieval**: Cassandra's data storage and retrieval mechanisms are optimized for high throughput and low latency, aligning with aNode's goal of near real-time data storage. Its efficient handling of large data sets ensures quick access and updates, enhancing the overall performance of aNode. The syntax of CQL is also similar to SQL, making it easy to learn and use.
4. **Eventual Consistency Model**: Consistent with the principles of the CAP theorem and comply with AP, Cassandra operates on an eventual consistency model. This approach complements the Gossip protocol used in aNode, ensuring that all data across the nodes eventually reaches a consistent state.

### Memberlist for Gossip Protocol Implementation

1. **Memberlist Library by HashiCorp**: The Gossip protocol in aNode is implemented using Golang and HashiCorp's memberlist library, a solution known for its efficiency and reliability in managing cluster membership and node failure detection. The famous distributed coordination system, Consul, is also based on this library.
2. **Dynamic Cluster Membership**: Memberlist facilitates dynamic handling of cluster membership, which is essential for aNode's decentralised environment. It allows nodes to join or leave the network seamlessly, ensuring the cloud infrastructure remains flexible and adaptable.
3. **Efficient and Reliable Node Communication**: The library provides an efficient mechanism for nodes to communicate and exchange information. This is critical for the rapid propagation of data in aNode, adhering to the real-time data transfer requirements.
4. **Failure Detection**: Memberlist includes robust failure detection. This feature enhances aNode's resilience, as it can quickly identify node failures, ensuring minimal impact on the network's performance.
5. **Lightweight and Scalable**: Memberlist is designed to be lightweight and scalable, complementing aNode's goal of being a scalable and efficient cloud infrastructure. Its low overhead and ability to handle large clusters make it an ideal choice for aNode's Gossip protocol implementation.

In conclusion, the integration of Apache Cassandra and the memberlist library is a strategic decision that significantly contributes to aNode's performance as a cloud infrastructure. Cassandra’s scalable and fault-tolerant database management capabilities, combined with Memberlist’s efficient and reliable implementation of the Gossip protocol, create a robust foundation for aNode. These basics not only enhances aNode’s capabilities in real-time data transfer and scalability but also ensures high availability and consistency across the decentralised network.

## Conclusion

In conclusion, aNode not only meets all the requirements of challenge 3, but also is forward-thinking in the realm of open-source cloud infrastructure. While this article has provided an overview of aNode's features and its unique implementation, the intricacies and technical depths of its design are worth further exploration. To delve deeper into the nuts and bolts of how aNode is implemented, I will write a subsequent article to provide a more detailed description of its implementation. This upcoming piece will discuss the technical layers of aNode, providing insights and in-depth analysis for those interested in the finer aspects of its innovative architecture and operational dynamics. Stay tuned for this deeper dive into the world of aNode, where technology meets practicality in the cloud computing landscape.

## Future Reading

- GitLab repository of aNode backend: [https://gitlab.com/cloud-captains-of-unsw/anode-back-end](https://gitlab.com/cloud-captains-of-unsw/anode-back-end).
- Try it out: [Installation Guide](https://gitlab.com/cloud-captains-of-unsw/anode-back-end/-/wikis/Try-aNode-Out:-Installation-Guide).
