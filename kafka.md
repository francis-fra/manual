## Kafka
create topic (kafka-arch)
```
kafka-topics --create --topic kafka-arch --partitions 1 --replication-factor 1 --zookeeper localhost:2181
```
inspect directory
```
ls -alh /var/lib/kafka/data
```
produce data from cli
```
kafka-console-producer --topic "kafka-arch" --broker-list localhost:9092
```

### Kafka (Docker)
Download compose file
```
curl --silent --output docker-compose.yml \
  https://raw.githubusercontent.com/confluentinc/cp-all-in-one/6.2.0-post/cp-all-in-one-community/docker-compose.yml
```
Install
```
docker-compose up -d
```
check if it is running
```
docker-compose ps
```
Control Center
```
http://localhost:9021/
```

### Kafka command
run command preceded by:
```
docker-compose exec broker <command>
```
e.g. Create topic
```
docker-compose exec broker kafka-topics \
  --create \
  --bootstrap-server localhost:9092 \
  --replication-factor 1 \
  --partitions 1 \
  --topic users
```

Stop Containers
```
docker-compose stop
```
to prune (remove image)
```
docker system prune -a --volumes --filter "label=io.confluent.docker"
```
