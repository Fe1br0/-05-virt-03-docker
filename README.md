# Домашнее задание к занятию "5.3. Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера"



## Задача 1
 
 https://hub.docker.com/r/fe1br0/netology
 
 Возможно я не совсем правильно понял задачу , но делал так : запулил образ ubuntu/nginx , далее зашел внутрь этого контейнера , там поменял необходимые значения в конфиг файле nginx, после закоммитил этот контейнер и запушил его в свой репозиторий , или это все необходимо было производить непосредственно через Dokcerfile? В доказательство проделанной работы прикладываю скрины :)
 
 

![virt03](https://user-images.githubusercontent.com/106814458/195726862-169808e0-2264-438d-aecd-094e167db1bc.jpg)
![virt03-2](https://user-images.githubusercontent.com/106814458/195726867-fdf3ed06-8c90-4af7-8b41-5fa92a903c5c.jpg)

## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
"Подходит ли в этом сценарии использование Docker контейнеров или лучше подойдет виртуальная машина, физическая машина? Может быть возможны разные варианты?"

Детально опишите и обоснуйте свой выбор.
```


Сценарий:

- Высоконагруженное монолитное java веб-приложение - считаю самым оптимальным выбором будет физическая машина ,  докер не подойдет т.к. нужны максимальная производительность 
- Nodejs веб-приложение - в этом случае мой выбор бы пал на ВМ/докер т.к. вряд-ли у веб приложений будет серьезная нагрузка.
- Мобильное приложение c версиями для Android и iOS  - здесь также считаю уместны ВМ/докер , физическая машина будет излишне
- Шина данных на базе Apache Kafka - ВМ либо физическая машина , Kafka написан на Java , думаю не лишним будет максимальная производительность 
- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana - Докер / ВМ отлично справятся с этой задачей
- Мониторинг-стек на базе Prometheus и Grafana ВМ/докер , в физ.машине считаю необходимости нет 
- MongoDB, как основное хранилище данных для java-приложения - здесь приоритет в физ.машина, высокая отказоустойчивость и производительность.
- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry - ВМ\докер подойдет , высоких нагрузок не ожидается , также нет необходимости в высокой отказоустойчивости 


```

## Задача 3

```
Netology_DZ> sudo docker run -t -d --name centos_netology -v  /root/Netology_DZ:/share/data centos
0bf3e3aa1917281f411b524eeb025598c5f23835628cdcea6f139f40c572735c
Netology_DZ> sudo docker run -t -d --name debian_netology -v  /root/Netology_DZ:/share/data debian
ef3730f4a6e2c82aa0672e9bf9705f3a8be117cbc668ddfeba2f99a17898a1a2
Netology_DZ> docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED             STATUS             PORTS     NAMES
ef3730f4a6e2   debian         "bash"                   8 seconds ago       Up 6 seconds                 debian_netology
0bf3e3aa1917   centos         "/bin/bash"              58 seconds ago      Up 56 seconds                centos_netology
6f5ec9243fa3   ubuntu/nginx   "/docker-entrypoint.…"   About an hour ago   Up About an hour   80/tcp    dreamy_mendel
Netology_DZ> docker exec -it centos_netology bash
[root@0bf3e3aa1917 /]# echo 'test centos' > /share/data/centos_test.txt
[root@0bf3e3aa1917 /]# exit
exit
Netology_DZ> docker exec -it debian_netology bash
root@ef3730f4a6e2:/# echo 'test debian' > /share/data/debian_test.txt
root@ef3730f4a6e2:/# exit
exit
Netology_DZ> echo 'test ubunta' > ubuntu.txt
Netology_DZ> ll
итого 20
drwxr-xr-x  2 root root 4096 окт 12 00:00 ./
drwx------ 14 root root 4096 окт 11 21:03 ../
-rw-r--r--  1 root root   12 окт 11 23:58 centos_test.txt
-rw-r--r--  1 root root   12 окт 12 00:00 debian_test.txt
-rw-r--r--  1 root root   12 окт 12 00:00 ubuntu.txt
Netology_DZ> docker exec -it centos_netology bash
[root@0bf3e3aa1917 /]# ll /share/data/
bash: ll: command not found
[root@0bf3e3aa1917 /]# ls /share/data/
centos_test.txt  debian_test.txt  ubuntu.txt
[root@0bf3e3aa1917 /]# exit
exit
Netology_DZ> docker exec -it debian_netology bash
root@ef3730f4a6e2:/# ls /share/data/
centos_test.txt  debian_test.txt  ubuntu.txt
root@ef3730f4a6e2:/# 

```

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

https://hub.docker.com/r/fe1br0/ansible


