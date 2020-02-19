# SF Crime Statistics with Spark Streaming Project
## Requirements
Before you start this project you will need the following requires:
- Spark 2.4.3
- Scala 2.11.x
- Java 1.8.x
- Kafka build with Scala 2.11.x
- Python 3.6.x or 3.7.x
## Hands On
#### After all stacks installed and configured you will follow the steps below:
1. Run `bin/zookeeper-server-start.sh config/zookeeper.properties` in one tab terminal and `bin/kafka-server-start.sh config/server.properties` in other;
2. Run `python kafka_server.py`
3. Run `bin/kafka-console-consumer.sh --bootstrap-server localhost:<your-port-number> --topic <your-topic-name> --from-beginning`

The first command will start the zookeper and kafka servers, the second one will be responsible for insert data into topic and the last (but not least), will be the consumer.

### After all these steps, we can now run the spark-job itself with the following command:
```
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py
```
