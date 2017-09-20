### Creating the Neo4j DB in a Docker container

* [Reference card](https://neo4j.com/docs/cypher-refcard/current/)
* ```docker pull neo4j```
* Download the Dockerfile from [here](https://hub.docker.com/_/neo4j/)
* Navigate to where you downloaded the Dockerfile and run ```docker build -t neo4j .```
* Run this:
    ```
    docker run \
    --publish=7474:7474 --publish=7687:7687 \
    --volume=~/path/to/your/data/files:/data \
    --env=NEO4J_AUTH=none \
    neo4j
    ```
