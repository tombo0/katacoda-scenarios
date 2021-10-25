## Create Event

Kali ini kita akan sedikit membuat message pada Topic yang sudah dibuat. 

`docker-compose exec kafka-1 kafka-console-producer --bootstrap kafka-1:9092 --topic Topic-X`{{execute}}

Disini coba teman teman masukan message seperti:

`Hello world`{{execute}}
`Hello Big Data #9`{{execute}}

## Consume Event

Buatlah sebuah terminal baru dengan cara mengeklik ikon (+) disamping `Terminal` lalu pilih `Open New Terminal`.

Kita akan melihat event/message yang ada pada `Topic-X`.

`docker-compose exec kafka-1 kafka-console-consumer --bootstrap kafka-2:9092 --topic Topic-X --from-beginning`{{execute}}

Kembali ke `Terminal 1` untuk membuat message baru.

`Ini message baru`{{execute}}
`Salam kenal`{{execute}}

Lalu lihat lagi `Terminal 2` untuk melihat hasilnya.