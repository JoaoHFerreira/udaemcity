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
## Kafka Consumer Console Output Screenshot
![kafka_consumer_console_output](https://github.com/JoaoHFerreira/udaemcity/blob/master/udacity_data_streaming/sf_crime_data-project_files/kafka_consumer_console_output.png)
## Progress Reporter Screenshot
![progress_reporter](https://github.com/JoaoHFerreira/udaemcity/blob/master/udacity_data_streaming/sf_crime_data-project_files/progress_reporter.png)
## Spark Streaming UI
![spark_streaming_ui](https://github.com/JoaoHFerreira/udaemcity/blob/master/udacity_data_streaming/sf_crime_data-project_files/spark_streaming_ui.png)
## Q&A
### 1. How did changing values on the SparkSession property parameters affect the throughput and latency of the data?
Change parameters shou can be used in different use cases. Increasing the maxOffsetsPerTrigger for example, you will have a higher troughout at the same time will have higher latency. Each scenario will have a different approach.
### 2. What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?
Like every scenario, there' is no right anwser, one solution for each different problem. In a generic scendario where performance need but fault tolerance is alos, I would choose:
- 1.spark.streaming.kafka.maxRatePerPartition 
- 2.spark.streaming.receiver.writeAheadLog.enable
- 3.spark.streaming.kafka.maxRetries
- 4.spark.streaming.kafka.minRatePerPartition
Explaining the decision, 1 and 4 to guarantee a max and minimal troughput. 4 because some times crashs happens in a momentary way, this simple action would previne. 1 is similar to 4 reason, but additionally It prevents the streaming application of more several system failures