Prerequisites::
------------------------------
	Docker
	Docker version 1.11 or later is installed and running.
	Docker Compose is installed. Docker Compose is installed by default with Docker for Mac.
	Docker memory is allocated minimally at 8 GB. When using Docker Desktop for Mac, the default Docker memory allocation is 2 GB. You can change the default allocation to 8 GB in Docker. Navigate to Preferences > Resources > Advanced.
	Git
	Internet connectivity
	Operating System currently supported by Confluent Platform
	Networking and Kafka on Docker
	Step 1: Download and Start Confluent Platform Using Docker
	Clone the confluentinc/cp-all-in-one GitHub repository.

** Goto below docker compose location path :
----------------------------------
cd C:\Tech_Learn_welcome\Kubernates\confluent_kafka\cp-all-in-one\cp-all-in-one

** Check out the 6.0.1-post branch:

	cd cp-all-in-one
	git checkout 6.0.1-post
    Navigate to the cp-all-in-one directory under cp-all-in-one:

** cd cp-all-in-one
Start Confluent Platform with the -d option to run in detached mode:

** docker-compose up -d
The above command starts Confluent Platform with a separate containers for each Confluent Platform component. Your output should resemble the following:

Creating network "cp-all-in-one_default" with the default driver
Creating zookeeper ... done
Creating broker    ... done
Creating schema-registry ... done
Creating rest-proxy      ... done
Creating connect         ... done
Creating ksql-datagen    ... done
Creating ksqldb-server   ... done
Creating control-center  ... done
Creating ksqldb-cli      ... done
To verify that the services are up and running, run the following command:

** docker-compose ps
	Your output should resemble the following:

		 Name                    Command               State                Ports
	------------------------------------------------------------------------------------------
	broker            /etc/confluent/docker/run        Up      0.0.0.0:29092->29092/tcp,
															   0.0.0.0:9092->9092/tcp
	connect           /etc/confluent/docker/run        Up      0.0.0.0:8083->8083/tcp,
															   9092/tcp
	control-center    /etc/confluent/docker/run        Up      0.0.0.0:9021->9021/tcp
	ksqldb-cli        /bin/sh                          Up
	ksql-datagen      bash -c echo Waiting for K ...   Up
	ksqldb-server     /etc/confluent/docker/run        Up      0.0.0.0:8088->8088/tcp
	rest-proxy        /etc/confluent/docker/run        Up      0.0.0.0:8082->8082/tcp
	schema-registry   /etc/confluent/docker/run        Up      0.0.0.0:8081->8081/tcp
	zookeeper         /etc/confluent/docker/run        Up      0.0.0.0:2181->2181/tcp,
															   2888/tcp, 3888/tcp
If the state is not Up, rerun the docker-compose up -d command.

Reference Link:
----------------------------
https://docs.confluent.io/platform/current/quickstart/ce-docker-quickstart.html
