# Documentation of configuration decisions for the Digispine

## Kafka
TODO

## Schemaregistry
TODO

## Kafka-UI
Kafka-UI provides an interface for direct interaction with Kafka.
It is also able to provide an interface for the schemaregistry and ksqlDB, if they are registered.
The environment-properties "KAFKA_CLUSTERS_0_SCHEMAREGISTRY" and "KAFKA_CLUSTERS_0_KSQLDBSERVER" provide default configurations for the address of the schemaregistry and ksqlDB-Server, so that they are registered automatically.
In an SCS, the schemaregistry and ksqlDB-Server can be accessed with the following addresses respectively: "http://schemaregistry:8085", "http://ksqldbServer:8088".

TODO: document other decisions

## ksqlDB-Server
TODO

## ksqlDB-CLI
TODO

## Volumes
TODO
