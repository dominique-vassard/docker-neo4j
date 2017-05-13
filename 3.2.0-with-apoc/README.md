# Neo4j 3.2.0 with APOC

## Introduction
This code is designed to create a Neo4j Community Edition image which includes APOC procedures.
Neo4j, graph database: https://neo4j.com/developer/get-started/
APOC, plugin containing hundreds of useful procedures: https://neo4j-contrib.github.io/neo4j-apoc-procedures/

## Description
This image:
- is based on neo4j 3.2.0 image (available images: https://hub.docker.com/_/neo4j/)
- includes APOC procedure (default: 3.2.0.2)
-  exposes 3 ports:
    +  7474: browser and HTTP REST api
    +  7473: browser and HTTPS REST api
    +  7687: Bolt
- has 3 volumes:
    + /data: for the database data
    + /logs: database logs
    + /var/lib/import: used by LOAD CSV queries
- has 2 overridable env variable:
    + APOC_VERSION: the wanted APOC version (will be downloaded from: https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/${APOC_VERSION}/apoc-${APOC_VERSION}-all.jar)
    + NEO4J_AUTH: the user/password (default: neo4j/neo4j). Note that in Neo4J Community Edition, username is always `neo4j`

## How to use

### Prerequisite: Install Docker Engine
https://docs.docker.com/engine/installation/

### Build the image
`docker build -t wanted_image_name:wanted_tag .`
Example: `docker build -t dominiquev/neo4j:3.2.0 .`

### Or pull an image from registry
Image list is availabe at: https://hub.docker.com/r/dominiquev/neo4j/
Pull example: ` dominiquev/neo4j:3.2.0`

### Use the image
The minimal command is:
```
docker run \
-p 7474:7474
-p 7687:7687
image_name
```
Example:
```
docker run \
-p 7474:7474
-p 7687:7687
 dominiquev/neo4j:3.2.0
```

The complete command is:
```
docker run --name wanted_container_name \
-p 7474:7474 -p 7687:7687 \
-v path_to_data_dir:/data \
-v path_to_import_dir:/var/lib/neo4j/import \
-v parto_to_logs_dir:/logs \
--env NEO4J_AUTH neo4j/password \
--env APOC_VERSION 3.2.0.2 \
image_name
```
Example:
If you have create a folder structured as:
neo4j
    |- conf
    |- data
    |- import
    |- logs
after `cd path_to_neo4j_dir`, you will launch this command:
```
docker run --name neo4j_3_2_0 \
-p 7474:7474 -p 7687:7687 \
-v $(pwd)/data:/data \
-v $(pwd)/import:/var/lib/neo4j/import \
-v $(pwd)/logs:/logs \
--env NEO4J_AUTH neo4j/my_secret_pass \
--env APOC_VERSION 3.2.0.2 \
 dominiquev/neo4j:3.2.0 
```