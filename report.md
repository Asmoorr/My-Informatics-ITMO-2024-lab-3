# Отчёт по лабораторной работе №3

## Проверка подключения к интернету
Для осуществелния проверки попробуем помощью утилиты `ping` попробуем подключиться к удалённому серверу, например, google.com

![image](https://github.com/user-attachments/assets/5a956909-2cbd-45ec-ab47-862c13c69340)

*0% packet loss* говорит о наличии стабильного интернет соединения

## Создание локальной сети
1. С помощью приложения Virtual Box создадим локальную сеть NAT:
   
![image](https://github.com/user-attachments/assets/9dd3edba-c183-4403-8e1b-83ab663b6d1d)

![image](https://github.com/user-attachments/assets/708aadfe-cfc8-4aa2-b2b0-3ff2e5060d5c)

2. Затем в настройках каждой виртуальной машины добавим созданную сеть:
   
![image](https://github.com/user-attachments/assets/48c08cac-876c-4f74-b1d7-0b75cc5a86e2)

## Проверка доступа
Для проверки доступа от машины А к машине Б воспользуемся той же командой `ping`. Для этого:
1. С помощью `ip a` посмотрим IP адрес машины Б в локальной сети
   
   ![image](https://github.com/user-attachments/assets/9d89bdab-0657-4169-a3db-959fd4ca72ba)
   
   *10.0.4.7*
2. Командой `ping` попробуем подключиться к машине Б
   
   ![image](https://github.com/user-attachments/assets/ac8bc52b-f6aa-48fb-892f-a79257894c96)
   
   *0% packet loss*! Нам удалось подлючиться
3. Аналогично для проверки доступа от машины А к машине В
   
   ![image](https://github.com/user-attachments/assets/a5c125da-7d65-437e-be63-31c7975f9836)

## Ограничение доступа
Для ограничения доступа восользуемся утилитой `iptables`
1. Ограничение входящиих запросов `sudo iptables -A INPUT -s 10.0.4.7 -j DROP`
2. Ограничение исходящих запросов `sudo iptables -A OUTPUT -d 10.0.4.7 -j DROP`
3. Сохраним настройки в `/etc/iptables-conf/iptables_rules.ipv4`
4. Проверим отстутсвие доступа
   
   ![image](https://github.com/user-attachments/assets/e1bb1ead-09d1-472d-b649-8d6dbe366e29)

   ![image](https://github.com/user-attachments/assets/847f95e8-741b-46ed-8298-2c85d4ba70dd)
   
P.s При перезапуске машины необходимо заново применять правила с помощью команды `sudo iptables-restore /etc/iptables-conf/iptables_rules.ipv4` или автоматизировать данный процесс. Например с помощью сторонней утилиты `iptables-persistent`.


