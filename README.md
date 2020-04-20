#Confluent Kafka Setup 

# Default Port 

#	Component	Port
 i.	    Apache Kafka brokers (plain text)	9092
 
 ii.	Confluent Control Center	9021
         http://localhost:9021/clusters/
 
 iii.	Kafka Connect REST API	8083
          http://localhost:8082/
		  
 iv.	REST Proxy	8082
	   http://localhost:8082/
 
 v.	Schema Registry REST API	8081
	    http://localhost:8081/
 
 vi.	ZooKeeper	2181
 
 vii.	ksql-server :8088
	    http://localhost:8088/info


#Down load Confluent Kafka 
   https://www.confluent.io/download/
   https://github.com/anjijava16/confluent-windows-5.0.1.git
   
   
# Confulent Control Center 

http://localhost:9021/clusters/
https://github.com/confluentinc/examples




# Production Environment

Start each Confluent Platform service in its own terminal:

# Start ZooKeeper.  Run this command in its own terminal.
$ <path-to-confluent>/bin/zookeeper-server-start <path-to-confluent>/etc/kafka/zookeeper.properties
# Start Kafka.  Run this command in its own terminal.
$ <path-to-confluent>/bin/kafka-server-start <path-to-confluent>/etc/kafka/server.properties
# Start Schema Registry. Run this command in its own terminal.
$ <path-to-confluent>/bin/schema-registry-start \
<path-to-confluent>/etc/schema-registry/schema-registry.properties
# Start Connect in distributed mode. Run this command in its own terminal.
$ <path-to-confluent>/bin/connect-distributed \
<path-to-confluent>/etc/schema-registry/connect-avro-distributed.properties	

# Development Environement

Run this command to start all Confluent Platform services by using the CLI.

$ <path-to-confluent>/bin/confluent start

# Set the gedit ~/.bashrc

export CONFLUENT_HOME=/home/welcome/work_inst/confluent-5.4.1-2.12/confluent-5.4.1
export PATH="${CONFLUENT_HOME}/bin:$PATH"


# How to start Local mode 
	confluent local start
	
Starting zookeeper
zookeeper is [UP]
Starting kafka
kafka is [UP]
Starting schema-registry
schema-registry is [UP]
Starting kafka-rest
kafka-rest is [UP]
Starting connect
connect is [UP]
Starting ksql-server
ksql-server is [UP]

# Login Below Location 

cd /home/welcome/work_inst/confluent-5.4.1-2.12/confluent-5.4.1


# Input Sources 
   Files,Database ,Real time data 
   
# Producer : 
		  Kafak Producer 
		 Kafka Connect Source


# kafka
		 Kafka Streams 
		 KSQL 
 
# Consumer 
		Kafka Consumer 
		Kafka COnnect Sink

#Target 
	Target Database  
	 Target System (NOSQL,Any FIle System) 
 



# Create Topic as users 
./bin/kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic users	

# Create one more topic :
  ./bin/kafka-topics --create --bootstrap-server localhost:9092  --replication-factor 1 --partitions 1 --topic pageviews
  
# List of Topics :
   ./bin/kafka-topics --list --bootstrap-server localhost:9092
   
#  Install a Kafka Connector and Generate Sample Data
wget https://github.com/confluentinc/kafka-connect-datagen/raw/master/config/connector_pageviews_cos.config 
curl -X POST -H "Content-Type: application/json" --data @connector_pageviews_cos.config http://localhost:8083/connectors   


wget https://github.com/confluentinc/kafka-connect-datagen/raw/master/config/connector_users_cos.config
curl -X POST -H "Content-Type: application/json" --data @connector_users_cos.config http://localhost:8083/connectors

#Create Streams and Tables
Start the KSQL CLI in your terminal with this command.

LOG_DIR=./ksql_logs ./bin/ksql

https://docs.confluent.io/current/quickstart/ce-quickstart.html
https://docs.confluent.io/current/quickstart/cos-quickstart.html



welcome@welcome-Inspiron-5558:~/work_inst/confluent-5.4.1-2.12/confluent-5.4.1$ LOG_DIR=./ksql_logs ./bin/ksql
                  
                  ===========================================
                  =        _  __ _____  ____  _             =
                  =       | |/ // ____|/ __ \| |            =
                  =       | ' /| (___ | |  | | |            =
                  =       |  <  \___ \| |  | | |            =
                  =       | . \ ____) | |__| | |____        =
                  =       |_|\_\_____/ \___\_\______|       =
                  =                                         =
                  =  Streaming SQL Engine for Apache Kafka® =
                  ===========================================

Copyright 2017-2019 Confluent Inc.

CLI v5.4.1, Server v5.4.1 located at http://localhost:8088

Having trouble? Type 'help' (case-insensitive) for a rundown of how things work!

ksql> 




#Create a stream pageviews from the Kafka topic pageviews, specifying the value_format of AVRO.

CREATE STREAM pageviews (viewtime BIGINT, userid VARCHAR, pageid VARCHAR) WITH (KAFKA_TOPIC='pageviews', VALUE_FORMAT='AVRO');

#show streams
  show streams;
CREATE TABLE users (registertime BIGINT, gender VARCHAR, regionid VARCHAR,  userid VARCHAR) WITH (KAFKA_TOPIC='users', VALUE_FORMAT='AVRO', KEY = 'userid');


https://github.com/kaiwaehner/ksql-fork-with-deep-learning-function/blob/master/ksql-clickstream-demo/demo/clickstream-schema.sql


RUN SCRIPT '/home/welcome/work_inst/confluent-5.4.1-2.12/confluent-5.4.1/demo/clickstream-schema.sql'


# show tables;
   show tables;
   
ksql> SET 'auto.offset.reset'='earliest';


# Data Generation by Default have in KSQL-datagen 
# KSQL-datagen
./bin/ksql-datagen quickstart=clickstream format=json topic=clickstream maxInterval=100 iterations=50000

# By default KSQL-datagen below events info using above CLI Command 
    [CLICKSTREAM_CODES, CLICKSTREAM, CLICKSTREAM_USERS, ORDERS, RATINGS, USERS, USERS_, PAGEVIEWS] (case-insensitive)


welcome@welcome-Inspiron-5558:~/work_inst/confluent-5.4.1-2.12/confluent-5.4.1$ ./bin/ksql-datagen  quickstart =clickstream format=json topic =clickstream maxInterval=100 iterations=50000
Invalid argument format in 'quickstart'; expected <name>=<value>
usage: DataGen 
[help] 
[bootstrap-server=<kafka bootstrap server(s)> (defaults to localhost:9092)] 
[quickstart=<quickstart preset> (case-insensitive; one of 'orders', 'users', or 'pageviews')] 
schema=<avro schema file> 
[schemaRegistryUrl=<url for Confluent Schema Registry> (defaults to http://localhost:8081)] 
key-format=<message key format> (case-insensitive; one of 'avro', 'json', 'kafka' or 'delimited') 
value-format=<message value format> (case-insensitive; one of 'avro', 'json' or 'delimited') 
topic=<kafka topic name> 
key=<name of key column> 
[iterations=<number of rows> (if no value is specified, datagen will produce indefinitely)] 
[maxInterval=<Max time in ms between rows> (defaults to 500)] 
[propertiesFile=<file specifying Kafka client properties>] 
[nThreads=<number of producer threads to start>] 
[msgRate=<rate to produce in msgs/second>] 
[printRows=<true|false>]

welcome@welcome-Inspiron-5558:~/work_inst/confluent-5.4.1-2.12/confluent-5.4.1$ ./bin/ksql-datagen quickstart=clickstream format=json topic=clickstream maxInterval=100 iterations=50000

./bin/ksql-datagen quickstart=clickstream format=json topic=clickstream maxInterval=100 iterations=50000


./bin/kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic clickstream
	
./bin/ksql-datagen -daemon quickstart =clickstream format=json topic =clickstream maxInterval=100 iterations=50000
CREATE STREAm clickstream(_time BIGINT, time VARCHAR ,ip VARCHAR , request VARCHAR , status INT,userid INT ,bytes BIGINT ,agent VARCHAR) WITH (KAFKA_TOPIC='clickstream',VALUE_FORMAT='JSON')

SELECT * FROM clisteam emit CHNAGS;
select * from CLICKSTREAM EMIT CHANGES limit 10;

./bin/kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic clickstream_codes

./bin/ksql-datagen quickstart=clickstream_codes format=json topic=clickstream_codes maxInterval=100 iterations=10

# Select Stream 
SELECT * from CLICKSTREAM_CODES EMIT CHANGES;


./bin/kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic web_users
./bin/ksql-datagen quickstart=web_users format=json topic=web_users maxInterval=100 iterations=10

# Show commands 
show streams; list streams ;

show tables; or list tables ;

show queries ;
show properties 

# Terminates Queries
  terminate query_id 

# Print Streams (OR) tables 
print clickstream;

# describe stream
  describe clickstream 
  describe extended clickstream 
# Drop streams or tables   
  drop stream clickstream 
  drop table clickstream 
  
  
  
#Stream vs Table 
   # Stream 
     A Steam is an unbounded sequence of events : Immutable 
	   It is similar to Under Kafka Topic data 
	   
	   KStream ==>> List / Stream ===> KSQL (Stream) ===>> List / Stream[(K,V)] : Python []
  # Table 	 
	 A Table is a materilazied view of events with only the latest value for each key.
	 It is latest account balance ,per user that evolves with each transaction .
	 Table :===> KTable ==> Table ===> HashMap ===> mutable.map[K,V] {}
	 
	 
		Stream : Current and Full history  : commit history  (git log)
		Table : current info  : repo at commit (git checkout <<commit >> )


create stream user_clickstream as select userid,u.username,ip,	



 Topic is a stream of continuous data ,never ending data 
 
 
 
 
 ##  Kafka is not a 
     Storage solution
	 
## Real time usecase 	 
Sensor data 	 tempatature 
0.0.30.c 
 
 # Kafka Streams (KSQL)
 Stream processing Solution 
 
  Kafka Streams is a clinet Libray for building applications and microservices 
  where input and output data stored in apache kafka cluster .
  
  Streamsing SQL Engine for kafka 
  Provide interactive SQL interface
  Scalable ,elastic,fault-tolerant and real time
  Supports wide range of streaming operations:
    data filtering
	transformation
	aggregations
	joins
	windowing
	sessionzation
	KSQL Engine 
	KSQL CLI
	KSQL REST intrface(hostname:8088)
	
	

KSQL : SQL Interface Kafka Streams 

   Interactive MODE : CLI or REST mode 
   Headless Mode (Execute file) Idle for Production envormnet 
   
   KSQL Engine 
   REST Interface
   
   KSQL client UI/CLI 
      
	
	
	UI (KSQL Client ) ---> KSQL engine or KSQL REST ---> Kafka Server 
	


# Kafka Connect :

 Application1  --->> Database --->>> Copy to SnowFlake DB 

DataSource ===> Kafka Connect ===> Kafka Cluster ===>> Kafka Connector --->> SnowFlakeDB 
	                        Source Connector                                     Sink Connector 
							
SourceConnector :
  RDBMS Databaases
  Teradatabase
  IOT hubs
  SalesSource
  Twitter
  Reddit
  
  
Kafka Connector Framework:
   i. Source Connector :
                i. Source Connector 
				ii. SourceTask 
   ii. Sink Connector 
                 i. Sink Connector 
				 ii. Sink Task 
				 
RDMBS : To Kafka 
Predefined : Kafka Connector JDBC Source Connector 

DB ---> KafkaConnector (JDBC Connector) ====> Kafka Cluster ===> KafkaConnector(SnowFlakeConnector) ===> SnowFlake   
Kafka Connector Arch:
    i. Worker 
	ii. Connector 
	iii. Task 
	
   Fault Tolerant 
   Self Managed 


Reliability
High Avaiablity    




# Kafka Streams 

Sensors
Log Entries
ClickStreams
Transactions
Data Feeds


It is Java /Scala Libary
Input Data mus be Kafka Topic
You can embed kafka Streams in yours microservices
Deploy anywhere (No Cluster needed)
Out of box parallel processing,scalability and fault tolerane...


