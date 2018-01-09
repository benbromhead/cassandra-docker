# Cassandra-docker

This is the Instaclustr public docker image for Apache Cassandra. 
It contains docker images for Cassandra 3.0 and 3.11.1. 

I contains best practices and lessons learnt from running Cassandra on docker for the last 4 years over 1000's of clusters. 
It also supports configuration via environment variables in the same manner as the [official docker cassandra image](https://hub.docker.com/_/cassandra/)

Primary configuration of Cassandra should be done by creating a volume mount on the Cassandra config
directory and providing configuration externally (manually, docker swarm, k8s), however support for
basic configuration via environment variables does exist. See below. 

For the best experince, Cassandra in docker should be run with the following:

todo dockewr recommended runtime flags