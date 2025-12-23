## Dt: 7th Dec 2025

## Apache Kafka

- Distributed event streaming platform.
- It is designed to handle high volums of real-time data streeams.
- It provides a pub/sub messaging system(publisher/subscriber)

---

## Integrations of two components:

The source system should not directly communication with destination system it is a wrong design.

---

## Problems:

1. For every new destination system, I have to modify the source systems where I have to add/remove destination system.
2. In case the data is not delivered, we have to retry the sending or we need to store the message some where.
3. Fault tolerant system(incase destination sytem is down, and comes back, the message is lost)

---

## Solution:

Introduce a messaging sytem called as brokers, so bascically we are building a decoupled architechture.  
Means the source system is unaware of the destination system.  
So the source and destination are independent.

---

## Components of Kafka:

1. Producer: Application through which we can send messages to the Kafka server.
2. Consumer: Application through which we can consume the messages.
3. Broker: It’s a node/indevidual machine - server
4. Kafka Clusters: Collecton of brokers - server group
5. Topic: Feed name/Channel
6. Partitions: Logical division of topics, decided based on volume of data- every broker stores one partition
7. Offset: Auto increment number maintained by Kafka- every message we deliver, a unique identifier is assigned starting from zero. This is used for message retrieval.
8. Consumer Groups: Group of consumer to reduce the load on a particular consumer  

   If one consumer reads the message, other consumer cant read it.  
   In actual scenario like production, Consumer group is alsways used instead of just consumer.

9. Zookeeper:
   - Co-ordinates with brokers
   - Choosing the leader partition
   - To ensure the brokers know eachother

---

From Beginning will not availablein consumer group.

---

## ISR: In Sync Replication

Which all nodes are intact/ in sync with the leader.

---

- Multiple producers can send the data to a single topic.
- It is not practically possible to store all data in a single topic with single broker, because it can go beyond the capacity of the boker.
- Here Kafka breaks the topic in to multiple partition.
- When this happens it is guranteed that each partition data is stored in individual broker.

  <img width="692" height="358" alt="image" src="https://github.com/user-attachments/assets/cdf598d0-a57d-4bfa-b1af-ded10ffe7cfb" />

  ## Types of Partition:

1. Sticky partition- It will ocupy the entire broker, once it is full it will go to the next partition.

2. Hash-based - Along with the message, we will give a key. It will calculate a hash value for K1.

   K1=21% no of partition


3. Custom Partition

---

## Steps to run Kafka:

1. Start Zookeeper
2. Start KAFKA server
3. Start Topic : eg: t01
4. Start Producer : eg: t01
5. Start Consumer : eg: t01

---

## Pluggin required for Pycharm:

- Batch script support

---

If I only started two kafka server(broker), but used partition=2 and replication 3, then we cant achieve the following:

Partition-0 → stored on Broker1, Broker2, Broker3
Partition-1 → stored on Broker1, Broker2, Broker3


Kafka tries to assign replicas but no brokers are available to hold the extra copies, so replicas stay unassigned.

---

## Topic Description Output

```cmd
C:\Users\sarada>kafka-topics.bat --describe --topic topic_03 --bootstrap-server localhost:9092

Topic: topic_03
TopicId: meiZiUogSPCSapHGSI1IBg
PartitionCount: 2

ReplicationFactor: 2
Configs:

Topic: topic_03 Partition: 0 Leader: 1 Replicas: 1,2 Isr: 1,2
Topic: topic_03 Partition: 1 Leader: 2 Replicas: 2,1 Isr: 2,1

Replication Factor Scenario

How Kafka handles the situation when you requested replication factor = 3, but only 2 brokers were available.

Kafka automatically reduced the replication factor to 2, because replication cannot exceed the number of broTopic: topic_03

PartitionCount: 2
ReplicationFactor: 2    ← expected 3 but set to 2

Partition: 0  Leader: 1  Replicas: 1,2  Isr: 1,2
Partition: 1  Leader: 2  Replicas: 2,1  Isr: 2,1

What this means:
Item	Interpretation
ReplicationFactor: 2	Kafka used only 2 copies since only 2 brokers exist
Leader	The broker responsible for handling reads/writes for this partition
Replicas	Copies of the partition across available brokers
ISR (In-Sync Replicas)	Replicas currently synchronized and active

Cluster

In Kafka, a cluster is a group of one or more Kafka brokers (servers) working together.

Cluster = multiple brokers running together to share workload, replicate data, and provide high availability.

🧠 Simple way to understand

Think of a cluster like a team, and brokers are team members.

Term	Meaning
Broker	A single Kafka server
Cluster	Collection/group of brokers

If one team member (broker) fails, the team (cluster) continues to work.
Cluster

In Kafka, a cluster is a group of one or more Kafka brokers (servers) working together.

Cluster = multiple brokers running together to share workload, replicate data, and provide high availability.

🧠 Simple way to understand

Think of a cluster like a team, and brokers are team members.

Term	Meaning
Broker	A single Kafka server
Cluster	Collection/group of brokers

If one team member (broker) fails, the team (cluster) continues to work.
All of these brokers together form one cluster.

Why do we need a cluster?
Benefit	Explanation
High availability	If one broker fails, another takes over
Load balancing	Topic partitions can be spread across brokers
Scalability	Add more brokers → more storage & processing power
Replication	Data can be stored/copied across brokers
set /p topic=Enter topic name?
kafka-topics.bat --describe --bootstrap-server localhost:9092 --topic %topic%



