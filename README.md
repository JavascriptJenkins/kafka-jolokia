# kafka-jolokia



<b>How to get into a docker container:</b><br>

    `docker exec -it 4f7453a4d1c  bash`


<b>Run Docker zookeeper image:</b><br>

` docker run -e ZOOKEEPER_CLIENT_PORT=2181 -e ZOOKEEPER_TICK_TIME=2000 -e ALLOW_ANONYMOUSE_LOGIN=yes -p 2181 javascriptjenkins/red-zookeeper
`
<br>

<b>Run Docker kafka image:</b><br>

`docker run -e KAFKA_ADVERTISED_HOST_NAME=localhost -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 -e KAFKA_ZOOKEEPER_CONNECT=172.17.0.2:2181 javascriptjenkins/kafka-jolokia 
`

<b>How to use Jolokia:</b><br>



`http://localhost:8080/jolokia/read/kafka.server:type=BrokerTopicMetrics
 
 https://github.com/DataDog/the-monitor/blob/master/kafka/monitoring-kafka-performance-metrics.md#broker-metrics
 http://grokbase.com/t/kafka/users/164ksnhff0/enable-jmx-on-kafka-brokers
 
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::SAMPLE REQUESTS FOR KAFKA M-BEAN METRICS::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 http://kafka-jolokia-jmx-kafka-project-1.b9ad.pro-us-east-1.openshiftapps.com/jolokia/read/kafka.server:type=ReplicaManager,name=UnderReplicatedPartitions
 
 http://kafka-jolokia-jmx-kafka-project-1.b9ad.pro-us-east-1.openshiftapps.com/jolokia/read/kafka.controller:type=KafkaController,name=ActiveControllerCount
 
 http://kafka-jolokia-jmx-kafka-project-1.b9ad.pro-us-east-1.openshiftapps.com/jolokia/read/
 kafka.controller:type=KafkaController,name=OfflinePartitionsCount
 
 
 
 
 http://kafka-jolokia-jmx-kafka-project-1.b9ad.pro-us-east-1.openshiftapps.com/jolokia/read/java.lang:type=GarbageCollector,name=ParNew	
 
 
 
 
 https://github.com/DataDog/the-monitor/blob/master/kafka/monitoring-kafka-performance-metrics.md#broker-metrics
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
 ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
`
------------------------------------------------------------------------------------------------------------------------
To calculate broker usage - add up all the data that will be written accross kafka.  divide that number by 
the number of days before the data expires.
40GB * 5 = 200GB --- expires @ 80GB/day, will stay right @200GB max if same load is maintained
------------------------------------------------------------------------------------------------------------------------





create topic (run these commands on kafka broker in container shell):

kafka-topics --create --topic peter --partitions 1 --replication-factor 1 --if-not-exists --zookeeper 172.17.0.3:2181

kafka-topics --describe --topic peter --zookeeper 172.17.0.3:2181

bash -c "seq 42 | kafka-console-producer --request-required-acks 1 --broker-list localhost:9092 --topic peter && echo 'Produced 42 messages.'"


kafka-console-consumer --bootstrap-server localhost:9092 --topic peter --from-beginning --max-messages 42


kafka-topics --zookeeper 172.17.0.3:2181 --list

kafka-topics --zookeeper 172.17.0.3:2181 --delete --topic peter

---- actual commands, not confluents version
./bin/kafka-topics.sh --zookeeper localhost:2181 --list

./bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic remove-me



