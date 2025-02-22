# Выполнение домашнего задания. 1 месяц. Занятие 4. Канальный уровень. Ethernet 
## Цели
### Часть 1. Создание и настройка сети
### Часть 2. Изучене таблицы MAC-адресов коммутатора

## Мое решение
### Часть 1. Создание и настройка сети

Согласно данной в ТЗ топологии (см. скриншот) создал схему:

![image](https://github.com/user-attachments/assets/abd8a84e-e5a1-48da-80ba-ca08229ef0ec)

Моя схема: 

![image](https://github.com/user-attachments/assets/e5b6e53d-df32-4474-a43c-92e0733c467e)


#### Настройка
Далее провел настройку по аналогии с первой лабой для обоих коммутаторов и PC  - https://github.com/iosif-tihonenkov/Network-Engineer.-Basic/tree/main/lab01

Как видно - все работает. С PC1 можно достать до SW1: 

![image](https://github.com/user-attachments/assets/5604361d-bc4d-44d3-bff2-d212f04a9da3)


Переходим ко второй части) 

### Часть 2. Изучение таблицы MAC-адресов коммутатора
#### Шаг 1. Запишите MAC-адреса сетевых устройств.

*a.	Откройте командную строку на PC-A и PC-B и введите команду ipconfig /all.
Открытие окна командной строки Windows
Вопрос:
Назовите физические адреса адаптера Ethernet.
MAC-адрес компьютера PC-A:
MAC-адрес компьютера PC-B:*

Окей, поехали) 

Залетаем на PC0 (оно же у нас PC-A). Выполняем команду *ipconfig /all*. 
По факт - получаем информацию на FastEthernet0 и Bluetooth. Нас интересует только FastEthernet. 
MAC-адрес компьютера PC-A: 0090.0C64.7974 (см. скриншот)

![image](https://github.com/user-attachments/assets/170f0928-c3bf-4f11-bf34-383e8af6b316)

На самом деле можно посмотреть MAC-адрес, просто наведя мышку на PC на схеме: 

![image](https://github.com/user-attachments/assets/f7ef241b-cfcc-42fe-b1b0-6014e02cc965)








