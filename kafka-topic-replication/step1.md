## Setup Cluster

Cluster ini berisikan 2 broker dengan masing masing zookeeper (total ada 4 service). Cluster ini dibangun diatas service docker.

Sekarang kita akan membuat sebuah file bernama `docker-compose.yaml`

`touch docker-compose.yaml`{{execute}}

Lalu masukan code berikut kedalam file tersebut.

`
---
version: '2'
services:
  zookeeper-1:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - 22181:2181

  zookeeper-2:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - 32181:2181
  
  kafka-1:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper-1
      - zookeeper-2

    ports:
      - 29092:29092
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper-1:2181,zookeeper-2:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka-1:9092,PLAINTEXT_HOST://localhost:29092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
  kafka-2:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper-1
      - zookeeper-2
    ports:
      - 39092:39092
    environment:
      KAFKA_BROKER_ID: 2
      KAFKA_ZOOKEEPER_CONNECT: zookeeper-1:2181,zookeeper-2:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka-2:9092,PLAINTEXT_HOST://localhost:39092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1

`{{copy}}

## Fire Up Cluster

Langkah selanjutnya kita tinggal menjalankan Cluster agar dapat digunakan.

`docker-compose up -d`{{execute}}

Pada langkah ini, service docker mengunduh dan mengelola segala yang dibutuhkan mulai dari image kafka, zookeeper dan juga membuat masing masing service.

## Check Cluster ID

Pengecekan ini dilakukan untuk melihat output cluster dari masing masing broker kafka. Output yang diekspektasi harusnya sama.

Untuk mengecek cluster id dari kafka-1, kita menggunakan perintah dibawah. 

`docker-compose exec kafka-1 kafka-cluster cluster-id --bootstrap-server kafka-1:9092`{{execute}}

Selanjutnya untuk kafka-2, kita menggunakan perintah dibawah. 

`docker-compose exec kafka-2 kafka-cluster cluster-id --bootstrap-server kafka-2:9092`{{execute}}

Output yang ditampilkan kedua perintah harusnya sama.