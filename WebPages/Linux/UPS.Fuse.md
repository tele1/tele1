

# Kiedy nie ma oprogramowania do UPS-a jakiego byś chciał.



Natknąłem się na UPS PowerWalker który używa ViewPower oprogramowania.



Po uruchomieniu ViewPower wszystko co związane z UPS można przeglądać w przeglądarce internetowej ( tutaj potrzebna jest wtyczka flash player ).

Po uruchomieniu ViewPowerMini można to samo skonfigurować w okienku programu.





Niestety mam kilka problemów:
- aplikacje potrzebują uprawnień root,

$ ./ViewPowerMini
Experimental:  JNI_OnLoad called.
check_group_uucp(): error testing lock file creation Error details:Permission deniedcheck_lock_status: No permission to create lock file.
please see: How can I use Lock Files with rxtx? in INSTALL


 próbowałem dodać użytkownika do uucp grupy , a następnie 
 sg Nazwa_Grupy Nazwa_aplikacji
ale to nie działało. ( może robiłem to źle , nie wiem )
- przeglądarka, aplikacja są aplikacjami graficznymi,
więc mam wątpliwości czy będą działać w trybie tekstowym.
- narazie testowałem na Manjaro Linux i aplikacja jako tako działa bo się wyłącza, ale systemu już nie wyłączy.
- chciałem napisać własny skrypt, ale skąd wziąść dane ile % ma bateria w  UPS,
albo czy zasilanie jest z UPS-a ?  Nie wiem.


Szperając w interenecie najpierw znalazłem pomysł żeby pingować
własny router który jest przed UPS-em i w ten sposób będziemy wiedzieć czy w domu jest prąd. A potem komendę
arp -n 
Jest ona lepszym pomysłem niż ping, 
- bo nie musimy nic robić w zaporze internetowej, 
- odrazu nam mówi czy system ma połaczenie z siecią internetową.

Więc czas na skrypt:

```
#!/bin/bash


if [[ -z "$(arp -n)" ]] ; then
 echo "No power"
 sleep 70s
 if [[ -z "$(arp -n)" ]] ; then
  dt=`date '+%d-%m-%Y %H:%M:%S'`
  echo "$dt Shut down." | tee -a /var/log/UPS.log && shutdown -h now
 fi
 echo "Power back."
else
 echo "Connected."
fi
```

Skrypt sprawdzi czy jest jakiekolwiek połączenie internetowe,
jeśli nie ma, 
poczeka 70 sekund ( mniej więcej tyle czasu potrzebuje router by wstać i nawiązać kolejne połączenie )
a następnie jeszcze raz sprawdzi połączenie
i jeśli nie będzie zapisze te zdarzenie do logu i wyłączy komputer.
  jeśli natomiast będzie połączenie skrypt zakończy swoje działanie.



Teraz trzeba to jakoś dodać do cron-a aby skrypt sprawdzał co minutę,
czy system ma połączenie internetowe.
Bo założenie jest takie, że gdy mamy internet, to router jest zasilany
( oczywiście w domu trzeba mieć najpierw router )
A gdy zabraknie prądu, skrypt ma za zadanie wyłączyć komputer zanim rozładują się akumulatory w UPS.
A ponieważ nie wiem ile mają akumulatory napięcia to skrypt wyłączy system jak najszybciej jak się da.

Skrypt nazwałem sobie closesystem 
 a nastepnie przeniosłem do /usr/bin/ i zmieniłem uprawnienia
i zmieniłem właściciela.

użyte komendy:
mv closesystem /usr/bin/closesystem
chown root /usr/bin/closesystem
chmod 500 /usr/bin/closesystem

Kalkulator chmod:
http://www.chmod.pl/


Dodawanie do cron-a.
W terminalu :

```
export EDITOR=mousepad
```

gdzie mousepad to mój przykładowy edytor.

A następnie

```
crontab -e
```


i dopisujemy


```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
* * * * *        /usr/bin/closesystem
```

zapisujemy i gotowe, można testować, wyłączając router.


# Edit:
Udało mi się trochę więcej.
Może gdy znajdę kiedyś czas to napiszę więcej.
