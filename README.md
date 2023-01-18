# Kafka-Ranger-Demo

This repository consists of all the important requirements to set up a kafka integrated with Apache Ranger, it is based on https://github.com/apache/ranger/tree/master/dev-support/ranger-docker

## Steps to set up the demo system:

1. Run the following:
~~~
chmod +x download-archives.sh && ./download-archives.sh 
~~~

2. Execute following commands to set environment variables to build Apache Ranger docker containers:
   ~~~
   export DOCKER_BUILDKIT=1
   export COMPOSE_DOCKER_CLI_BUILD=1
   export RANGER_DB_TYPE=postgres
   ~~~
   
3. Build Apache Ranger in containers using docker-compose

   * Execute following command to build Apache Ranger:
      ~~~
      docker-compose -f docker-compose.ranger-base.yml -f docker-compose.ranger-build.yml up
      ~~~

      Time taken to complete the build might vary (upto an hour), depending on status of ```${HOME}/.m2``` directory cache.
   * Execute following command to start Ranger, Ranger enabled HDFS/YARN/HBase/Hive/Kafka/Knox and dependent services (Solr, DB) in containers:
       ~~~
      docker-compose -f docker-compose.ranger-base.yml -f docker-compose.ranger.yml -f docker-compose.ranger-${RANGER_DB_TYPE}.yml -f docker-compose.ranger-usersync.yml -f docker-compose.ranger-tagsync.yml -f docker-compose.ranger-kafka.yml up -d
      ~~~
  
4. Ranger Admin can be accessed at http://localhost:6080 (admin/rangerR0cks!)

5. To bring the containers down run:
  ~~~
 docker-compose -f docker-compose.ranger-base.yml -f docker-compose.ranger.yml -f docker-compose.ranger-${RANGER_DB_TYPE}.yml -f docker-compose.ranger-usersync.yml -f docker-compose.ranger-tagsync.yml -f docker-compose.ranger-kafka.yml down
 ~~~
    
