## Шаг 1:
Построим сеть:
![](/IMAGES/Pasted_image_20260413161555.png)
*Устройства в сети (пока-что без соединений)*

Установим топологию согласно схеме:
![](/IMAGES/Pasted_image_20260413162417.png)
*Топология сети с подключенными устройствами*

---
## Шаг 2:
В каждом роутере создадим Сообщение дня в следующем формате:
"Работу выполнил(-а) %фио% студент(-а/-ки) группы %название%, в журнале под номером %число%!"

Роутер 1 (МОСКВА)
![](/IMAGES/Pasted_image_20260413171139.png)
*Настройка сообщения дня на rus-msk-r0*

Роутер 2 (МОСКВА)
![](/IMAGES/Pasted_image_20260413171259.png)
*Настройка сообщения дня на rus-msk-r1*

Роутер 3 (НОВОСИБИРСК)
![](/IMAGES/Pasted_image_20260413171332.png)
*Настройка сообщения дня на rus-nsk-r0*

Теперь при каждом запуске роутера будет видна следующая надпись:
![](/IMAGES/Pasted_image_20260413164403.png)
*Демонстрация сообщения дня на rus-msk-r0*

---
## Шаг 3:
Переименуем все устройства согласно данному шаблону:
Сокращённое название страны-Сокращённое название города-Сокращённая роль устройства с порядковым номером.

![](/IMAGES/Pasted_image_20260413164144.png)
*Итоговый внешний вид топологии сети*


---
## Шаг 4:
Раздадим доменные имена согласно тому, как мы их переименовали в "Шаг 3"

Коммутатор 1 (МОСКВА)
![](/IMAGES/Pasted_image_20260413165523.png)
*Переименование первого коммутатора в rus-msk-sw0*

Маршрутизатор 1 (МОСКВА)
![](/IMAGES/Pasted_image_20260413165614.png)
*Переименование первого маршрутизатора в rus-msk-r0*

Маршрутизатор 2 (МОСКВА)
![](/IMAGES/Pasted_image_20260413165727.png)
*Переименование второго маршрутизатора в rus-msk-r0*

МЛС (МОСКВА)
![](/IMAGES/Pasted_image_20260413165854.png)
*Переименование многоуровнего коммутатора в rus-msk-mls0*

Маршрутизатор 1 (НОВОСИБИРСК)
![](/IMAGES/Pasted_image_20260413170222.png)
*Переименование первого маршрутизатора в rus-nsk-r0*

Коммутатор 1 (НОВОСИБИРСК)
![](/IMAGES/Pasted_image_20260413170345.png)
*Переименование первого коммутатора в rus-nsk-sw0*

Коммутатор 2 (НОВОСИБИРСК)
![](/IMAGES/Pasted_image_20260413170431.png)
*Переименование второго коммутатора в rus-nsk-sw1*

---
## Шаг 5:
Создаём Vlan 2, 3 ,4 (не присваивая им имён) на коммутаторах в Новосибирске.

Коммутатор 1:
![](/IMAGES/Pasted_image_20260413172007.png)
*Создание Vlan 2-4 на rus-nks-sw0*

Коммутатор 2:
![](/IMAGES/Pasted_image_20260413174734.png)
*Создание Vlan 2-4 на rus-nsk-sw1*

---
## Шаг 6:
На коммутаторах в Новосибирске назначим интерфейс f0/2 VLAN 2, f0/3 VLAN 3, f0/4 VLAN 4.

Коммутатор 1:
![](/IMAGES/Pasted_image_20260413175429.png)
*Назначение соответствующих интерфейсов в соответствующие VLAN
на rus-nsk-sw0*

Коммутатор 2:
![](/IMAGES/Pasted_image_20260413175737.png)
*Назначение соответствующих интерфейсов в соответствующие VLAN
на rus-nsk-sw1

---
## Шаг 7:
Создадим канал EtherChannel 2-го уровня между коммутаторами в Новосибирске, используя интерфейсы G0/1 и G0/2, со следующими требованиями:
- Используем стандартный протокол для создания логической связи под номером 1.
- Убедимся, что коммутатор 1 (он же rus-nsk-sw0) является ответственным за инициирование согласование канала EtherChannel.
- Изменим интерфейс агрегированного канала на транковый на обоих коммутаторах.

Коммутатор 1:
![](/IMAGES/Pasted_image_20260413180819.png)
Настройка EtherChannel на rus-nsk-sw0*

Коммутатор 2:
![](/IMAGES/Pasted_image_20260413181128.png)
*Настройка EtherChannel на rus-nsk-sw1*

> Поправка 1:
>![](/IMAGES/Pasted_image_20260413183628.png)
>
>(изменены интерфейсы подключения, и Port-Channel заработал)
>
>![](/IMAGES/Pasted_image_20260413183713.png)
>*уведомление системы о том, что Port-Channel и порты G0/1, G0/2 теперь активны*

---
## Шаг 8:
Создадим Management Interface на SW0 коммутаторе (он же rus-nks-sw0) для VLAN 1, используя адрес 1.0.0.50/8 и шлюз по умолчанию установим 1.0.0.1.

![](/IMAGES/Pasted_image_20260413182155.png)
*Настройка для VLAN 1 на rus-nks-sw0*

---
## Шаг 9:
Создадим Management Interface на SW1 коммутаторе (он же rus-nks-sw1) для VLAN 2, используя адрес 2.0.0.50/8 и шлюз по умолчанию установим 2.0.0.1.

![](/IMAGES/Pasted_image_20260413182421.png)
*Настройка для VLAN 2 на rus-nsk-sw1*

---
## Шаг 10:
Включим SSHv2 на коммутаторах в Новосибирске, используя имя пользователя "nsk" и пароль типа 5 "cisco". Укажем их в отчете. Убедимся, что только SSH разрешен для удаленного подключения к обоим коммутаторам.
>username (логин): nsk
>password (пароль): cisco



Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415142624.png)
*Настройка SSHv2 на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1)
![](/IMAGES/Pasted_image_20260415143128.png)
*Настройка SSHv2 на rus-nks-sw1*

>Поправка 2 (!)
>вместо пароля типа 5 лучше использовать обычный пароль, который позже можно зашифровать (service password-encryption)
>![](/IMAGES/Pasted_image_20260415150450.png)
>*вариант настройки через обычный пароль с последующим шифрованием*


---
## Шаг 11:
Интерфейс f0/24 коммутатора SW0 будет подключен к маршрутизатору R1 для межсетевой маршрутизации VLAN на транке (на палке), поэтому убедимся, что он настроен как транк.

Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415150959.png)
*настройка межсетевой маршрутизации на f0/24 у rus-nsk-sw0*

---
## Шаг 12:
Настроим Сообщение дня (MOTD) для SW0 и SW1 со следующим сообщением: "Это %наименование коммутатора%". Сообщение должно отображаться пользователям при подключении через SSH или консоль

Коммутатор 1 (rus-nsk-sw0):
![](/IMAGES/Pasted_image_20260415151413.png)
*Настройка Сообщения дня на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1):
![](/IMAGES/Pasted_image_20260415151613.png)
*Настройка Сообщения дня на rus-nsk-sw1*

---
## Шаг 13:
Настроим порты f0/2-4 со следующими требованиями:
- Они должны переходить в состояние пересылки (forwarding) сразу после подключения к ним кабеля;
- Они не должны принимать фреймы BPDU;
- Отключите проприетарный протокол обнаружения Cisco (CDP);
- Убедимся, что трафик поступает только с одного MAC-адреса, который должен быть сохранен в коммутаторах даже после перезагрузки. И если происходит нарушение, то интерфейсы должны переходить в состояние err-disable

Коммутатор 1 (rus-nsk-sw0):
![](/IMAGES/Pasted_image_20260415160907.png)
*Настройка портов f0/2-4 согласно требованиям на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1):
![](/IMAGES/Pasted_image_20260415160629.png)
*Настройка портов f0/2-4 согласно требованиям на rus-nsk-sw1*

---
## Шаг 14:
Защита консоли тем же именем пользователя и паролем, что и в Шаге 10

Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415161132.png)
*Настройка защиты консоли на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1)
![](/IMAGES/Pasted_image_20260415161407.png)
*Настройка защиты консоли на rus-nsk-sw0*

---
## Шаг 15:
Отключим таймаут exec для консоли и SSH

Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415161824.png)
*Отключение exec-timeout в консоли и SSH на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1)
![](/IMAGES/Pasted_image_20260415161942.png)
*Отключение exec-timeout в консоли и SSH на rus-nsk-sw1

---
## Шаг 16:
Предотвратим прерывание консольной сессии каждым выводом журнала (логирования) (для консоли и SSH)

Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415162127.png)
*Отключение прерываний консоли на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1)
![](/IMAGES/Pasted_image_20260415162433.png)
*Отключение прерываний консоли на rus-nsk-sw1

---
## Шаг 17
Увеличим размер буфера истории для этой сессии до 256 строк (для консоли и SSH)

Коммутатор 1 (rus-nsk-sw0)
![](/IMAGES/Pasted_image_20260415162741.png)
*Увеличение размер буфера истории до 256 на rus-nsk-sw0*

Коммутатор 2 (rus-nsk-sw1)
![](/IMAGES/Pasted_image_20260415162816.png)
*Увеличение размер буфера истории до 256 на rus-nsk-sw0*

---
## Часть 2:
## Шаг 1:

Назначим интерфейсу f0/1 маршрутизатора R1 IP-адрес 40.40.40.1/24
![](/IMAGES/Pasted_image_20260415164147.png)
*Назначение IP-адреса интерфейсу*

---
## Шаг 2:
Настроим R1 (rus-nsk-r0) для поддержки маршрутизации между VLAN 1, 2, 3, 4 для SW1 и SW2, используя следующие требования:
- VLAN 1 IP-адрес R1 1.0.0.1.
- VLAN 2 IP-адрес R1 2.0.0.1.
- VLAN 3 IP-адрес R1 3.0.0.1.
- VLAN 4 IP-адрес R1 4.0.0.1.
![](/IMAGES/Pasted_image_20260415171925.png)
*Назначение IP-адресов на сабинтерфейс для VLAN 1*
![](/IMAGES/Pasted_image_20260415172004.png)
*Назначение IP-адресов на сабинтерфейс для VLAN 2
![](/IMAGES/Pasted_image_20260415172026.png)
*Назначение IP-адресов на сабинтерфейс для VLAN 3
![](/IMAGES/Pasted_image_20260415172052.png)
*Назначение IP-адресов на сабинтерфейс для VLAN 4

---
## Шаг 3:
Настройте R1 в качестве DHCP-сервера для любой машины, подключенной к VLAN 1, 2, 3, 4 на SWO и SW1, используя следующие требования:
- Для VLAN 1 диапазон IP-адресов DHCP на R1 будет от 1.0.0.100 до 1.0.0.200 не включительно.
- Для VLAN 2 диапазон IP-адресов DHCP на R1 будет от 2.0.0.100 до 2.0.0.200 не включительно.
- Для VLAN 3 диапазон IP-адресов DHCP на R1 будет от 3.0.0.100 до 3.0.0.200 не включительно.
- Для VLAN 4 диапазон IP-адресов DHCP на R1 будет от 4.0.0.100 до 4.0.0.200 не включительно.
Исключаем шлюзы и адреса до 100 и выше 200
![](/IMAGES/Pasted_image_20260415172526.png)
*исключение шлюзов и адресов до 100 и выше 200*

Создаём пулы для выдачи адресов
![](/IMAGES/Pasted_image_20260415172810.png)
*настройка пулов на rus-nsk-r0*

---
## Шаг 4:
Проверяем пингом связь с PC0 до 3.0.0.101 (он же PC5):
![](/IMAGES/Pasted_image_20260416152018.png)
_пинг с компьютера "0" на компьютер "5"_

---
## Часть 3:
## Шаг 1:
Выдадим имя хоста для MLS:
![](/IMAGES/Pasted_image_20260416162145.png)
*Переименование rus-msk-mls в MLS*

---
## Шаг 2:
Включим возможности маршрутизации на этом устройстве
![](/IMAGES/Pasted_image_20260416162533.png)
*Включение маршрутизации на MLS*

---
## Шаг 3:
Создадим VLAN 100 с именем Sales_dept и VLAN 200 с именем IT_dept
![](/IMAGES/Pasted_image_20260416162933.png)
*Создание VLAN'ов на MLS*

---
## Шаг 4:
Назначим нужные интерфейсы для созданных VLAN'ов
![](/IMAGES/Pasted_image_20260416163201.png)
*Назначение интерфейсов в VLAN-ы*

---
## Шаг 5:
Включим маршрутизацию между VLAN 100 и VLAN 200, используя SVI (Switch Virtual Interface)
![](/IMAGES/Pasted_image_20260416163701.png)
*Включение маршрутизации между VLAN'ами на MLS*

---
## Шаг 6:
Изменим интерфейсы f0/1-3 на интерфейсы 3-го уровня со следующими требованиями:
- IP-адрес f0/1: 11.0.0.50/8
- IP-адрес f0/2: 12.0.0.50/8
- IP-адрес f0/3: 40.40.40.50/24
![](/IMAGES/Pasted_image_20260416164415.png)
*Изменение интерфейсов с ?-го уровня до 3-го уровня*

---

## Шаг 7:
Пропингуем 200.0.0.50 с rus-msk-pc0
![](/IMAGES/Pasted_image_20260416173520.png)
*проверка*

---
## Часть 4:
## Шаг 1:
Настроим на московском R0 ip-адреса для f0/0-1
![](/IMAGES/Pasted_image_20260416174752.png)
*Настройка IP-адресов для f0/0 и f0/1*

## Шаг 2:
Настроим на московском R1 ip-адреса для f0/0-1
![](/IMAGES/Pasted_image_20260416175424.png)
*Настройка IP-адресов для f0/0 и f0/1*

## Шаг 3:
Настроим Cisco High availability по следующим критериям:
- Используем номер группы 1.
- Убедимся, что R2 является основным маршрутизатором, а R3 - резервным.
- R2 должен вытеснять (preempt) R3, когда он возвращается из нерабочего состояния.
- Виртуальный IP-адрес должен быть 10.0.0.1.
- R2 должен отслеживать свой интерфейс, подключенный к внешним сетям.
![](/IMAGES/Pasted_image_20260416180824.png)
*Настройка московского R0*

![](/IMAGES/Pasted_image_20260416181255.png)
*Настройка московского R1*

--------------------------------------------------------------------------------

ГАЛЯ ТУТ НАДО ВСЁ ВЕРНУТЬ
У НАС НЕ ПРАВИЛЬНО СОХРАНИЛСЯ ФАЙЛ
ПИШУ ОГРОМНЫМ СЛОЕМ ТЕКСТА ЧТОБЫ ТОЧНО ЗАМЕТИЛ
ыъы
ыъы
ыъы
ыъы
ыъы
-------------------------------------------------------------------------------------

---
## Часть 7:
## Шаг 1:
Создадим loopback-интерфейс 1 на маршрутизаторе R1 с определенным IP-адресом

![](/IMAGES/Pasted_image_20260421144232.png)

*Создание первого петлевого интерфейса на маршрутизаторе R1*

---
## Шаг 2:
Создадим loopback-интерфейс 3 на маршрутизаторе R3 с определенным IP-адресом

![](/IMAGES/Pasted_image_20260421144337.png)

*Создание третьего петлевого интерфейса на маршрутизаторе R3*


---
## Шаг 3:
Убеждаемся, что R1 и R3 объявляют эти петлевые интерфейсы друг другу, используя RIPv2

![](/IMAGES/Pasted_image_20260421144642.png)

*Включение протокола RIPv2 на R1*

![](/IMAGES/Pasted_image_20260421144819.png)

*Включение протокола RIPv2 на R3*

---
## Шаг 4:
Мы настроили протокол шагом выше

---
## Шаг 5:
Раздаём IP-адреса для маршрутизаторов (роутеров) 200.200.200.х/24

![](/IMAGES/Pasted_image_20260421151137.png)

*Создаем туннель на R1 и задаём к чему он идёт*

![](/IMAGES/Pasted_image_20260421151158.png)

*Включаем трансляцию для туннеля*

![](/IMAGES/Pasted_image_20260421151213.png)

*Включение нужного режима трансляции для туннеля*

![](/IMAGES/Pasted_image_20260421151933.png)

*Схожая настройка на маршрутизаторе R3*

---
## Шаг 6:
Используем расширенный пинг для проверки настройки

![](/IMAGES/Pasted_image_20260421152133.png)

*Создание правила для возможности пинга туннеля на роутере R1*

![](/IMAGES/Pasted_image_20260421152210.png)

*Создание правила для возможности пинга туннеля на роутере R3*

![](/IMAGES/Pasted_image_20260421153120.png)

*Прохождение пинга без особых проблем*

---
## Часть 8:
## Шаг 1:
Настраиваем маршрутизаторы и MLS на использование сервера 10.0.0.100 в качестве защищенного NTP-сервера, используя ключ 1 "cisco", и в качестве Syslog-сервера.

![](/IMAGES/Pasted_image_20260421161140.png)

*Настройка на rus-nsk-r0*

![](/IMAGES/Pasted_image_20260421162145.png)

*Настройка на rus-msk-r0*

![](/IMAGES/Pasted_image_20260421162454.png)

*Настройка на rus-msk-r1*

![](/IMAGES/Pasted_image_20260421162941.png)

*Настройка на LMS*

---
## Шаг 2:
 Включим SNMP на R2 и R3, используя пароль "cisco" для сообщений set и get.

![](/IMAGES/Pasted_image_20260421170109.png)

*Настройка snmp R2*

![](/IMAGES/Pasted_image_20260421170718.png)

*Настройка snmp R3*

---
## Шаг 3:
 Включим telnet на R3, используя сервер 10.0.0.100 в качестве АAA-сервера в качестве первого метода аутентификации, и в случае его недоступности R3 должен будет использовать локальное имя пользователя и пароль.


![](/IMAGES/Pasted_image_20260421171451.png)

*Конфигурация Telnet и Radius на R3*

---
## Шаг 4:
Настроим R2 на использование сервера 10.0.0.100 в качестве FTP-сервера, используя имя пользователя "cisco" и пароль "cisco".

![](/IMAGES/Pasted_image_20260421172721.png)

*Настройка R2 на использование сервера*

---
## Шаг 5:
Отправим копию текущей конфигурации R2 на сервер 10.0.0.100, используя протокол FTP.

![](/IMAGES/Pasted_image_20260421173205.png)

*Копирование конфигурации*

---
## Шаг 6:
Отправьте копию текущей конфигурации R3 на сервер 10.0.0.100, используя протокол TFTP подобно шагу 5

![](/IMAGES/Pasted_image_20260421173652.png)

---
## Шаг 7:
Убедимся, что мы не используем никаких команд boot system в R3.

Мы уверены🥀

---
## Шаг 8:
Убедитесь, что R2 может пинговать или подключаться к R3 по telnet, используя имя "standby"

![](/IMAGES/Pasted_image_20260421175055.png)

*Работает*

---

## ШАГ 9:
Изменим локальное имя пользователя в R3, используя процедуры восстановления пароля.

![](/IMAGES/Pasted_image_20260421175359.png)

*Выключили R3*

![](/IMAGES/Pasted_image_20260421175501.png)

*Включили R3 и вошли в ROMMON*

![](/IMAGES/Pasted_image_20260421175623.png)

*Сбросили до заводских*

![](/IMAGES/Pasted_image_20260421175823.png)

*Восстановили конфигурацию*

![](/IMAGES/Pasted_image_20260421175940.png)

*Изменить пароль и восстановить config-register*

![](/IMAGES/Pasted_image_20260421180129.png)

*Пароль установился при перезапуске*

---

```
SW1
enable
configure terminal
hostname rus-nsk-sw0
ip domain-name nsk.local
banner motd "Работу выполнили %КИА, ЕСС, АМП% студенты группы %9СА-321%, в журнале под номером %11, 9, 3%!"
vlan 2
vlan 3
vlan 4
exit
interface f0/2
switchport mode access
switchport access vlan 2
no shutdown
exit
interface f0/3
switchport mode access
switchport access vlan 3
no shutdown
exit
interface f0/4
switchport mode access
switchport access vlan 4
no shutdown
exit
interface range g0/1-2
channel-group 1 mode desirable
exit
interface port-channel 1
switchport mode trunk
switchport trunk allowed vlan all
exit
interface vlan 1
ip address 1.0.0.50 255.0.0.0
no shutdown
exit
ip default-gateway 1.0.0.1
username nsk secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
transport input ssh
login local
exec-timeout 0 0
exit
interface f0/24
switchport mode trunk
switchport trunk allowed vlan all
no shutdown
exit
banner motd ^CЭто SW0^C
interface range f0/2-4
spanning-tree portfast
spanning-tree bpduguard enable
no cdp enable
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
exit
line console 0
login local
exec-timeout 0 0
logging synchronous
history size 256
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
write memory
```

---

```
SW2
enable
configure terminal
hostname rus-nsk-sw1
ip domain-name nsk.local
banner motd "Работу выполнили %КИА, ЕСС, АМП% студенты группы %9СА-321%, в журнале под номером %11, 9, 3%!"
vlan 2
vlan 3
vlan 4
exit
interface f0/2
switchport mode access
switchport access vlan 2
no shutdown
exit
interface f0/3
switchport mode access
switchport access vlan 3
no shutdown
exit
interface f0/4
switchport mode access
switchport access vlan 4
no shutdown
exit
interface range g0/1-2
channel-group 1 mode desirable
exit
interface port-channel 1
switchport mode trunk
switchport trunk allowed vlan all
exit
interface vlan 2
ip address 2.0.0.50 255.0.0.0
no shutdown
exit
ip default-gateway 2.0.0.1
username nsk secret cisco
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
transport input ssh
login local
exec-timeout 0 0
exit
banner motd ^CЭто SW1^C
interface range f0/2-4
spanning-tree portfast
spanning-tree bpduguard enable
no cdp enable
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
exit
line console 0
login local
exec-timeout 0 0
logging synchronous
history size 256
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
write memory
```

```
R1
enable
configure terminal
hostname rus-msk-r1
ip domain-name msk.local
banner motd "Работу выполнили %КИА, ЕСС, АМП% студенты группы %9СА-321%, в журнале под номером %11, 9, 3%!"
interface f0/1
ip address 40.40.40.1 255.255.255.0
no shutdown
exit
interface f0/0
no shutdown
exit
interface f0/0.1
encapsulation dot1Q 1
ip address 1.0.0.1 255.0.0.0
exit
interface f0/0.2
encapsulation dot1Q 2
ip address 2.0.0.1 255.0.0.0
exit
interface f0/0.3
encapsulation dot1Q 3
ip address 3.0.0.1 255.0.0.0
exit
interface f0/0.4
encapsulation dot1Q 4
ip address 4.0.0.1 255.0.0.0
exit
ip dhcp excluded-address 1.0.0.1 1.0.0.99
ip dhcp excluded-address 1.0.0.201 1.0.0.255
ip dhcp pool VLAN1_POOL
network 1.0.0.0 255.0.0.0
default-router 1.0.0.1
exit
ip dhcp excluded-address 2.0.0.1 2.0.0.99
ip dhcp excluded-address 2.0.0.201 2.0.0.255
ip dhcp pool VLAN2_POOL
network 2.0.0.0 255.0.0.0
default-router 2.0.0.1
exit
ip dhcp excluded-address 3.0.0.1 3.0.0.99
ip dhcp excluded-address 3.0.0.201 3.0.0.255
ip dhcp pool VLAN3_POOL
network 3.0.0.0 255.0.0.0
default-router 3.0.0.1
exit
ip dhcp excluded-address 4.0.0.1 4.0.0.99
ip dhcp excluded-address 4.0.0.201 4.0.0.255
ip dhcp pool VLAN4_POOL
network 4.0.0.0 255.0.0.0
default-router 4.0.0.1
exit
access-list 101 permit tcp host 2.0.0.100 host 10.0.0.100 eq 80
access-list 101 deny tcp any host 10.0.0.100 eq 80
access-list 101 permit ip any any
interface f0/0.2
ip access-group 101 in
exit
interface loopback 1
ip address 192.168.101.1 255.255.255.0
exit
router rip
version 2
network 192.168.101.0
network 200.200.200.0
no auto-summary
exit
interface tunnel 0
ip address 200.200.200.1 255.255.255.0
tunnel source 40.40.40.1
tunnel destination 40.40.40.50
exit
router rip
network 200.200.200.0
exit
router eigrp 100
network 1.0.0.0
network 2.0.0.0
network 3.0.0.0
network 4.0.0.0
network 40.40.40.0
no auto-summary
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
write memory
```

---

```
R2
enable
configure terminal
hostname rus-msk-r2
ip domain-name msk.local
banner motd "Работу выполнили %КИА, ЕСС, АМП% студенты группы %9СА-321%, в журнале под номером %11, 9, 3%!"
interface f0/0
ip address 10.0.0.2 255.0.0.0
no shutdown
exit
interface f0/1
ip address 11.0.0.2 255.0.0.0
no shutdown
exit
interface f0/0
standby 1 ip 10.0.0.1
standby 1 priority 110
standby 1 preempt
standby 1 track f0/1 20
exit
router eigrp 100
network 10.0.0.0
network 11.0.0.0
no auto-summary
exit
access-list 102 deny icmp any any echo
access-list 102 permit ip any any
interface f0/0
ip access-group 102 in
exit
interface f0/1
ip access-group 102 in
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
snmp-server community cisco rw
snmp-server enable traps
exit
ip ftp username cisco
ip ftp password cisco
exit
copy running-config ftp:
write memory
```

---

```
R3
enable
configure terminal
hostname rus-msk-r3
ip domain-name msk.local
banner motd "Работу выполнили %КИА, ЕСС, АМП% студенты группы %9СА-321%, в журнале под номером %11, 9, 3%!"
interface f0/0
ip address 10.0.0.3 255.0.0.0
no shutdown
exit
interface f0/1
ip address 12.0.0.3 255.0.0.0
no shutdown
exit
interface f0/0
standby 1 ip 10.0.0.1
standby 1 priority 100
exit
router eigrp 100
network 10.0.0.0
network 12.0.0.0
no auto-summary
exit
access-list 102 deny icmp any any echo
access-list 102 permit ip any any
interface f0/0
ip access-group 102 in
exit
interface f0/1
ip access-group 102 in
exit
interface loopback 3
ip address 192.168.103.3 255.255.255.0
exit
router rip
version 2
network 192.168.103.0
network 200.200.200.0
no auto-summary
exit
interface tunnel 0
ip address 200.200.200.3 255.255.255.0
tunnel source 12.0.0.3
tunnel destination 12.0.0.50
exit
router rip
network 200.200.200.0
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
snmp-server community cisco rw
snmp-server enable traps
exit
aaa new-model
radius-server host 10.0.0.100 key cisco
aaa authentication login RADIUS_AUTH group radius local
username cisco secret cisco
line vty 0 4
login authentication RADIUS_AUTH
transport input telnet
exec-timeout 0 0
exit
exit
copy running-config tftp:
write memory
```

---

```
MLS
enable
configure terminal
hostname rus-msk-mls
ip domain-name msk.local
ip routing
vlan 100
name Sales_dept
exit
vlan 200
name IT_dept
exit
interface f0/4
switchport mode access
switchport access vlan 100
no shutdown
exit
interface f0/5
switchport mode access
switchport access vlan 200
no shutdown
exit
interface vlan 100
ip address 100.0.0.50 255.0.0.0
no shutdown
exit
interface vlan 200
ip address 200.0.0.50 255.255.255.0
no shutdown
exit
interface f0/1
no switchport
ip address 11.0.0.50 255.0.0.0
no shutdown
exit
interface f0/2
no switchport
ip address 12.0.0.50 255.0.0.0
no shutdown
exit
interface f0/3
no switchport
ip address 40.40.40.50 255.255.255.0
no shutdown
exit
router eigrp 100
network 11.0.0.0
network 12.0.0.0
network 40.40.40.0
network 100.0.0.0
network 200.0.0.0
no auto-summary
exit
ntp authenticate
ntp authentication-key 1 md5 cisco
ntp trusted-key 1
ntp server 10.0.0.100 key 1
ntp update-calendar
logging host 10.0.0.100
service timestamps log datetime msec
exit
write memory
```
