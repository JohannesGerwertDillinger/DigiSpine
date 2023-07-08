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