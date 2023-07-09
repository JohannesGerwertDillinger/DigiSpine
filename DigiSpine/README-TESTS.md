## Tests

- Start one of the compose files 

```shell
docker run -it --network=host edenhill/kcat:1.7.1 -b 192.168.178.63:9092 -L           
Metadata for all topics (from broker -1: 192.168.178.63:9092/bootstrap):
3 brokers:
broker 1 at localhost:9092
broker 2 at localhost:9093
broker 3 at localhost:9094 (controller)
1 topics:
topic "flugdaten" with 1 partitions:
partition 0, leader 2, replicas: 2, isrs: 2
michael@Michaels-Mac-mini-2 .docker % 
```

### Test restarting single kafka instances


```bash 
./kafka-topics.sh --delete --topic flugdaten --bootstrap-server 127.0.0.1:9092
```

./kafka-topics.sh --create --topic flugdaten --partitions 1 --replication-factor 3 --bootstrap-server 127.0.0.1:9092


```shell
MYCOUNTER=0; while true; do let MYCOUNTER++; echo "MyCounter $MYCOUNTER"; sleep 1; done | ./kafka-console-producer.sh --topic flugdaten --bootstrap-server=localhost:9092
```

```shell
./kafka-console-consumer.sh --topic flugdaten --bootstrap-server=localhost:9092
```
