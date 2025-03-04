# Выполнение домашнего задания. 1 месяц. Занятие 2. Команды IOS. Базовая конфигурация устройств

## Задания

### Часть 1. Проверка конфигурации коммутатора по умолчанию

### Часть 2. Создание сети и настройка основных параметров устройства
- Настройте базовые параметры коммутатора.
- Настройте IP-адрес для ПК.

### Часть 3. Проверка сетевых подключений
- Отобразите конфигурацию устройства.
- Протестируйте сквозное соединение, отправив эхо-запрос.
- Протестируйте возможности удаленного управления с помощью Telnet.

## Решение

### Часть 1. Проверка конфигурации коммутатора по умолчанию
#### Шаг 1. Создайте сеть согласно топологии
Я создал сеть из двух устройств:
- ПК;
- Коммутатор Cisco 2960;

*а) Подсоедините консольный кабель, как показано в топологии. На данном этапе не подключайте каель Ethernet компьютера PC-A*

**Моя реализация на скриншоте:**
![](https://github.com/iosif-tihonenkov/Network-Engineer.-Basic/blob/main/lab01/jpg/shema01.jpg)

*b) Установите консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.*

*Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? Почему нельзя подключиться к коммутатору через Telnet или SSH?*

**Мой ответ:**
Подключение установлено (см. скриншот):
![](https://github.com/iosif-tihonenkov/Network-Engineer.-Basic/blob/main/lab01/jpg/scrin01.jpg)

Консольное подключение для первоначальной настройки коммутатора нужно использовать по причине того, что это первоначальная настройка и коммутатор чист. Следовательно не настроены IP адресс, на VTY линии не настроен доступ, пароли. Следовательно наш единственный вариант работать с коммутатором на данном моменте - консольное подключение. Собственно, по тем же причинам к нему нельзя подключиться через Telnet или SSH. 

#### Шаг 2. Проверьте настройки коммутатора по умолчанию. 
**Мое решение:**
Я перешел в привилегированный режим: 

    Switch>enable
    Switch#

Проверяю, что файл конфигурации пустой. Для этого запускаю команду *show running-config* и вижу, что не указан пароль и, что важнее - IP адресс.

*b) Изучите текущий файл running configuration.*
- *Сколько интерфейсов FastEthernet имеется на коммутаторе 2960?* - **Мой ответ - 24**
- *Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960?* - **Мой ответ - 2**
- *Каков диапазон значений, отображаемых в VTY-линиях?* - **Мой ответ - 0-15. Если точнее - 0-4 и 5-15**

*с)Изучите файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM).
Почему появляется это сообщение?*

**Мой ответ:** я вызываю данный файл при помощи команды *show startup-config* из верхнего уровня привелигированного доступа. Мне выдается сообщение: *startup-config is not present*, что означает, что файл не представлен. Я считаю, что данное сообщение появляется по причине того, что коммутатор запускается первый раз и его конфигурация еще не была сохранена в NVRAM.

*d.	Изучите характеристики SVI для VLAN 1.
Вопросы:
Назначен ли IP-адрес сети VLAN 1?
Какой MAC-адрес имеет SVI? Возможны различные варианты ответов.
Данный интерфейс включен?*

**Мой ответ:**

Что бы посмотреть характеристики SVI (интерфейс для удаленного доступа к коммутатору) для Vlan1 я использовал команду *Switch#show interfaces Vlan1*. В результате я получил информацию по данному виртуальному интерфейсу. 
- Что бы проверить IP адрес сети VLAN1 я ввел команду *Switch#show ip interface Vlan 1*. В результате получил ответ, что оно вообще отключено и не настроено. Соответственно, я так понимаю ,IP адрес не назначен.
- Какой MAC-адрес? В выгрузке указано, цитирую *Hardware is CPU Interface, address is 0040.0b47.a739 (bia 0040.0b47.a739)* . Собственно тут и указаны MAC адреса. На сколько я понимаю - установленный (bia родной с завода).
- Данный интерфейс включен? Нет

*e.	Изучите IP-свойства интерфейса SVI сети VLAN 1.
Вопрос:
Какие выходные данные вы видите?*

**Мой ответ:** 
Что бы посмотреть IP-свойства интерфейса SVI сети VLAN 1 нужно ввести команду *Switch#show ip interface Vlan 1*. Которая выведет информацию, что ничего не настроено 

*f.	Подсоедините кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучите IP-свойства интерфейса SVI сети VLAN 1. Дождитесь согласования параметров скорости и дуплекса между коммутатором и ПК.
Примечание. При использовании Netlab включите интерфейс F0/6 на коммутаторе S1.
Вопрос:
Какие выходные данные вы видите*

**Мой ответ:**
Подсоединил к 6 порту. Результат на скриншоте ниже: 
![](https://github.com/iosif-tihonenkov/Network-Engineer.-Basic/blob/main/lab01/jpg/shema02.jpg)
Какие выходные данные я виже? Согласно тому, что показано на скриншоте, я вижу что данный порт подключен, использует VLAN 1 и указан MAC адресс порта.

*g.	Изучите сведения о версии ОС Cisco IOS на коммутаторе.
Вопросы:
Под управлением какой версии ОС Cisco IOS работает коммутатор?
Как называется файл образа системы?*

**Мой ответ:**
Что бы получить сведения о версии ОС Cisco IOS на коммутаторе я ввел команду *Switch# show version*, которая показывает, что установлена версия 15.0(2)SE4. Файл образа системы называется *flash:c2960-lanbasek9-mz.150-2.SE4.bin*. 

*h.	Изучите свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A.
Switch# show interface f0/6 
Вопрос:
Интерфейс включен или выключен?
Что нужно сделать, чтобы включить интерфейс?
Какой MAC-адрес у интерфейса?
Какие настройки скорости и дуплекса заданы в интерфейсе?*

**Мой ответ:**
Тут мне уже указана команда) 
Интерфейс включен - на это указывает информация *FastEthernet 0/6 is up, line protocl is up (connected).
Что нужно сделать, что бы включить интерфейс? В данном случае ничего. Но если бы он был выключен - то команды были бы в следующем порядке (проверил): 
- Switch#configure terminal (переходим в режим управления конфигурацией)
- Switch(config)#interface fastEthernet 0/6 (переходим к конфигурированию нужного нам порта)
- Switch(config-if)#no shutdown (включаем порт)

Какой MAC-адрес у интерфейса? Переходим опять к команде *Switch#show interface FastEthernet 0/6* и получаем информацию по MAC-адресу: *address is 00d0.58a0.0406 (bia 00d0.58a0.0406)*. Кстати, на крайнем скрине так же можно посмотреть MAC-адреса всех портов. 
Что же касается настроек скорости и дуплекса заданных в интерфейсе? Нам эту информацию дает строка: *Full-duplex, 100Mb/s*, которая показывает скорость в 100Мб в секунду и полный дуплекс. 

*i.	Изучите флеш-память.
Выполните одну из следующих команд, чтобы изучить содержимое флеш-каталога.
Switch# show flash 
Switch# dir flash: 
В конце имени файла указано расширение, например .bin. Каталоги не имеют расширения файла.
Вопрос:
Какое имя присвоено образу Cisco IOS?*

**Мой ответ:**

Имя: 2960-lanbasek9-mz.150-2.SE4.bin

### Часть 2. Настройка базовых параметров сетевых устройств
#### Шаг 1. Настройте базовые параметры коммутатора

Так, ну теперь задачки я буду сразу объединять в блоки и соответственно на них отвечать.

*a.	В режиме глобальной конфигурации скопируйте следующие базовые параметры конфигурации и вставьте их в файл на коммутаторе S1. 
no ip domain-lookup
hostname S1
service password-encryption
enable secret class
banner motd #
Unauthorized access is strictly prohibited. #*

*b.	Назначьте IP-адрес интерфейсу SVI на коммутаторе. Благодаря этому вы получите возможность удаленного управления коммутатором.
Прежде чем вы сможете управлять коммутатором S1 удаленно с компьютера PC-A, коммутатору нужно назначить IP-адрес. Согласно конфигурации по умолчанию коммутатором можно управлять через VLAN 1.*

*c.	Доступ через порт консоли также следует ограничить  с помощью пароля. Используйте cisco в качестве пароля для входа в консоль в этом задании. Конфигурация по умолчанию разрешает все консольные подключения без пароля. Чтобы консольные сообщения не прерывали выполнение команд, используйте параметр logging synchronous.
S1(config)# line con 0
S1(config-line)# logging synchronous*

*d.	Настройте каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet. Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet.
Вопрос:
Для чего нужна команда login?*

**Мой ответ**

a)Для начала при помощи *configure terminal* переходим в режим глобальной конфигурации
*no ip domain-lookup* - отключили обращение к домену
*hostname S1* - установили имя коммутатору
*service password-encryption* - включаем шифрование паролей
*enable secret class* - устанавливаем пароль "class"
*banner motd #*
*Unauthorized access is strictly prohibited. #* -  устанавливаем баннер

b) Так, назначаем IP адрес интерфейсу SVI. У нас в начале ТЗ была таблица ( и в лекции также рассматривали). Опять идем в глобальную конфигурацию, а оттуда в конфигурацию интерфейста VLAN. Выглядит как то так: 

- S1(config)#interface Vlan 1
- S1(config-if)#ip address 192.168.1.2 255.255.255.0
- S1(config-if)#no shutdown
- Выходим наверх
- S1#copy running-config startup-config (и сохраняем все)

c)Теперь закрываем консольный порт от несанкционнированного доступа 
опять переходим в глобальный конфиг и подключаемся к консольному порту, а потом ставим пароль: 
- S1(config)#line console 0
- S1(config-line)#password cisco
- S1(config-line)#login (активируем пароль)

Также по заданию включаем синхронное логирование:
- S1(config-line)# logging synchronous

d) Теперь настраиваем канал виртуального соединения VTY. (сколько же повсюду доступов надо настроить)
Для этого снова идем в глобальный конфиг, там переходим на VTY 0 4 (как в лекции), устанавливаем пароль, запускаем его и записываем в память:

- S1#configure terminal
- Enter configuration commands, one per line.  End with CNTL/Z.
- S1(config)#line vty 0 4
- S1(config-line)#password class
- S1(config-line)#login
- S1(config-line)#end
- S1#
- %SYS-5-CONFIG_I: Configured from console by console
- S1#copy running-config startup-config
- Destination filename [startup-config]? 
- Building configuration...
- [OK]

Ответ на вопрос - для чего нужен login? Эта команда по сути включает саму проверку пароля на VTY. 

#### Шаг 2. Настройте IP-адрес на компьютере PC-A
*Назначьте компьютеру IP-адрес и маску подсети в соответствии с таблицей адресации.*

*1. Перейдите в Панель управления. (Control Panel)*

*2. В представлении «Категория» выберите « Просмотр состояния сети и задач».*

*3. Щелкните Изменение параметров адаптера на левой панели.*

*4. Щелкните правой кнопкой мыши интерфейс Ethernet и выберите «Свойства» .*

*5. Выберите Протокол Интернета версии 4 (TCP/IPv4) > Свойства.*

*6. Выберите Использовать следующий IP-адрес и введите IP-адрес и маску подсети  и нажмите ОК.*

**Мой ответ:**

Тут я больше двигался по лекции. Открыл настройки "IP Configuration" у ПК в схеме и вбил в IPv4 Address значение из начала ТЗ. В качестве проверки отключил консольный кабель и прослушал канал по команде: 
- ping 192.168.1.2 и подождал, пока пришел ответ, который говорит о том, что коннект есть между устройствами. Причем консольный кабель был убран. )


### Часть 3. Проверка сетевых подключений
#### Шаг 1. Отобразите конфигурацию коммутатора
*Используйте консольное подключение на компьютере PC-A для отображения и проверки конфигурации коммутатора. Команда show run позволяет постранично отобразить всю текущую конфигурацию. Для пролистывания используйте клавишу пробела.*

**Мой ответ:**
Поехали.) Смотрим при помощи команды *show running-config*. Все выводится, сравниваем с ТЗ. У меня в целом бьется, кроме строки *ip default-gateway 192.168.1.1* - её у меня нет. И VTY у меня настроен только на 0 4, а в примере - еще и на 5 15. 

Также есть еще и задача проверить параметры VLAN 1. Проверяем через show interface Vlan 1. Полоса пропусканя - 100 Мб/с.

#### Шаг 2. Протестируйте сквозное соединение, отправив эхо запрос. 
**мой ответ:**
Ну с PC я уже отправлял эхо на коммутатор. Но поехали по интрукции. 
Сперва проверяю через ping связь PC-A с адресом PC-A. (зачем, ведь он же сам себя получается опрашивает?) Связь есть
Потом опять из командной строки проверяю связь с коммутатором S1. Все работает.) А как иначе) 

#### Шаг 3. Проверьте удаленное управление коммутатором S1.

Тут все просто - через командную строку PC подклюился к маршрутизатору, ввел все пароли, полазил и сохраняем все настройки в нем командой *S1#copy running-config startup-config*. Завершаем сеанс.

### Вопросы для повторения
1.	Зачем необходимо настраивать пароль VTY для коммутатора?
2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде?

**Мой ответ:**
1. Что бы избежать есанкционнированного доступа;
2. Не использовать telnet, а использовать SSH. На крайний вариант - *service password-encryption*, что бы хоть как то жить безопаснее, если другого ничего нельзя. 







