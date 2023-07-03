## Part 1. Инструмент ipcalc

### 1.1 Сети и маски

### Адрес сети
![ipcalcadr](misc/images/ipcalcadr.png)
- Как показано на скриншоте, адрес сети: 110000000.10100111.00100110, а 00110110 - локальный адрес хоста.

### Маски сети
![ipcalcmask1](misc/images/ipcalcmask1.png)
- Для сетевой маски 255.255.255.0 префиксной формой будет 24, а бинарной - 11111111.11111111.11111111.00000000.

![ipcalcmask2](misc/images/ipcalcmask2.png)
- Для сетевой маски 15 "нормальной" формой будет 255.254.0.0, а бинарной - 11111111.11111110.00000000.00000000.

- Для сетевой маски 11111111.11111111.11111111.11110000 "нормальной" формой будет 255.255.240.0, а префиксной - 28.
(скриншот отсутствует, ибо в ipcalc невозможно задать значения в бинарной форме).

### Диапазон хостов
![ipcalchost1](misc/images/ipcalchost1.png)
- Минимальный и максимальный адрес хоста для адреса 12.167.38.4/8 выделен на скриншоте.

![ipcalchost2](misc/images/ipcalchost2.png)
- Минимальный и максимальный адрес хоста для адреса 12.167.38.4/16 выделен на скриншоте. (префиксная форма маски 11111111.11111111.00000000.00000000 - 16, так как состоит из 16 единиц).

![ipcalchost3](misc/images/ipcalchost3.png)
- Минимальный и максимальный адрес хоста для адреса 12.167.38.4/255.255.254.0 выделен на скриншоте.

![ipcalchost4](misc/images/ipcalchost4.png)
- Минимальный и максимальный адрес хоста для адреса 12.167.38.4/4 в очередной раз выделен на скриншоте.

### 1.2. localhost

Для взаимодействия с localhost посредством интерфейса loopback зарезервированы адреса 127.0.0.0 – 127.255.255.255.

![localhost1](misc/images/localhost1.png)
- Адрес 194.34.23.100 является публичным адресом и не является адресом loopback => невозможно обратиться к приложению, работающему на localhost. 

![localhost2](misc/images/localhost2.png)
- Адрес 127.0.0.2 лежит в диапазоне адресов loopback => можно обратиться к приложению, работающему на localhost.

![localhost3](misc/images/localhost3.png)
- Адрес 127.1.0.1 лежит в диапазоне адресов loopback => можно обратиться к приложению, работающему на localhost.

![localhost4](misc/images/localhost4.png)
- Адрес 128.0.0.1 является публичным адресом и не является адресом loopback => невозможно обратиться к приложению, работающему на localhost. 

### 1.3. Диапазоны и сегменты сетей

### Публичные и частные IP

Диапазоны частных IP: 10.0.0.0 – 10.255.255.255, 172.16.0.0 – 172.31.255.255, 192.168.0.0 – 192.168.255.255

![nettype1](misc/images/nettype1.png)
- Частный

![nettype2](misc/images/nettype2.png)
- Не частный и не lo => публичный

![nettype3](misc/images/nettype3.png)
- Частный

![nettype4](misc/images/nettype4.png)
- Частный

![nettype5](misc/images/nettype5.png)
- Не частный и не lo => публичный

![nettype6](misc/images/nettype6.png)
- Не частный и не lo => публичный

![nettype7](misc/images/nettype7.png)
- Не частный и не lo => публичный

![nettype8](misc/images/nettype8.png)
- Частный

![nettype9](misc/images/nettype9.png)
- Частный

![nettype10](misc/images/nettype10.png)
- Не частный и не lo => публичный

### IP шлюзов

![gatewayip](misc/images/gatewayip.png)
Диапазон возможных шлюзов для сети 10.10.0.0/18: 10.10.0.1 - 10.10.63.254 => Возможные IP шлюзов: 10.10.0.2, 10.10.1.255, 10.10.10.10. Адреса 10.0.0.1 и 10.10.100.1 не могут быть адресами шлюзов соответственно.

## Part 2. Статическая маршрутизация между двумя машинами

![interfaces](misc/images/interfaces.png)
- сетевые интерфейсы ws1 и ws2 соответственно.

![staticadr](misc/images/staticadr.png)
- статически задаем IP адреса и маски для ws1 и ws2 соответственно.

![netplan1](misc/images/netplan1.png)
- Применяем внесенные изменения.

### 2.1. Добавление статического маршрута вручную
![ipradd](misc/images/ipradd.png)
- добавляем статические маршруты от одной машины к другой и обратно.

![ping1](misc/images/ping1.png)
- пингуем соедиение между машинами.

### 2.2. Добавление статического маршрута с сохранением

![staticroute](misc/images/staticroute.png)
- Добавляем статический маршрут от одной машины до другой и обратно.

![netplan2](misc/images/netplan2.png)
- Применяем внесенные изменения.

![ping2](misc/images/ping2.png)
- пингуем соедиение между машинами.

## Part 3. Утилита iperf3

### 3.1. Скорость соединения

Перевод:
- 8 Mbps в 1 MB/s
- 100 MB/s в 800000 Kbps
- 1 Gbps в 1000 Mbps

### 3.2. Утилита iperf3

![iperf3](misc/images/iperf3.png)
- `iperf3 -s` запускает сервер. `iperf3 -c <server address>` в клиентском режиме обращается к серверу для измерения скорости передачи данных с сервера (при добавлении флага `-R` можно измерить скорость получения данных сервером).

## Part 4. Сетевой экран

### 4.1. Утилита iptables

![firewall](misc/images/firewall.png)
- /etc/firewall.sh на двух виртуальных машинах. `iptables` используется для работы с таблицами фильтрующих правил. `-F` и `-X` удаляют все существующие ранее цепочки правил. `-A` добавляет новое правило в конец указанной цепочки правил (INPUT/FORWARD/OUTPUT), `-I` мог бы добавлять в указанное место в цепочки (по умолчанию в начало). `-p` используется для указания протокола, на который будет распространяться правило. `-j` используется для указания цепочки или системного действия (ACCEPT/DROP/REJECT), которое будет применяться при соответствии правилу.

![chmod](misc/images/chmod.png)
- Даем права скрипту и применяем его. Машина не должна "пинговаться” => не должна давать ответ на запрос(пинг) => блокировка на OUTPUT.

![ping](misc/images/ping.png)
- На ws1 сначала применяется запрещающее правило, а затем разрешающее. Таким образом при пинге ws1 с ws2 выполнится запрещающее правило и пинг не пройдет, а до разрешающего правила пинг не дойдет, ибо полностью заблокируется первым правилом. На ws2 соответственно произойдет наоборот.

![nmap1](misc/images/nmap1.png)
- `nmap` c ws2 о ws1.

## Part 5. Статическая маршрутизация сети

![part5_network](misc/images/part5_network.png)
- Схема сети.

### Part 5.1. Настройка адресов машин

![wsyaml1](misc/images/wsyaml1.png)
- `.yaml` файлы на ws11, ws22, ws21 соответственно.

![ryaml1](misc/images/ryaml1.png)
- `.yaml` файлы на r1, r2 соответственно.

![wsip](misc/images/wsip.png)
- Проверка правильности заданных IP на ws11, ws22, ws21 соответственно.

![rip](misc/images/rip.png)
- Проверка правильности заданных IP на r1, r2 соответственно.

![wsping](misc/images/wsping.png)
- Пингуем ws22 с ws21 и r1 с ws11.

### Part 5.2. Включение переадресации IP-адресов

![sysctl](misc/images/sysctl.png)
- `sysctl -w net.ipv4.ip_forward=1` включение переадресации, применяемое только для запущенной сессии.

![sysctlconf](misc/images/sysctlconf.png)
- Изменяем `/etc/sysctl.conf`, чтобы переадресация происходила и в будущих сессиях. 

### Part 5.3. Установка маршрута по-умолчанию

![wsyaml1](misc/images/wsyaml1.png)
- Настраиваем маршрут по умолчанию для рабочих станций.

![wsipr](misc/images/wsipr.png)
- Убеждаемся в добавлении марщрута в таблицу маршрутизации.

![tcpdump1](misc/images/tcpdump1.png)
- Пингуем с ws11 роутер r2.

### Part 5.4. Добавление статических маршрутов

![ryaml2](misc/images/ryaml2.png)
- Добавляем статические маршруты в сеть с роутера.

![ripr](misc/images/ripr.png)
- Таблица с маршрутами на роутерах.

![iprlist](misc/images/iprlist.png)
- Вызов `ip r list` на ws11.

- Для адреса 10.10.0.0/18 был выбран не маршрут 0.0.0.0/0, потому что на 0.0.0.0/0 пакет отправляется только тогда, когда другой маршрут не задан явным образом в таблице маршрутизации хоста.

### Part 5.5. Построение списка маршрутизаторов

![traceroute](misc/images/traceroute.png)
- Вызов `traceroute` на ws11.

![tcpdump2](misc/images/tcpdump2.png)
- Менее подробный вызов `tcpdump -tn -i enp0s3`.

![tcpdump3](misc/images/tcpdump3.png)
- Нечитаемый, но подробный вызов `tcpdump -tnv -i enp0s3`.

- Утилита traceroute отправляет серию пакетов данных целевому узлу и каждый раз увеличивает значение поля TTL на 1. Первый пакет отправляется с TTL = 1, traceroute фиксирует адрес маршрутизатора, а также время между отправкой пакета и получением ответа. Они выводят на экран. Затем traceroute повторяет отправку пакета, но уже с TTL, равным 2, что позволяет первому маршрутизатору пропустить пакет дальше. Процесс повторяется до тех пор, пока при определённом значении TTL пакет не достигнет целевого узла.

### Part 5.6. Использование протокола ICMP при маршрутизации

![tcpdump4](misc/images/tcpdump4.png)
- Перехват трафика на r1 при помощи `tcpdump -n -i enp0s3 icmp`.

![ping3](misc/images/ping3.png)
- Пингуем несуществующий IP.

## Part 6. Динамическая настройка IP с помощью DHCP

![dhcpconf](misc/images/dhcpconf.png)
- Указываем адрес маршрутизатора по-умолчению, DNS-сервер и адрес внутренней сети на r2 в файле */etc/dhcp/dhcpd.conf*.

![resolvconf](misc/images/resolvconf.png)
- Прописываем `nameserver 8.8.8.8` в файле resolv.conf

![restartdhcp](misc/images/restartdhcp.png)
- Перезапускаем службу DHCP.

![ipar2](misc/images/ipar2.png)
- Перезагружаем машину ws21 и вызываем `ip a`.

![ping4](misc/images/ping4.png)
- Пингуем с ws22 ws21.

![yamlr1](misc/images/yamlr1.png)
- Указываем MAC адрес у ws11.

![dhcpconf1](misc/images/dhcpconf1.png)
![resolvconf1](misc/images/resolvconf1.png)
![restartdhcp1](misc/images/restartdhcp1.png)
- Настраиваем r1 аналогично r2, но с жесткой привязкой к MAC адресу(Отличия только в содеражнии */etc/dhcp/dhcpd.conf*).

![ipar1](misc/images/ipar1.png)
- Аналогичный тест с вызовом `ip a` на ws11.

- Запрашиваем обновление ip адреса с ws21:

![ipaws1](misc/images/ipaws1.png)
- `ip a` до обновления.

![ipaws2](misc/images/ipaws2.png)
- `ip a` после обновления.

- Для обновления пользуемся `sudo dchlient -r` и `sudo dchlient -v`.

## Part 7. NAT

- В файле */etc/apache2/ports.conf* на ws22 и r1 изменяем строку `Listen 80` на `Listen 0.0.0.0:80`, то есть делаем сервер Apache2 общедоступным.

![portsws22](misc/images/portsws22.png)
- */etc/apache2/ports.conf* на ws22.

![portsr1](misc/images/portsr1.png)
- */etc/apache2/ports.conf* на r1.

- Запускаем веб-сервер Apache командой `service apache2 start` на ws22 и r1.

![apachews22](misc/images/apachews22.png)
- `service apache2 start` на ws22.

![apacher1](misc/images/apacher1.png)
- `service apache2 start` на r1.

![firewall1](misc/images/firewall1.png)
- firewall на r1 аналогичный firewall из части 4.

![chmod1](misc/images/chmod1.png)
- Аналогично части 4 запускаем.

![ping5](misc/images/ping5.png)
- Проверяем соединение между ws22 и r1.

![firewall2](misc/images/firewall2.png)
- Дополняем firewall.

![ping6](misc/images/ping6.png)
- Снова проверяем соединение между ws22 и r1.

- Проверяем соединение по TCP для SNAT, для этого с ws22 подключяемся к серверу Apache на r1 командой: `telnet [адрес] [порт]`
![telnetws22r2](misc/images/telnetws22r2.png)
telnet ws22 -> r2

![telnetr1ws22](misc/images/telnetr1ws22.png)
telnet r1 -> ws22

## Part 8. Дополнительно. Знакомство с SSH Tunnels

- Запустим на r2 фаервол с правилами из Части 7
- Запустим веб-сервер Apache на ws22 только на localhost (то есть в файле /etc/apache2/ports.conf изменить строку Listen 80 на Listen localhost:80) 
![ports](misc/images/ports.png)

- Запустим веб-сервер Apache командой service apache2 start на ws22 и проверим командой `service apache2 status`
![apachestart](misc/images/apachestart.png)

- Воспользуемся Local TCP forwarding с ws21 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws21 
командой `ssh -L 8080:localhost:80 trunkslo@10.20.0.20)` 
![sshl](misc/images/sshl.png)

- Воспользуемся Remote TCP forwarding c ws11 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws11 командой
- `ssh -R 8080:localhost:80 trunkslo@10.20.0.20)`
![sshr](misc/images/sshr.png)

- Проверим, сработало ли подключение в обоих предыдущих пунктах, выполнив команду: `telnet 127.0.0.1 80`
![telnetws11](misc/images/telnetws11.png)
- ws11
![telnetws21](misc/images/telnetws21.png)
- ws21