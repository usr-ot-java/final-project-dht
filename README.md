# Distributed Hash Table (DHT) based on Chord protocol 

Distributed Hash Table (DHT) based on the Chord architecture with the access by REST API model written in Java.

It is a decentralized distributed system that provides a lookup service similar to a hash table. 
Key, value pairs are stored in a DHT, and any participating node can retrieve the value associated with a given key. 
All the nodes communicate with each other through the HTTP and HTTPs protocols and REST-ful APIs. 
The nodes authenticate each other requests using basic access authentication method.

## Project Presentation

The presentation of the project is available on 
[Google Slides](https://docs.google.com/presentation/d/1MySI3ElJZ2e-NUjAcMdtX_0gvpC8tb_pILWDZl8wVHk/edit?usp=sharing).

## Features

- Lookup for a key takes at most `O(log N)` hops where N is the number of nodes in the cluster.
- Dynamic node join in the cluster topology (knowing one arbitrary node endpoint address is enough).
- Data transfer to the joining nodes (rebalancing).
- Implemented stabilization protocol for the cluster.
- Secure communication between the nodes (if enabled).
- The nodes use basic authentication method.

## OpenAPI Specification

The API is documented using the OpenAPI Specification.

The specification is stored in the file [openapi.yaml](./openapi.yml).

## Configuration

There are the parameters that allows configuration of DHT server node
through the VM options:

```shell
-Dserver.port=<port> # Server node port
-Ddht.node.id=<id> # Server node ID (optional)
-Ddht.node.address="<host>:<port>" # Current server node address 
-Ddht.node.join.address="<host>:<port>" # Arbitrary node's number of the cluster topology (pass empty iff it is the first node of the cluster)  
-Ddht.node.security.username="<login>" # Username for basic auth (used by nodes in communication)
-Ddht.node.security.password="<password>" # Password for basic auth (used by nodes in communication)
```

## Running locally 2-node cluster

To run 2-node cluster locally you should specify the following VM options.

The VM options of the first instance:
```shell
-Dserver.port=8081
-Ddht.node.id=1
-Ddht.node.address="localhost:8081"
-Ddht.node.join.address="" 
-Ddht.node.security.username="login"
-Ddht.node.security.password="password"
```

The VM options of the second instance (this node joins the first node):
```shell
-Dserver.port=8082
-Ddht.node.id=2
-Ddht.node.address="localhost:8082"
-Ddht.node.join.address="localhost:8081" 
-Ddht.node.security.username="login"
-Ddht.node.security.password="password"
```


## How to run?

There are two ways to run our project: plain Java process and Docker container.

### Run in Docker

```bash
docker build -t dht .
docker run -p 8080:8080 dht
```

### Building Jar

```bash
/mvnw clean install
java -jar ./target/dht-chord-0.0.1-SNAPSHOT.jar
```

## Contribution
You can contribute to our project - we are glad to new ideas and fixes.

## License

The project is released and distributed under [MIT License](https://en.wikipedia.org/wiki/MIT_License).

