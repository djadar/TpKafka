Name of my first topic : essai1
Name of first group : group1


# Part 1 : a single broker

1. What happens if the Kafka server crashes and needs to be restarted? Is it possible for clients
that connect after the server has restarted to retrieve the messages that were published before
the crash?

- Yes
Because of *Log* stored on disks, old records can be replayed.
When it wakes up, it starts by reading logs.

2. What happens if multiple consumers are registered to the same topic? When a message is
published, which consumer receives the messages?

- The both

3. What happens if multiple producers produce messages on the same topic? What is received
by the consumers?

- Yes

4. During the lecture on Kafka, we introduced the notion of consumer group. To associate a
consumer to a specific consumer group, the following comment should be used

**We need as many of partitions as number of clients to receive messages in the consumer group**

5. What happens on message publication when two consumers belonging to the same group
are registered to the same topic?

- It doesn't work.

6. What happens when new messages are published on this topic if 2 consumers belonging to
the same group are registered to this topic? 

- Then the 2 consumers receive the messages.
With 3 consumers, it doesn't work also.

**It is important to stop the Kafka broker first because **

rm -rf /tmp/zookeeper/* /tmp/kafka-logs/*

# Part 2 : a cluster of 3 broker

Explain the output of the command that describes the replicated topic

Topic: essai1	PartitionCount: 1	ReplicationFactor: 3	Configs: segment.bytes=1073741824
	Topic: essai1	Partition: 0	Leader: 2	Replicas: 2,3,1	Isr: 2,3,1



• Can a producer connect to any broker to publish a message on the topic? (To change the
broker to connect to, simply change the port number in the url of the -bootstrap-server
option)


• Create 3 consumers, each connected to a different broker. What happens when a message is
published on the topic?

- The message is received by the consumers

• Kill the broker that plays the role of leader for the replicated topic.
– Can we still publish and consume messages on the topic?

- We can publish but we cannot consume

– Observe the new state of the replicated topic and explain what happened.

- the broker 3 is elacted as leader.


• Restart the killed broker and observe the state of the replicated topic. Explain.

- The leader is still 3 and 2 appears in the list.

• Create a new topic with a replication degree of 3 and 2 partitions. Register 3 clients belonging
to the same consumer group to this topic.
– Observe the state of the new replicated topic and explain the difference with the previ-
ous case.
– What happens when a producer publishes messages on the topic?