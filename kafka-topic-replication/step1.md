## Setup Cluster

Cluster ini berisikan 2 broker dengan masing masing zookeeper (total ada 4 service). Cluster ini dibangun diatas service docker.

Sekarang kita akan mengunduh sebuah file bernama `docker-compose.yaml`

`curl https://gist.githubusercontent.com/sdcilsy/7030550f64cd87abf3d3e102fd0aa14e/raw/4d9003f9b2773334d1670839142a4e0c228ca0cb/kafka-topic-replication-cluster.yaml -o docker-compose.yaml`{{execute}}

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