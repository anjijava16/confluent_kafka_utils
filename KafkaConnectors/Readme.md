
# Kafka Connector 

	Sources ===> Kafka Connecot ===>> Kafka Brokers 

	Kafka Brokers ===>> Kafka Connector ===> Sinks 

{
"connector.class":"io.confluent.connector.jdbc.JDBCSourceConnector",
"connector.url":"jdbc:mysql://abc:3306/db",
"table.whitelist":"sales,orders,customers"

}

#Confluent Hub 
https://www.confluent.io/hub/



# Streaming PipeLines
   RDBMS ----> Kafka Connector --->> Kafka Brokers --->Kafka Connector ====> Amazon S3
   
# Streaming PipeLines write into S3 && HDFS 
      RDBMS ----> Kafka Connector --->> Kafka Brokers --->Kafka Connector ====> Amazon S3
                                                                                     --->Kafka Connector ====> HDFS 
																					 
# 

  Exsiting APP ---> RDBMS --->> Kafka Connect ---> Kafka Brokers ---> 
  
  http://rmoff.dev/kafka-connect-code
https://github.com/confluentinc/demo-scene/tree/master/kafka-connect-zero-to-hero
https://github.com/confluentinc/demo-scene/blob/master/kafka-connect-zero-to-hero/demo_zero-to-hero-with-kafka-connect.adoc


MYSQL > SELECT * FROM ORDERS BY CREATE_TS DES LIMIT 1\G
Open Source: io.debezium.connector.mysql.MySQLConnector 
$ curl -i -x PUT -H http://localhost:8083/connectors/source-debezium-orders-00/config -d '{

}'

# Source Connector 
io.debezium.connector.mysql.MySQLConnector 

# Elastic Seach Sink Connector 
 io.confluent.connect.elasticsearch.ElasticSearchSinkConnector 
 
 ## Check the status of Connector 
 $ curl -s "http://localhost:8083/connectors?expand =infoexpand=status"
 
#Putting into the neo4jSinkConnector 


Source ---> Native data ---> Kafka Connector(Connect Recrod ) ----> Kafka 


Kafka Connector ::
===================================
i. Serilazation && Schemas 
ii. Avro(Confluent && Schema Registry)
 Protobuf
 JSON 
 CSV 
 
 # The Confluent Schema Registry 
 Source ---> Kafka Connector ---Using Internally Avro Schema (Schema Registry Server) ===> Push Avro Message to ===> Kafka Server ===>
                          Consumer Side ===>>> Avro messages ===> Kafka Sink Connector(Connect to Schema Registry Server) ===> target Systems..

# Converters :
	key.converter=io.confluent.connector.avro.AvroConverter
	key.converters.schema.registry.url=http://localhost:8081
	
	value.converter=io.confluent.connector.avro.AvroConverter
	Value.converters.schema.registry.url=http://localhost:8081
 

# Connectors and tasks

JDBC Source                                   S3 Sink
   
# Worker 
   S3 Task #1
   JDBC Task #1                 JDBC Task #2    

# Kafka Connect Standalone worker 

Scaling the standalne

# kafka Connector Distributed Worker 
  S3 Task #1
  JDBC Task #1   JDBC Task #2
  Kafka Connector worker ==> Offset ,Config ,status 
  
 ## KafkaConnector Cluster #2

  JDBC Task #1,JDBC Task #2  ===>> Offset ,Config,Statussss 
  



