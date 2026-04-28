# Часть 1:
## Шаг 1:
Построим сеть согласно схеме

![](/ThePhotos2/Pasted_image_20260422144207.png)

*Выставленные устройства по схеме*

---
## Шаг 2:
Настроим IP-адреса у роутера 1 по необходимым условиям

![](/ThePhotos2/Pasted_image_20260422144953.png)

*Выдача IP-адресов для R1*

---
## Шаг 3:
Настроим IP-адреса у роутера 2 по необходимым условиям

![](/ThePhotos2/Pasted_image_20260422145157.png)

*Выдача IP-адресов для R2*

---
## Шаг 4:
Настроим IP-адреса у роутера 3 по необходимым условиям

![](/ThePhotos2/Pasted_image_20260422145325.png)

*Выдача IP-адресов для loopback 3 на R3*

![](/ThePhotos2/Pasted_image_20260422145424.png)

*Выдача IP-адресов для loopback 33 на R3*

![](/ThePhotos2/Pasted_image_20260422145506.png)

*Выдача IP-адресов для Gigabit Ethernet на R3*

![](/ThePhotos2/Pasted_image_20260422145620.png)

*Выдача IP-адресов для serial на R3*

---
## Шаг 5:
Настроим IP-адреса у роутера 1973 по необходимым условиям

![](/ThePhotos2/Pasted_image_20260422145933.png)

*Выдача IP-адресов для serial на R1973*

![](/ThePhotos2/Pasted_image_20260422150030.png)

*Выдача IP-адресов для loopback на R1973*

---
# Часть 2:
## Шаг 1:
Настроим последовательные интерфейсы между R3 и R1973 с использованием инкапсуляции РРР. При необходимости поставим пароль

![](/ThePhotos2/Pasted_image_20260422151203.png)

*Установка инкапсуляции на R3*

![](/ThePhotos2/Pasted_image_20260422151327.png)

*Установка инкапсуляции на R1973*

---
# Часть 3:
## Шаг 1:
Настроим OSPFv2 протокол на роутерах 1-3

![](/ThePhotos2/Pasted_image_20260422152156.png)

*Настройка OSPFv2 на R1*

![](/ThePhotos2/Pasted_image_20260422152251.png)

*Настройка OSPFv2 на R2*

![](/ThePhotos2/Pasted_image_20260422152317.png)

*Настройка OSPFv2 на R3*

---
## Шаг 2:
Настроим роутер 2, чтобы он использовал ID роутера 0.0.0.2

![](/ThePhotos2/Pasted_image_20260422153450.png)

*Настройка ID роутера 2*

---
## Шаг 3:
Настроим роутеры 1-3 для объявления своих подключенных сетей в OSPF

![](/ThePhotos2/Pasted_image_20260422153748.png)

*Настройка объявлений для роутера 1*

![](/ThePhotos2/Pasted_image_20260422154139.png)

*Настройка объявлений для роутера 2*

![](/ThePhotos2/Pasted_image_20260422160126.png)

*Настройка объявлений для роутера 3*

---
## Шаг 4:
Используем ID процесса 100 для OSPF на роутерах 1-3

> Этот шаг мы выполнили выше в шаге 1

---
## Шаг 5 - 9:
Настроим нужные интерфейсы на определенных маршрутизаторах, чтобы они принадлежали своим зонам:

- f0/0 - R1 принадлежит зоне 1
- f0/1 (у нас f1/0) - R1 принадлежит зоне 0
- f0/0 - R2 принадлежит зоне 23
- f0/1 (у нас f1/0) - R2 принадлежит зоне 0
- f0/0 - loopback 3 и 33 у R3 принадлежит зоне 23

> Эти шаги мы выполнили выше в шаге 3

---
## Шаг 10:
Заблокируем отправку hello-пакетов OSPF на всех интерфейсах роутера 1, кроме интерфейса f1/0

![](/ThePhotos2/Pasted_image_20260423145309.png)

*Блокирование отправки hello-пакетов у роутера 1*

---
## Шаг 11:
Настроим R2 так, чтобы он всегда был назначенным роутером на всех многодоступовых сетях.

![](/ThePhotos2/Pasted_image_20260422163747.png)

*Изменение роутера 2 в назначенный роутер*

---
## Шаг 12:
Настроим R3 так, чтобы он работал в качестве шлюза по умолчанию для всех роутеров OSPF, чтобы они могли взаимодействовать с любыми другими сетями.

![](/ThePhotos2/Pasted_image_20260422164512.png)

*Настройка роутера 3 как шлюз по умолчанию*

---
# Часть 4:
## Шаг 1:
Настроим BGP между роутером 3 и 1973

![](/ThePhotos2/Pasted_image_20260422170550.png)

*Настройка BGP на роутере 3*

![](/ThePhotos2/Pasted_image_20260422170903.png)

*Настройка BGP на роутере 1973*

---
## Шаг 2 - 6:

- Укажем, что все роутеры, использующие протокол OSPF, находятся в автономной системе BGP (AS) номер 3

- Роутер R1973 находится в автономной системе BGP (AS) номер 1973

- Настроим роутер R3 для установления внешнего BGP-соседства с роутером R1973.

- Настроим роутер R1973 так, чтобы он объявил свой loopback-интерфейс роутер R3.

- Настроим роутер R1973 так, чтобы маршрут по умолчанию указывал на роутер R3.

> Все эти шаги мы сделали выше в шаге 1

![](/ThePhotos2/Pasted_image_20260422171346.png)

*Настройка шлюза роутера 1973*

---
# Часть 5:
## Шаг 1:

Мы абсолютно точно и безоговорочно уверены в том, что у нас всё поддерживается.

---
## Шаг 2:
Установим лицензию uck9

![](/ThePhotos2/Pasted_image_20260423163856.png)

*Установка модуля лицензии UCK9*

---
## Шаг 3:
Установим лицензию securityk9

![](/ThePhotos2/Pasted_image_20260423164410.png)

*Установка модуля лицензии securityk9*

---
## Шаг 4:
Сохраним конфигурацию

![](/ThePhotos2/Pasted_image_20260423164547.png)

*Сохранение конфигурации*

---
## Шаг 5:
Перезагрузим маршрутизатор

![](/ThePhotos2/Pasted_image_20260423164706.png)

*Перезагрузка маршрутизатора R3*

![](/ThePhotos2/Pasted_image_20260423164750.png)

*Так выглядит успешная установка лицензий после перезагрузки*

---
# Часть 6:
## Шаг 1:
Нужно настроить роутер 1 как DHCP-ретранслятор

Сначала установим статический IP-адрес на сервер (DHCP-server)

![](/ThePhotos2/Pasted_image_20260423170006.png)

*Установка статического IP-адреса на DHCP-сервере*

Далее нужно настроить сам пул адресов на DHCP-сервере

![](/ThePhotos2/Pasted_image_20260423170324.png)

*Настройка нового пула IP-адресов*

Теперь настроим R1 как DHCP-ретранслятор адресов

![](/ThePhotos2/Pasted_image_20260423170529.png)

*Настройка ретрансляции DHCP адресов*

---
## Шаг 2:
Проверим получение IP-адреса компьютером PC0

![](/ThePhotos2/Pasted_image_20260423170822.png)

*Успешное получение DHCP-адреса компьютером PC0*

---
# Часть 7:
## Шаг 1 - 4:
Настроим роутеры 1-1973 с IPv6-адресами

R1:
• f0/0:
* Link-local адрес: fe80::1
* Глобальный адрес: сгенерируйте EUI-64 адрес для префикса 2001:10:10:10::/64 с помощью команды
• f0/1:
* Глобальный адрес: 2001:11:11:11::1/64

R2:
• f0/0:
* Глобальный адрес: 2001:12:12:12::2/64
• f0/1:
* Глобальный адрес: 2001:11:11:11::2/64

R3:
• g0/0:
* Глобальный адрес: 2001:12:12:12::3/64
• s0/0/0:
* Глобальный адрес: 2001:30:30:30::3/64

R1973:
• Loopback3:
* Глобальный адрес: 2001:1973:1973:1973::1973/64
• f0/0:
* Глобальный адрес: 2001:30:30:30::1973/64

![](/ThePhotos2/Pasted_image_20260424162920.png)

*Настройка IPv6 на R1 (на f0/0 используя eui-64)*
>Поправка: ipv6 на другом интерфейсе был создан обычным путем (без eui-64)

![](/ThePhotos2/Pasted_image_20260424163043.png)

*Настройка IPv6 на R2*
>Поправка: ipv6 были создан обычным путем (без eui-64)

![](/ThePhotos2/Pasted_image_20260424163823.png)

*Настройка IPv6 на R3*

![](/ThePhotos2/Pasted_image_20260424164613.png)

*Настройка IPv6 на R1973*

---
# Часть 8:
## Шаг 1:
Настроим OSPFv3 на роутерах 1-3

![](/ThePhotos2/Pasted_image_20260424165740.png)

*R1 настройка router-id*

![](/ThePhotos2/Pasted_image_20260424170757.png)

*R2 настройка router-id*

![](/ThePhotos2/Pasted_image_20260424171130.png)

*R3 настройка router-id*

---
## Шаг 2-9:
Настроим весь OSPFv3 на роутерах 1-3

![](/ThePhotos2/Pasted_image_20260424170338.png)

*Настройка OSPFv3 роутера 1*

![](/ThePhotos2/Pasted_image_20260424171500.png)

*Настройка OSPFv3 роутера 2*

![](/ThePhotos2/Pasted_image_20260424171822.png)

*Настройка OSPFv3 роутера 3*

---
# Часть 9:
## Шаг 1 - 3:
Настроим EIGRPv6 между роутерами 3 и 1973, а именно: установим номер автономной системы "100" и установим router-id

![](/ThePhotos2/Pasted_image_20260424173243.png)

*Настройка EIGRPv6 на R3*

![](/ThePhotos2/Pasted_image_20260424173250.png)

*Настройка EIGRPv6 на R1973*

---
## Шаг 4 - 5:
Объявим свою петлевую сеть для роутера 3 и настроим маршрут по умолчанию на роутере 1973

![](/ThePhotos2/Pasted_image_20260427145216.png)

*Объявляем петлевую сеть роутер 3*

![](/ThePhotos2/Pasted_image_20260427145848.png)

*Настройка маршрута по умолчанию на роутере 1973*

---

Блоки кода для устройств:

```
R1
!
version 12.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 10.1.1.1 255.255.255.0
 ip helper-address 10.23.23.100
 ip ospf priority 255
 duplex auto
 speed auto
 ipv6 address FE80::1 link-local
 ipv6 address 2001:10:10:10::/64 eui-64
 ipv6 ospf 100 area 1
!
interface FastEthernet0/1
 ip address 10.12.12.1 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:11:11:11::1/64
 ipv6 ospf 100 area 0
!
interface Serial0/0/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/0/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface FastEthernet1/0
 switchport mode access
!
interface FastEthernet1/1
 switchport mode access
 shutdown
!
interface FastEthernet1/2
 switchport mode access
 shutdown
!
interface FastEthernet1/3
 switchport mode access
 shutdown
!
interface FastEthernet1/4
 switchport mode access
 shutdown
!
interface FastEthernet1/5
 switchport mode access
 shutdown
!
interface FastEthernet1/6
 switchport mode access
 shutdown
!
interface FastEthernet1/7
 switchport mode access
 shutdown
!
interface FastEthernet1/8
 switchport mode access
 shutdown
!
interface FastEthernet1/9
 switchport mode access
 shutdown
!
interface FastEthernet1/10
 switchport mode access
 shutdown
!
interface FastEthernet1/11
 switchport mode access
 shutdown
!
interface FastEthernet1/12
 switchport mode access
 shutdown
!
interface FastEthernet1/13
 switchport mode access
 shutdown
!
interface FastEthernet1/14
 switchport mode access
 shutdown
!
interface FastEthernet1/15
 switchport mode access
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 100
 log-adjacency-changes
 passive-interface default
 no passive-interface FastEthernet0/1
 network 10.1.1.0 0.0.0.255 area 1
 network 10.12.12.0 0.0.0.255 area 0
!
ipv6 router ospf 100
 router-id 0.0.0.1
 log-adjacency-changes
 passive-interface default
 no passive-interface FastEthernet0/1
!
ip classless
!
ip flow-export version 9
!
!
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end
```

---

```
R2
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R2
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
license udi pid CISCO2811/K9 sn FTX1017GI43-
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 10.23.23.2 255.255.255.0
 ip helper-address 10.23.23.100
 ip ospf priority 255
 duplex auto
 speed auto
 ipv6 address 2001:12:12:12::2/64
 ipv6 ospf 100 area 23
!
interface FastEthernet0/1
 ip address 10.12.12.2 255.255.255.0
 ip ospf priority 255
 duplex auto
 speed auto
 ipv6 address 2001:11:11:11::2/64
 ipv6 ospf 100 area 0
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 100
 router-id 0.0.0.2
 log-adjacency-changes
 network 10.12.12.0 0.0.0.255 area 0
 network 10.23.23.0 0.0.0.255 area 23
!
router rip
!
ipv6 router ospf 100
 router-id 0.0.0.2
 log-adjacency-changes
!
ip classless
!
ip flow-export version 9
!
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end
```

---

```
R3
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R3
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
username R1973 password 0 CiscoCHAP
!
!
license udi pid CISCO2911/K9 sn FTX152465XI-
license boot module c2900 technology-package uck9
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface Loopback3
 ip address 3.3.3.3 255.0.0.0
!
interface Loopback33
 ip address 33.33.33.33 255.0.0.0
!
interface GigabitEthernet0/0
 ip address 10.23.23.3 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:12:12:12::3/64
 ipv6 ospf 100 area 23
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/0/0
 no ip address
!
interface Serial0/1/0
 ip address 30.30.30.3 255.255.255.0
 encapsulation ppp
 ppp authentication chap
 ipv6 address 2001:30:30:30::3/64
 ipv6 eigrp 100
 clock rate 2000000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
!
interface Vlan1
 no ip address
!
router ospf 100
 log-adjacency-changes
 network 10.23.23.0 0.0.0.255 area 23
 network 3.3.3.0 0.0.0.255 area 23
 network 33.33.33.0 0.0.0.255 area 23
 default-information originate
!
router bgp 3
 bgp router-id 3.3.3.3
 bgp log-neighbor-changes
 no synchronization
 neighbor 30.30.30.73 remote-as 1973
 network 10.23.23.0 mask 255.255.255.0
 network 3.0.0.0
 network 33.0.0.0
!
ipv6 router ospf 100
 router-id 0.0.0.3
 default-information originate
 log-adjacency-changes
!
ipv6 router eigrp 100
 eigrp router-id 0.0.0.3
 shutdown 
!
ip classless
ip route 0.0.0.0 0.0.0.0 Loopback3 
!
ip flow-export version 9
!
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end
```

---

```
R1973
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1973
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
username R3 password 0 CiscoCHAP
!
!
license udi pid CISCO2911/K9 sn FTX15242629-
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface Loopback3
 no ip address
 shutdown
!
interface Loopback1973
 ip address 73.73.73.73 255.255.255.0
 ipv6 address 2001:1973:1973:1973::1973/64
 ipv6 eigrp 100
!
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:30:30:30::1973/64
 shutdown
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/0
 no ip address
 shutdown
!
interface Serial0/1/0
 ip address 30.30.30.73 255.255.255.0
 encapsulation ppp
 ppp authentication chap
 ipv6 eigrp 100
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router bgp 1973
 bgp log-neighbor-changes
 no synchronization
 neighbor 30.30.30.3 remote-as 3
 network 73.73.73.0 mask 255.255.255.0
!
ipv6 router eigrp 100
 eigrp router-id 0.0.0.73
 shutdown 
!
ip classless
ip route 0.0.0.0 0.0.0.0 30.30.30.3 
!
ip flow-export version 9
!
ipv6 route ::/0 2001:30:30::3
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end
```
