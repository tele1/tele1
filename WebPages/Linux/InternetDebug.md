

# Diagnostyka internetu.

Problemy z połączeniem internetowym mogą się przyczynić
do nie prawidłowgo wyświetlenia treści w przeglądarce
lub błędach przy wysyłaniu danych, zdjęć, plików.


## 1. PING
```
# ping -c4 google.com
PING google.com (x.x.x.x) 56(84) bytes of data.
64 bytes from bud02s21-in-o.o.net (x.x.x.x): icmp_seq=1 ttl=54 time=41.4 ms
64 bytes from bud02s21-in-o.o.net (x.x.x.x): icmp_seq=2 ttl=54 time=41.6 ms
64 bytes from bud02s21-in-o.o.net (x.x.x.x): icmp_seq=3 ttl=54 time=41.6 ms
64 bytes from bud02s21-in-o.o.net (x.x.x.x): icmp_seq=4 ttl=54 time=41.9 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 41.418/41.670/41.919/0.229 ms
```

" 0% packet loss " sugeruje że połączenie odbyło się bez strat danych

Ping głównie przydaje się do sprawdzania DNS.
Jeśli
- nie mamy problemów z pingowaniem IP,
- a mamy problem z pingowaniem nazwy domeny
to znaczy że możemy mieć problem z DNS.

Ostrzeżenie:
Nie których adresów nie da się pingować, jest to celowe
zabezpieczenie przed atakami DDOS.

Inne narzedzia dla DNS to:   dig , nslookup , host


## 2. MTR
```
# mtr --report google.com
Start: Sat Jul 16 20:40:15 2016
HOST: home                        Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- ooooooooo.home             0.0%    10    0.5   0.5   0.4   0.5   0.0
  2.|-- xx.xx.xxx.xx               0.0%    10   18.0  17.9  17.5  18.0   0.0
  3.|-- xx.x.xxx.xxx               0.0%    10   18.0  18.3  17.9  18.7   0.0
  4.|-- WarsBoooRT02-oooooo.ineti  0.0%    10   23.9  22.6  21.1  23.9   0.8
  5.|-- xx.xxx.xxx.xx              0.0%    10   28.6  30.0  28.6  31.6   0.9
  6.|-- xx.xxx.xxx.xx              0.0%    10   31.3  30.9  29.4  32.5   0.7
  7.|-- lo67-cp.ooo.wooooooo.sint  0.0%    10   29.2  30.8  28.5  46.3   5.4
  8.|-- xx.xxx.xx.xx               0.0%    10   28.5  29.1  28.5  31.3   0.7
  9.|-- xx.xx.xxx.xx               0.0%    10   28.6  28.6  28.3  29.0   0.0
 10.|-- waw02s05-in-ooo.ooooo.net  0.0%    10   28.5  28.7  28.5  29.2   0.0  
```

Kolumna " Loss% " sugeruje również że przy każdym przystanku do serwera
google.com nie było strat danych.

Jeśli
- internet nam działa, wszystkie inne strony
- ale dana strona nie działa nam
- a strona działa normalnie z bramki proxy
to mtr może pomóc nam przypuszczać
który serwer jest za to winny.

Podobnym narzędziem  do mtr jest traceroute.


No dobra, załóżmy że mamy straty danych,
znamy "miejsce strat",
co robić ?
```
whois xx.xx.xxx.xx
```

- gdzie xx.xx.xxx.xx to jakieś IP

lub
```
whois nazwa
```

whois wyświetli nam pewne informacje jak np.
adres,  email lub nr. telefonu
gdzie możemy się spytać i spróbować zgłosić
problem z połączeniem z danym serwerem.


**Edytowane:**
 
Z przyczyn praktycznych chciałem dodać,
że "whois" komendę należy używać głównie z IP.
Ponieważ DNS nie musi wskazywać na właściciela.
Do właściciela jest przypisany adres IP
i kto jest właścicielem adresu IP może nam pokazać komenda "whois"
pod warunkiem, że dane są aktualne.

Przykład 1:
Trasa IP z komputera do liberainformatica.it
```
# mtr --report-wide --show-ips liberainformatica.it
Start: Sat Jan 13 13:40:40 2018
HOST: tee                                               
  1.|-- mój komputer                                        
  2.|-- Warsaw - Poland
  3.|-- Warsaw - Poland
  4.|-- Warsaw - Poland
  5.|-- Amsterdam - Netherlands
  6.|-- Amsterdam - Netherlands
  7.|-- Amsterdam - Netherlands
  8.|-- Amsterdam - Netherlands
  9.|-- Broomfield - United States
 10.|-- London - United Kingdom
 11.|-- Ponte San Pietro - Italy
 12.|-- Ponte San Pietro - Italy
 13.|-- Ponte San Pietro - Italy
```



Przykład 2:
Trasa DNS z komputera do liberainformatica.it
```
# mtr --report-wide --show-ips liberainformatica.it
Start: Sat Jan 13 13:40:40 2018
HOST: tee 
  1.|-- mój komputer                                        
  2.|-- Bonn - Germany
  3.|-- Bonn - Germany
  4.|-- Wien - Austria
  5.|-- Wien - Austria
  6.|-- Wien - Austria
  7.|-- Wien - Austria
  8.|-- IP --> Amsterdam - Netherlands
  9.|-- Broomfield - United States
 10.|-- Broomfield - United States
 11.|-- Bibbiena - Italy
 12.|-- Bibbiena - Italy
 13.|-- Bibbiena - Italy
```

I tak się złożyło że ostatnio liberainformatica.it miałem problem
ale "mtr" nie potrafiło ustalić problemów, ponieważ połączenie było,
ale bardzo niestabilne.

Jak dokonywać dokładniejsze analizy sieci, jeszcze nie wiem.
Ale znalazłem inną stronę która już wogóle nie działała
getfirebug.com
i w tym przypadku "mtr" wskazywał na problem z serwerem w Amsterdamie.

Po dwóch dniach, problem zniknął na obu serwisach,
co skłania mnie do podejrzeń, że problem dotyczył tego samego serwera pośredniczącego.


