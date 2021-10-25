## Create Event

Kali ini kita akan sedikit membuat message pada Topic yang sudah dibuat. 

`docker-compose exec kafka-1 kafka-console-producer --bootstrap kafka-1:9092 --topic Topic-X`{{execute}}

Disini coba teman teman masukan message seperti:
```
> Hello world
> Hello Big Data #9