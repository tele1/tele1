

# Bash - wykonywanie poleceń z konta root bez uprawnień root / jako inny użytkownik.


Problem jest taki:

Piszemy sobie skrypt który będzie uruchamiany jako root
i chcemy uruchomić aplikacje bez uprawnień root.

Z pomocą nam przychodzi poradnik z wyszukiwarki
https://www.cyberciti.biz/open-source/command-line-hacks/linux-run-command-as-different-user/

W którym są wymienione:
```
"  #1: runuser "
"  #2: su "
"  #3: sudo "
```

Zacznę może od tyłu ...

**sudo**

Nie będę używał ponieważ nie jest to domyślne polecenie w systemie i czasami trzeba sobie doinstalować i skonfigurować.
    Generalnie jest to komenda używana tylko w Ubuntowych distrach.
Dlatego denerwuje mnie jak ktoś używa sudo w skryptach na każdą dystrybucje linuxa.
Poza tym nie wiem na ile to jest bezpieczne, może już  jest bezpieczne.
Pamiętam też dziwoląga " sudo su " , dla mnie używanie dwóch komend które robią prawie to samo to utrudnianie sobie życia.

**su**

Ta komenda jest dostępna w każdej dystrybucji linuxa
Bardzo prosta i przydatna przy logowaniu sie do root.
Pojawia się tylko problem gdy chcemy użyć w skrypcie w celu ograniczenia praw root.
Tutaj nie mogę podać jakiej aplikacji używałem ale przy testowaniu
```
 su tele -c 'aplikacja'
```

 otrzymywalem
```
# ls -la-rw-r--r-- 1 root root  256 sie 12 12:29 plik
```

Co nie było tym czego oczekiwałem.
Poza tym trzeba inne dawać nawiasy w skrypcie a inne w wierszu poleceń
przy testowaniu, co jest trochę kłopotliwe.

**runuser**
```
 runuser -l tele -c 'aplikacja'
```

Sprawdzam ...
```
# ls
 -la-rw-r--r-- 1 tele tele  256 sie 12 12:29 plik
```

I stworzylo taki plik jaki oczekiwalem :-)


No to czym to się różni od su ?
Znowu szperając w sieci można znaleść
https://superuser.com/questions/1062576/difference-between-su-c-and-runuser-l-c
i dalej idąc po sznurku
http://danwalsh.livejournal.com/55588.html

> runuser is actually built from the su.c source code.
...
Basically runuser is just the su command with the pam stack removed as well as verifying the command is running as root, not setuid. ...


Poprzez aplikacje chodzi mi o własny skrypt z własnymi komendami które chcemy uruchomić z poziomu root.
 Ponieważ z "su" mogę podać komendę ale łączenie więcej komend bywa problematyczne, dlatego najłatwiej zapisać wszystkie do skryptu i uruchamiać skrypt.

Natomiast sudo nie lubię, poniewaz domyślne w dystrybucjach linuxa jest "su" a nie "sudo".
Także jak ktoś chce, to żeby używac "sudo" czasami musi sobie pierw zainstalować i skonfigurować.

Poradnik leżał od dawna w poczekalni i może nie oddawać wszystkiego co miało tu się znaleść.


