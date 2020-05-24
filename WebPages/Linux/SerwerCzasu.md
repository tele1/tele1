

# openntpd - serwer czasu

**openntpd** - to program dzięki któremu możemy zsynchronizować czas według jakiegoś serwera czasu.


System na którym będziemy testować :
```
$ lsb_release -a
No LSB modules are available.
Distributor ID:    Debian
Description:    Debian GNU/Linux 9.1 (stretch)
Release:    9.1
Codename:    stretch
```

Pakiet :
openntpd  1:6.0p1-2~bpo80+1


Szukamy pliku konfiguracyjnego
```
# dpkg -L openntpd | grep etc
/etc
/etc/openntpd
/etc/openntpd/ntpd.conf
/etc/network
/etc/network/if-up.d
/etc/network/if-up.d/openntpd
/etc/default
/etc/default/openntpd
/etc/init.d
/etc/init.d/openntpd
```

/etc/openntpd/ntpd.conf to chyba będzie to.
 więc otwieramy sobie w ulubionym edytorze i konfigurujemy według potrzeb,

Do pomocy sobie weźmiemy przykładowe poradniki z sieci:
1. https://wiki.archlinux.org/index.php/OpenNTPD
2. http://jlk.fjfi.cvut.cz/arch/manpages/man/ntpd.conf.5

 

Oraz jak kto woli poszukać sobie innego niż domyślnego serwera
1. http://www.pool.ntp.org/zone/@

Ja sobie zostawie bez zmian czyli :
```
# $OpenBSD: ntpd.conf,v 1.3 2015/05/18 11:10:03 dtucker Exp $
# sample ntpd configuration file, see ntpd.conf(5)

# Addresses to listen on (ntpd does not listen by default)
#listen on *
#listen on 127.0.0.1
#listen on ::1

# sync to a single server
#server ntp.example.org

# use a random selection of NTP Pool Time Servers
# see http://support.ntp.org/bin/view/Servers/NTPPoolServers
#servers pool.ntp.org

# Choose servers announced from Debian NTP Pool
servers 0.debian.pool.ntp.org
servers 1.debian.pool.ntp.org
servers 2.debian.pool.ntp.org
servers 3.debian.pool.ntp.org

# use a specific local timedelta sensor (radio clock, etc)
#sensor nmea0

# use all detected timedelta sensors
#sensor *
```

Sprawdzamy usługę :
```
# systemctl status openntpd
● openntpd.service - OpenNTPd Network Time Protocol
   Loaded: loaded (/lib/systemd/system/openntpd.service; enabled; vendor preset:
   Active: active (running) ...
```

" active (running) " oznacza że działa.
 Według dokumentacji to pozwoli na synchronizację czasu przy starcie systemu.

Testujemy :
```
# ntpd -s -d
adjtimex returns frequency of 0.000000ppm
/var/lib/openntpd/db/ntpd.drift is empty
ntp engine ready
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
sendto: Operation not permitted
set local clock to Sat Sep  9 06:48:54 CEST 2017 (offset 0.000000s)
```

No własnie ... Nie ustawiliśmy zapory żeby przepuściła usługę.
Skonfiguruj sobie zapore internetową.

Ja tylko podam przykład dla iptables,
którą także należy sobie odpowiednio skonfigurować do własnych potrzeb i bezpieczeństwa.

Dodawanie reguł iptables :
```
# iptables -A INPUT -p udp --sport 123 -m conntrack --ctstate ESTABLISHED -j ACCEPT

# iptables -A OUTPUT -p udp --dport 123 -m conntrack --ctstate NEW -j ACCEPT
```




Aaa i sprawdzimy czy program nasłuchuje :
```
# netstat -tulp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
```
 


Nie.
To dobrze.  :-)


**Pobawmy się trochę  :D**

Sprawdzamy datę
```
# date
sob, 9 wrz 2017, 06:50:06 CEST
```

Zmieniamy
```
# date --set 21:08:00
sob, 9 wrz 2017, 21:08:00 CEST
```

Sprawdzamy
```
# date
sob, 9 wrz 2017, 21:08:06 CEST
```


Testujemy przywrócenie prawidłowej godziny poprzez synchronizację z serwerem czasu.

Łączymy się z serwerem.
```
# ntpd -s -d
adjtimex returns frequency of 0.000000ppm
/var/lib/openntpd/db/ntpd.drift is empty
ntp engine ready
reply from 194.177.4.1: offset -50672.705547 delay 0.027347, next query 8s
set local clock to Sat Sep&nbsp; 9 07:32:50 CEST 2017 (offset -50672.705547s)
reply from 194.177.4.2: negative delay -50672.676585s, next query 3271s
reply from 193.219.28.147: negative delay -50672.674477s, next query 3212s
reply from 217.182.76.134: negative delay -50672.672578s, next query 3211s
reply from 46.175.224.7: negative delay -50672.672052s, next query 3077s
reply from 46.21.221.122: negative delay -50672.667908s, next query 3220s
reply from 91.212.242.21: negative delay -50672.667079s, next query 3164s
reply from 89.174.70.2: negative delay -50672.665639s, next query 3009s
reply from 78.46.78.167: negative delay -50672.660182s, next query 3096s
reply from 176.9.1.211: negative delay -50672.659739s, next query 3259s
reply from 178.33.227.201: negative delay -50672.643456s, next query 3215s
reply from 131.234.137.64: negative delay -50672.640149s, next query 3177s
reply from 212.59.0.1: negative delay -50672.630555s, next query 3206s
reply from 45.33.84.208: negative delay -50672.578659s, next query 3206s
reply from 138.236.128.36: negative delay -50672.543421s, next query 3137s
reply from 66.85.74.226: negative delay -50672.536333s, next query 3085s
```

Przerywamy działanie aplikacji kombinacja klawiszy Ctrl + C

Sprawdzamy ponownię datę
```
# date
sob, 9 wrz 2017, 06:55:43 CEST
```



Działa !  :D

Jest tylko jedno ale.

Komenda "  date --set 21:08:00 "
zmieni tylko czas systemowy, to znaczy że po restarcie systemu czas ponownie wróci do czasu sprzętowego.


Czas systemowy
```
# date
sob, 9 wrz 2017, 06:08:27 CEST
```


Czas sprzętowy
```
# hwclock
2017-09-09 06:08:54.546403+0200
```



Zmiana czasu sprzętowego
```
# date --set 21:08:00
sob, 9 wrz 2017, 21:08:00 CEST
```


Sprawdzamy:
```
# date
sob, 9 wrz 2017, 21:08:08 CEST
# hwclock
2017-09-09 06:08:52.765144+0200
```



Synchronizacja czasu systemowego ze spzętowym
```
# hwclock --systohc --localtime
```

Jest to
```
# hwclock --help
-w, --systohc        ustawienie zegara sprzętowego wg czasu systemowego
    --localtime      zegar sprzętowy utrzymuje czas lokalny
```


Sprawdzamy
```
# date
sob, 9 wrz 2017, 21:09:46 CEST
# hwclock
2017-09-09 21:10:01.483887+0200
```





Jeżeli chcemy zrezygnowac z synchronizacji czasu można usunąć
pakiet openntpd oraz usunąć reguły iptables.


Usuwanie reguł iptables :
```
# iptables -D INPUT -p udp --sport 123 -m conntrack --ctstate ESTABLISHED -j ACCEPT

# iptables -D OUTPUT -p udp --dport 123 -m conntrack --ctstate NEW -j ACCEPT
```

```
Przypominam :
#  <-- komendy które uruchomełem jako root
$  <-- komendy uruchomione jako użytkownik
```
