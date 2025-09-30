# kafka_local
Run Kafka locally

docker-compose up -d

# Создать топик
docker exec -it kafka kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

# Список всех топиков
docker exec -it kafka kafka-topics.sh --list --bootstrap-server localhost:9092

# Удалить топик
docker exec -it kafka kafka-topics.sh --delete --topic test-topic --bootstrap-server localhost:9092

# Отправить сообщение
docker exec -it kafka kafka-console-producer.sh --topic test-topic --bootstrap-server localhost:9092
> Hello from Kafka!  # Нажмите Enter. Ctrl-c (Выйти)

# Читаем сообщения (в другом терминале)
docker exec -it kafka kafka-console-consumer.sh --topic test-topic --bootstrap-server localhost:9092 --from-beginning

# Информация о топике
docker exec -it kafka kafka-topics.sh --describe --topic test-topic --bootstrap-server localhost:9092


-Spring-
Закомментировать аутентификацию, если есть:
kafka-auth:
  protocol: "SASL_PLAINTEXT"
  mechanism: "SCRAM-SHA-256"
  jaasConfig: ""

Добавить в local для нужного consumer или producer:
kafka:
  custom:
    exchangeSchedule:
      topic: "mpi.exchangeschedule.schedules.test"
      consumer:
        bootstrap-servers: localhost:9092
        group-id: "antonov"
        #key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
        #value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
