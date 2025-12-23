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
   
   21%3=0


4. Custom Partition

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

Visual Representation
Kafka Cluster
 ├── Broker 1 (server.id=1)
 ├── Broker 2 (server.id=2)
 └── Broker 3 (server.id=3)
All of these brokers together form one cluster.

Why do we need a cluster?
Benefit	Explanation
High availability	If one broker fails, another takes over
Load balancing	Topic partitions can be spread across brokers
Scalability	Add more brokers → more storage & processing power
Replication	Data can be stored/copied across brokers
set /p topic=Enter topic name?
kafka-topics.bat --describe --bootstrap-server localhost:9092 --topic %topic%

#Dt: 8th Dec 2025

<img width="692" height="306" alt="image" src="https://github.com/user-attachments/assets/16769fc1-e756-4ef6-945a-efce12769a4a" />

21 and 22 are hash numbers decided by Kafka

---

## Sticky Partition:

It will fill the entire offset and then it will choose other Partition.

---

## We have four APIS in Kafka:

1. Producer API- Java/python
2. Consumer API- Java/python
3. Kafka stream- Java
4. Connect API- Java

---

## Admin API:

Through this we can create topic

---

## Port Number:

Based on port number- number of nodes are decided

---

Where can I check I have three node kafka cluster.
#Consumer Group:
<img width="692" height="312" alt="image" src="https://github.com/user-attachments/assets/652e3a21-071d-4c25-afe1-d96a065cbe01" />

Topic is broken down in to partitions and replicas.

---

## Dt: 10th Dec 2025

## Message Sending Patterns / Strategies

Approach how producer sends message to topic:

1. Fire and Forget  
2. Synchronous Send  
3. Asynchronous send with call back  

---

## 1. Fire and Forget:

The producer sends a message and doesnot wait for any acknowlegement.

### Pros:

- It is one of the fastest way of sending data
- Low latency

### Cons:

- Don’t know the message delivery
- Not reliable for transactional data(super critical data)

---

## 2. Synchronous Send: (wait for the ack)

The producer sends a message and it waits for the broker to respond that a message has been delivered or not.

### Pros:

- Message delivery status

### Cons:

- Slower
- Blocks the next request

---

## 3. Asynch

Doesnot have to wait for the response, the response will appear on is own time, but it will not block the next send.

---

## Dt: 11Dec 2025

## API’s of Kafka

1. Producer API
2. Consumer API
3. Stream API
4. Connect API

Offset:

<img width="408" height="174" alt="image" src="https://github.com/user-attachments/assets/5f022f03-ecfe-4be1-b9e7-d8caafba3dd4" />

<img width="692" height="332" alt="image" src="https://github.com/user-attachments/assets/92e7c81f-9ebd-4eb1-ad9a-391f0f94de58" />

## Partitioning Mechanism

1. Sticky Partitions / Round Robin  
2. Hash partition / Key partition (partition no=hash_value%no of partiotion)  
3. Custom Partitioning  

---

```python
From confluent_kafka import producer
Producer = producer()
Producer.send(topic=, value=, partiion=)

If no key is sent, it goes with sticky partition / any partiono.

Load Balancing and Rebalancing:
Consumer Group A:

When there is a consumer group, a message sent to a consumergroup with a KEY is registered there, so next time any message sent with a KEY will always goes to the same consumer group.

In the same scenario, if the group is stopped, it the group will load balance and assign the KEY to some other Consumer Group.

If the Consumer Group Comes Back, entire rebalaning will happen. Existing keys will be reassigned to any partition.

Incase there is no consumer group available and a message is sent, there will be a LAG.

This will go away when a new consumer group is started.

Before Reset:

<img width="692" height="107" alt="image" src="https://github.com/user-attachments/assets/c2d81200-770a-453a-93ff-827ea9e5194a" />


After Reset:
<img width="693" height="86" alt="image" src="https://github.com/user-attachments/assets/e1afbe56-1d1e-4fd0-8ad6-447382489a97" />
After reset, it will reset the offset and start reading from zero.

---

## 15Dec 2025

## APIs of Apache Kafka

1. Producer APIs
2. Consumer APIs
3. Kafka Connect APIs
4. Kafka Stream APIs

---

## Kafka Connect APIs

### Data Integration Framework:

It is part of Kafka Eco system, that is moving data from in and out of Apachi Kafka without writing any code. If at all I have a business requirement

<img width="693" height="334" alt="image" src="https://github.com/user-attachments/assets/55f048b2-efe1-4dcd-a77b-4c9cfdb287e6" />
## Kafka souce connector (inbound)

1. We need Kafka souce connector: bringing data in to Kafka pulling data from different source and publishing data to Kafka.
2. It internally use Kafka producer
3. Uses some config
4. Topic creation also not required

---

## Kafka Sink Connector (Outbound):

1. Bring data to out of Kafka
2.

---

## Why Kafka Connect Exists:

- It provieds lot of pre-build connectors (JDBC, S3, Elastic, Search, Big Query)
- Configuration based pipelines
- Fault toloerance and scalling
- Standalone and distributed modes
<img width="692" height="207" alt="image" src="https://github.com/user-attachments/assets/d1907fee-22bb-42c1-a40c-98bd6d4f10e9" />
Kafka Connet Arcitechture

<img width="692" height="213" alt="image" src="https://github.com/user-attachments/assets/df3acd3c-5bed-4cc7-85de-eaf112749b54" />

## Kafka Connect Cluster:

All the workers in this cluster are nodes responsible for executing

---

## Kafka Stream API

It process coninuous data and write data into Kafka.

---

## Standalone vs Distributed Mode:

### Standalone Mode:

- Single kafka Connect Worker
- Runs as one JVM process
- All connectors and tasks run in that one process

---

### Distributed Mode

- Multiple Kafka Connect workers
- Forms a connect Cluster
- Tasks are distributed automatically

---

## Incremental Data Injestion from MySQL to Kafka using Kafka Connect API

<img width="546" height="234" alt="image" src="https://github.com/user-attachments/assets/53122969-c380-41d3-a364-7dce40b61603" />
Any data/record that gets inserted into the table, the JDBC Source Connector reads the event and pushes into kafka.

---

When we are going to define any connector SOURCE or SYNCH, we need Worker.Properties.

And then we need either SOURCE.Properties or SYNCH.Properties.

---

## Worker.Properties

We have to define the Kafka brokers

```properties
bootstrap.servers=localhost:9092

Converter--> How data is serialised or deserialised

key.converter=org.apache.kafka.connect.json.JsonConverter
value.converter=org.apache.kafka.connect.json.JsonConverter

Disable custom schema- no need to use any schema

key.converter.schemas.enable=false
value.converter.schemas.enable=false

Define the offset storage:
offset.storage.file.filename=C:/data-engineering-env-setup/kafka/logs/connect.offset


We need some pluggins to connect to mySql:

plugin.path=C:/data-engineering-env-setup/kafka/connectors/jdbc-connectors
listeners=localhost:8084

Source.Properties
name=mysql-source-connector

JDBC source connector
connector.class=io.confluent.connect.jdbc.JdbcSourceConnector

Maximum one single worker
tasks.max=1

Database location
connection.url=jdbc:mysql://localhost:3306/retaildb?useSSL=false&serverTimezone=UTC

Database credential

connection.user=root
connection.passsword=mysql


Connect driver

connect.driver.class=com.mysql.cj.jdbc.Drivers


Whitelist db

table.whitelist=retaildb.employees


Topic prefix:

Mysql-


Poll interval

poll.interval.ms=5000


NB: For different databases we only need to change the DB connection and connect driver
My Sql Commands:
\sql

CREATE DATABASE companydb;
USE companydb;

CREATE TABLE `employees` (
  `emp_id` int,
  `name` varchar(100),
  `department` varchar(50),
  `salary` int DEFAULT NULL,
  PRIMARY KEY (`emp_id`)
);

#Dt: 16Dec 2025
**Data Contract:
**

Consumer is indirectly couple with the dataformat with producer.

<img width="692" height="232" alt="image" src="https://github.com/user-attachments/assets/82618c03-8f18-4068-966c-0d9aa5c221c2" />

Serialization and Desereialisation:
Process of converting objects into bytes, deserialization is the reverse of it.
Deserialisation is restore the original state.

<img width="692" height="164" alt="image" src="https://github.com/user-attachments/assets/107b68a7-6ff4-40ab-9597-41415bb6224b" />
Class Employee
{
Private string fName,
Private string lname
}

String message=’Message01’
Producer.send(message)->simple data like string
But for custom objects we need to serialize and deserialize.
**Dt: 17 dec 2025**

<img width="692" height="333" alt="image" src="https://github.com/user-attachments/assets/d58e3dea-28a3-408c-b96e-047c9d96bd22" />

Components:
1.Source
2.Streaming Framework
3.Sink

<img width="692" height="288" alt="image" src="https://github.com/user-attachments/assets/b28fa1e7-e97f-439e-b22e-5a232f9f0b3b" />
Distributed streaming platform
Apache Sparc:
- The most widely used Bigdata framework used is Sparc.
- This is used to read continuously.
from pyspark.sql import SparkSession
from pyspark.sql.functions import col
from pyspark.sql.types import StringType

KafkaAvroSerializer 
In a Kafka-based system, a producer can use KafkaAvroSerializer to serialize messages and register schemas automatically. A consumer can use KafkaAvroDeserializer to deserialize messages, ensuring compatibility with the producer's schema. This setup allows seamless schema evolution without breaking the producer-consumer contract.
By combining Avro with Schema Registry, organizations can achieve efficient, scalable, and reliable data serialization while managing schema evolution effectively.
Dt: 18 Dec 2025
Put the file: docker-compose.yml
Run this:
>docker compose up
Landoop Kafka Development environment
Validate: http://localhost:3030/



 Serialization Formats:
1.Binary Serialiation Format
a)AVRO
b)ProtocolBuf
c)Thrift
2.Plaintext Serialization Format
a)JSON
b)XML
BINARY Serialization	PLAINTEXT Serialization
This serializes the data to  byte array	This serializaes the data to encoded text
Not human readable	Human readable
This is more efficient because the data is compact and less memory overhead	Data is versose
Serialization is faster	Serialization is slower
What is Avro
It is a data serialization fystem and it helps to exchange data between two systems (Producer and Consumer) using Binary Serialization Format
Why AVRO over other format
AVRO schema can be defined in JSON
Support for Interface definition language
Data owner defines a schema in JSON format

<img width="692" height="200" alt="image" src="https://github.com/user-attachments/assets/f4e2fe52-6131-4e44-bc6b-b0055998dd42" />

AVRO Data Structures
1.Primitive data types (string, bytes, int, long, null)
2.Complex Types
a)Enum
b)Arrays
c)Maps
d)Record
e)union
What is schema Registry
Store and retrieve schemas for producer and consumer
Problems without Schema Registry
ISSUE	REALITY
Schema Validation	None
Compatibility Check	
Runtime Safety	
Ownership of schema	
Dt: 22nd Dec 2025
KAFKA Streams:
File Format:
1.Row oriented format - 
2.Column oriented file format
Column: To retrieve this , it will directly go to the data locaation
Row Oriented:To retrieve this , we have to parse entire row
Solutions: (for column) -> lakehouse architecture
1.Parquet:
2.Lake house architectture: combination of best features of datalake and data warehouse
Datalake; - semi structured, strurctured,
Open Table Format;
-> Apache Hoodie
-> Apache Iceberg
-> Delta Lake/table (Databricks).


<img width="692" height="290" alt="image" src="https://github.com/user-attachments/assets/ef9b833c-07a9-4d14-af9e-865f97c54afa" />

<img width="692" height="256" alt="image" src="https://github.com/user-attachments/assets/c73a0ae8-74f3-4350-9511-5b1393eedfc4" />

Fault Tolerance: check pointing

<img width="692" height="341" alt="image" src="https://github.com/user-attachments/assets/d5015e65-c809-41b5-ae80-1ac706c34e23" />
Common Issues;
Tuning Configurations: (Throughput and low latency)
Replication
Log Compaction
OS Level
Optimize 
Throughput - number of messages Kafka can process per second.
Latency- Time taken foe a message from Producer to consumer and again back
Batch Size: How many messages we have to send in batch - e.g 10kb
Brocker side Tuning
1.Num.network.threads
2.Num.IO.thread
Log Compaction:

<img width="692" height="143" alt="image" src="https://github.com/user-attachments/assets/deef1eb5-1ea3-47d5-932c-0555bc7115b0" />
At any point o f time keep the latest value of each key.
To have the latest transaction- cluster level
Choosing the right partition: (chooseing partition count)
Helps us achieve
1.Parallelism
2.Scalability
3.Consumer Concurrancy
It’s a trade off between our requirement and resource for an iedeal scenario
1.50% disk space
2.Good SSD
3.OS level- thread??
Broker Balancing, Consumer LAG, Monitoring(offset exploring)
Auto Commit Offset=true

<img width="692" height="291" alt="image" src="https://github.com/user-attachments/assets/689cfa63-a90d-48b1-af06-e47bc659b894" />

Kafka Streaming:
- Functional Interface
- Kafka Streams API

<img width="692" height="233" alt="image" src="https://github.com/user-attachments/assets/dd19bcb5-bc27-44a0-97c9-d9fc21fe7f77" />
Streams API Implementation
1.Streams DSL(High level API)
2.Processor API (Low level API)
Kafka Streams Terminologies
1.Source Processor
2.Stream Processor
3.Sinc Processor

<img width="345" height="262" alt="image" src="https://github.com/user-attachments/assets/543abd77-f6cd-4666-8118-b5c33a615bf7" />
Kafka Security:
Four Layers:
1.Encryption 
2.Authentication
3.Authorization
4.Application Security
1.Encryption :
Advantage: secure delivery
Disadvantage: speed
2.Authentication-SASL/PLAIN
Kerberos
3.Authorization:
Permissions
Who is allowed to write
4.Application Security:
SSL
                              THE END
