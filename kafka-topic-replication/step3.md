## Create Event

Kali ini kita akan sedikit membuat message pada Topic yang sudah dibuat. 

`docker-compose exec kafka-1 kafka-console-producer --bootstrap kafka-1:9092 --topic Topic-X`{{execute}}

Disini coba teman teman masukan message seperti:
```
> Hello world
> Hello Big Data #9
```

## Consume Event

Buatlah sebuah terminal baru dengan cara mengeklik ikon (+) disamping `Terminal` lalu pilih `Open New Terminal`.

Kita akan melihat event/message yang ada pada `Topic-X`.

`docker-compose exec kafka-1 kafka-console-consumer --bootstrap kafka-2:9092 --topic Topic-X`{{execute}}