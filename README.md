# Mongo Sharded Cluster with Docker Compose
Based in https://github.com/singram/mongo-docker-compose, 

Mongo last version and initialize config with default ports: https://docs.mongodb.com/manual/reference/default-mongodb-port/

This repository provides a fully sharded mongo environment using docker-compose and volume storage.

The MongoDB environment consists of the following docker containers

 - **mongosrs(1-3)n(1-3)**: Mongod data server with three replica sets containing 3 nodes each (9 containers)
 - **mongocfg(1-3)**: Stores metadata for sharded data distribution (3 containers)
 - **mongos(1-2)**: Mongo routing service to connect to the cluster through (2 containers)

## Caveats

 - This is designed to have a minimal disk footprint at the cost of durability.
 - This is designed in no way for production but as a cheap learning and exploration vehicle.

## Installation:

### Install Docker
    https://docs.docker.com/engine/installation/

### Install Docker-compose
    https://docs.docker.com/compose/install/

### Check out the repository

    git clone git@github.com:psoldier/dockercompose-mongo-sharded-cluster.git
    cd dockercompose-mongo-sharded-cluster


### Setup Cluster
This will pull all the images from [Docker index](https://index.docker.io/u/jacksoncage/mongo/) and run all the containers.

    docker-compose up

Please note that you will need docker-compose 1.4.2 or better for this to work due to circular references between cluster members.
You will need to run the following *once* only to initialize all replica sets and shard data across them

    ./initiate

Stop containers

    ctrl + c

You should now be able connect to mongos1 and the new sharded cluster from the mongos container itself using the mongo shell to connect to the running mongos process

    docker exec -it mongos1 mongo

## Persistent storage
Data is stored at Data volumes from Docker


## Remove containers and data volume

    docker-compose down -v

