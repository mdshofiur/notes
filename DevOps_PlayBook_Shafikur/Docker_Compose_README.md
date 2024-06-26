# The Docker Compose file is the below of the a few projects:—-

```
version: '3.7'

services:
   # Mongodb
   mongodb:
      image: mongo:latest
      container_name: mongodb-container
      ports:
         - '27017:27017'

   # Zookeeper
   zookeeper:
      image: confluentinc/cp-zookeeper:latest
      container_name: zookeeper-container
      environment:
         ZOOKEEPER_CLIENT_PORT: 2181
         ZOOKEEPER_TICK_TIME: 2000
      ports:
         - 2181:2181

   # Kafka
   kafka:
      image: confluentinc/cp-kafka:latest
      container_name: kafka-container
      depends_on:
         - zookeeper
      ports:
         - 9092:9092
         - 29092:29092
      environment:
         KAFKA_BROKER_ID: 1
         KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
         KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://localhost:29092
         KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
         KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
         KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1

   # Postgresql
   postgresql:
      image: postgres:latest
      container_name: postgresql-container
      environment:
         POSTGRES_DB: my_database
         POSTGRES_USER: my_user
         POSTGRES_PASSWORD: 12345
      volumes:
         - ./local_pgdata:/var/lib/postgresql/data
      ports:
         - '5432:5432'

   #PGAdmin
   pgadmin:
      image: dpage/pgadmin4
      container_name: pgadmin-container
      ports:
         - '5050:5050'
      environment:
         PGADMIN_DEFAULT_EMAIL: shofiurbd13@gmail.com
         PGADMIN_DEFAULT_PASSWORD: 12345
      volumes:
         - ./pgadmin-data:/var/lib/pgadmin
      depends_on:
         - postgresql

   # Cassandra
   cassandra:
      image: cassandra:latest
      container_name: cassandra-container
      ports:
         - '9042:9042'
      environment:
         - CASSANDRA_USER=admin
         - CASSANDRA_PASSWORD=admin
      volumes:
         - ./cassandra:/var/lib/cassandra

   # Nginx
   nginx:
      image: nginx:latest
      container_name: nginx-container
      ports:
         - '80:80'
      volumes:
         - ./nginx.conf:/etc/nginx/nginx.conf

   # Redis
   redis:
      image: redis:latest
      container_name: redis-container
      ports:
         - '6379:6379'

   # Elasticsearch
   elasticsearch:
      image: docker.elastic.co/elasticsearch/elasticsearch:7.15.2
      container_name: elasticsearch
      environment:
         - discovery.type=single-node
         - xpack.security.enabled=false
      ports:
         - '9200:9200'
         - '9300:9300'
      volumes:
         - esdata:/usr/share/elasticsearch/data

volumes:
   local_pgdata:
      driver: local
   pgadmin-data:
      driver: local
   esdata:
      driver: local
```