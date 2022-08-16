# разворачиваем сетевую лабораторию

Дано
https://github.com/erlong15/otus-linux/tree/network
(ветка network)
Vagrantfile с начальным построением сети

inetRouter
centralRouter
centralServer
тестировалось на virtualbox
Планируемая архитектура
построить следующую архитектуру

Сеть office1
192.168.2.0/26 - dev
192.168.2.64/26 - test servers
192.168.2.128/26 - managers
192.168.2.192/26 - office hardware
Сеть office2
192.168.1.0/25 - dev
192.168.1.128/26 - test servers
192.168.1.192/26 - office hardware
Сеть central
192.168.0.0/28 - directors
192.168.0.32/28 - office hardware
192.168.0.64/26 - wifi
```
Office1 ---\
----> Central --IRouter --> internet
Office2----/
```
Итого должны получится следующие сервера
inetRouter
centralRouter
office1Router
office2Router
centralServer
office1Server
office2Server
Теоретическая часть
Найти свободные подсети
Посчитать сколько узлов в каждой подсети, включая свободные
Указать broadcast адрес для каждой подсети
проверить нет ли ошибок при разбиении
Практическая часть
Соединить офисы в сеть согласно схеме и настроить роутинг
Все сервера и роутеры должны ходить в инет черз inetRouter
Все сервера должны видеть друг друга
у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
при нехватке сетевых интервейсов добавить по несколько адресов на интерфейс
Формат сдачи ДЗ - vagrant + ansible


# сеть офис1

## dev
```
IP Address:	192.168.2.0
Network Address:	192.168.2.0
Usable Host IP Range:	192.168.2.1 - 192.168.2.62
Broadcast Address:	192.168.2.63
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```
## test servers
```
IP Address:	192.168.2.64
Network Address:	192.168.2.64
Usable Host IP Range:	192.168.2.65 - 192.168.2.126
Broadcast Address:	192.168.2.127
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```
## managers
```
IP Address:	192.168.2.128
Network Address:	192.168.2.128
Usable Host IP Range:	192.168.2.129 - 192.168.2.190
Broadcast Address:	192.168.2.191
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```
## office hardware
```
IP Address:	192.168.2.192
Network Address:	192.168.2.192
Usable Host IP Range:	192.168.2.193 - 192.168.2.254
Broadcast Address:	192.168.2.255
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```
# Сеть офис2

## dev
```
IP Address:	192.168.1.0
Network Address:	192.168.1.0
Usable Host IP Range:	192.168.1.1 - 192.168.1.126
Broadcast Address:	192.168.1.127
Total Number of Hosts:	128
Number of Usable Hosts:	126
Subnet Mask:	255.255.255.128
Wildcard Mask:	0.0.0.127
```
## test servers
```
IP Address:	192.168.1.128
Network Address:	192.168.1.128
Usable Host IP Range:	192.168.1.129 - 192.168.1.190
Broadcast Address:	192.168.1.191
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```
## office hardware
```
IP Address:	192.168.1.192
Network Address:	192.168.1.192
Usable Host IP Range:	192.168.1.193 - 192.168.1.254
Broadcast Address:	192.168.1.255
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```

# Сеть central
## directors
```
IP Address:	192.168.0.0
Network Address:	192.168.0.0
Usable Host IP Range:	192.168.0.1 - 192.168.0.14
Broadcast Address:	192.168.0.15
Total Number of Hosts:	16
Number of Usable Hosts:	14
Subnet Mask:	255.255.255.240
Wildcard Mask:	0.0.0.15
```
## office hardware
```
IP Address:	192.168.0.32
Network Address:	192.168.0.32
Usable Host IP Range:	192.168.0.33 - 192.168.0.46
Broadcast Address:	192.168.0.47
Total Number of Hosts:	16
Number of Usable Hosts:	14
Subnet Mask:	255.255.255.240
Wildcard Mask:	0.0.0.15
```
## wifi
```
IP Address:	192.168.0.64
Network Address:	192.168.0.64
Usable Host IP Range:	192.168.0.65 - 192.168.0.126
Broadcast Address:	192.168.0.127
Total Number of Hosts:	64
Number of Usable Hosts:	62
Subnet Mask:	255.255.255.192
Wildcard Mask:	0.0.0.63
```

Реализовал схему
![Иллюстрация к проекту](https://github.com/asm1213/dz_otus/blob/main/DZ_17/net.jpg)

при желании можно добавить дополнительный оффис.
