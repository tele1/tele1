
 
# Jak skompilować i zainstalować nowszy yad w Debianie.

 *Czyli znowu coś nie działa...*

Posiadam  "Debian GNU/Linux 9 (stretch)"
i normalnie bym włączyłbym repozytorium

> http://ftp.pl.debian.org/debian/  buster non-free main contrib

w menadżerze pakietów Synaptic
i zainstalował odpowiednio nowszy pakiet yad.

Problem w tym że tam jest aktualnie stary jakiś yad
i w dodatku nie działa tak jak powinien.
A na tu https://sourceforge.net/projects/yad-dialog/
mam aktualniejszy.


------------

**I tu parę wyjaśnień.**
- Lubię mieć programy w /home/użytkownik/bin
Ale jest problem ...
ponieważ każdy plik w katalogu domowym ~/
możemy dowolnie zmodyfikować. Nawet nieświadomie uruchamiając jakiś skrypt.
- W związku z tym pomyślałem , a może zainstalować domyślnie ?
( /usr/bin/ ) . I tu także pojawił się problem

```
# dpkg -i yad_0.40.0-1_amd64.deb
...
Rozpakowywanie pakietu yad (0.40.0-1) ...
dpkg: błąd przetwarzania archiwum yad_0.40.0-1_amd64.deb (--install):
 próba nadpisania "/usr/share/icons/hicolor/icon-theme.cache", który istnieje także w pakiecie gtkdialog 0.8.4-1
Przetwarzanie wyzwalaczy pakietu hicolor-icon-theme (0.15-1)...
Wystąpiły błędy podczas przetwarzania:
 yad_0.40.0-1_amd64.deb
```

- Żeby nie usuwac pliku, postanowiłem spróbować zainstalować do /opt
W założeniu cała aplikacja yad będzie się mieścić w katalogu /opt/yad/
I tu także pojawił się problem

```
$ yad
command not found

$ /opt/yad/yad
app running
```

To że możeszmy uruchomić komendę bez podania ścieżki odpowiada zmienna środowiskowa $PATH która jest zczytywana z
/etc/profile lub ostatecznie z ~/.profile

Problem w tym, że 
1. nie ma tam ścieżki /opt
```
...
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
fi
export PATH
...
```


2. zwykły użytkownik wcale nie używa pliku /etc/profile
```
$ cat /etc/X11/default-display-manager
/usr/sbin/lightdm
```

Używam lightdm jako menadżera logownia.
Wygląda na to że lightdm nadpisuje zmienną $PATH na własną.
A ponieważ zmienna siedzi pewnie w pliku binarnym, to nie będę tego edytował.
- Więc zrobiłem coś podobnie złego jak zrobił to lightdm,
 czyli teraz ja jemu podmieniłem trochę zmienną $PATH
wykorzystując plik ~/.bashrc który musi załadować. 
Taka metoda z oczywistych względów będzie skuteczna tylko dla użytkownika któremu edytowaliśmy  ~/.bashrc , jeśli dla innych użytkowników także potrzebujesz to możesz spróbować podmienić ~/.bashrc w /etc/skel/ i przy tworzeniu nowych użytkowników każdy z nich już dostanie ten podmieniony plik. Tylko ostrzegam po raz drugi że to niewłaściwa droga i korzystam z niej tylko w ostateczności. 

O tyle dobrze, że chociaż  $PATH dla root pochodzi z /etc/profile

Czy kiedy kolwiek developerzy usuną $PATH z lightdm ?
Nie wiem,
po wątkach w internecie i tym że kiedyś próbowałem zwrócić uwagę na ten problem, narazie nie widzę zmian.

------------

No to zaczynamy ...

1. Pobieramy aktualny i stabilny kod źródłowy yad z sourceforge.
https://sourceforge.net/projects/yad-dialog/


2. Tworzymy katalogi gdzie będzie zainstalowana aplikacja.
Ponieważ aplikacja domyślnie nie tworzy wszystkich katalogów przy instalacji ..
Przykład błędu:

```
$ checkinstall --install=no --maintainer=tele --pkgname=yad --pkgversion=0.40.0 --pkglicense="GPL v.3" --provides=yad --nodoc
...
 /bin/mkdir -p '/opt/yad/icons/hicolor/16x16/apps'
/bin/mkdir: nie można utworzyć katalogu „/opt/yad/icons”: Nie ma takiego pliku ani katalogu


To trzeba je stworzyć ręcznie.

$ su -c 'mkdir -p /opt/yad/icons/hicolor/{16x16,24x24,32x32,48x48,96x96,128x128}/apps'
$ su -c 'mkdir -p /opt/yad/man/man1'
```


3. Rozpakowujemy pobrany kod źródłowy yad.


4. Tworzymy katalog gdzie będziemy kompilować
Wejdz  do rozpakowanego kodu źródłowego i stwórz katalog BUILD
```
$ mkdir BUILD
$ cd BUILD/
```


5. Sprawdzamy zależności i konfigurujemy cel instalacji ( /opt/yad )
```
$ ../configure --bindir=/opt/yad --libdir=/opt/yad --datarootdir=/opt/yad
```

Oczywiście opcje wziełem z
```
$ ../configure --help

...

  --bindir=DIR            user executables [EPREFIX/bin]
  --libdir=DIR            object code libraries [EPREFIX/lib]
  --datarootdir=DIR       read-only arch.-independent data root [PREFIX/share]
```

Tak wygląda koniec wykonania skryptu configure
```
config.status: creating data/icons/96x96/Makefile
config.status: creating data/icons/128x128/Makefile
config.status: creating data/yad.m4
config.status: creating data/yad.spec
config.status: creating config.h
config.status: config.h is unchanged
config.status: executing depfiles commands
config.status: executing default-1 commands
config.status: executing po/stamp-it commands

Build configuratioh:
  GTK+ version         - gtk2
  Path to rgb.txt      - /etc/X11/rgb.txt
  HTML widget          - no
  Spell checking       - no
  GtkSourceView        - no
  GIO support          - yes
  Icon browser         - no
```


6. Kompilujemy yad.
```
$ make
```

Tak wygląda koniec kompilacji
```
make[4]: Nie ma nic do zrobienia w 'all-am'.
make[4]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD/data/icons'
make[3]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD/data/icons'
make[3]: Wejście do katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD/data'
make[3]: Nie ma nic do zrobienia w 'all-am'.
make[3]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD/data'
make[2]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD/data'
make[2]: Wejście do katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD'
make[2]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD'
make[1]: Opuszczenie katalogu '/home/tele/Pulpit/test/PACZKI/yad-0.40.0/BUILD'
```


7. Tworzymy pakiet .deb
```
$ checkinstall --install=no --maintainer=tele --pkgname=yad --pkgversion=0.40.0 --pkglicense="GPL v.3" --provides=yad --nodoc
```

Opcje wziełem np. z tąd
https://manpages.debian.org/stretch/checkinstall/checkinstall.8.en.html
chociaż opcja  **--help** i **man** także twoim przyjacielem.

Po wykonaniu komendy zobaczysz coś takiego
```
This package will be built according to these values: 

0 -  Maintainer: [ tele ]
1 -  Summary: [ Tool for create graphical dialogs from shell scripts. ]
2 -  Name:    [ yad ]
3 -  Version: [ 0.40.0 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL v.3 ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ amd64 ]
8 -  Source location: [ BUILD ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Provides: [ yad ]
12 - Conflicts: [  ]
13 - Replaces: [  ]

Enter a number to change any of them or press ENTER to continue: 
```

Zmień wartości jeśli potrzebujesz.


8. Sprawdźmy pakiet .deb
```
$ dpkg -c *.deb
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/aclocal/
-rw-r--r-- tele/tele      1154 2017-12-13 15:50 ./opt/yad/aclocal/yad.m4
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/128x128/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/128x128/apps/
-rw-r--r-- tele/tele     18809 2017-12-13 15:50 ./opt/yad/icons/hicolor/128x128/apps/yad.png
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/16x16/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/16x16/apps/
-rw-r--r-- tele/tele       908 2017-12-13 15:50 ./opt/yad/icons/hicolor/16x16/apps/yad.png
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/24x24/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/24x24/apps/
-rw-r--r-- tele/tele      1282 2017-12-13 15:50 ./opt/yad/icons/hicolor/24x24/apps/yad.png
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/32x32/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/32x32/apps/
-rw-r--r-- tele/tele      2132 2017-12-13 15:50 ./opt/yad/icons/hicolor/32x32/apps/yad.png
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/48x48/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/48x48/apps/
-rw-r--r-- tele/tele      3835 2017-12-13 15:50 ./opt/yad/icons/hicolor/48x48/apps/yad.png
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/96x96/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/icons/hicolor/96x96/apps/
-rw-r--r-- tele/tele     12091 2017-12-13 15:50 ./opt/yad/icons/hicolor/96x96/apps/yad.png
-rw-r--r-- tele/tele       232 2017-12-13 15:50 ./opt/yad/icons/hicolor/icon-theme.cache
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/de/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/de/LC_MESSAGES/
-rw-r--r-- tele/tele      8353 2017-12-13 15:50 ./opt/yad/locale/de/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/fr/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/fr/LC_MESSAGES/
-rw-r--r-- tele/tele     20844 2017-12-13 15:50 ./opt/yad/locale/fr/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/it/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/it/LC_MESSAGES/
-rw-r--r-- tele/tele     24799 2017-12-13 15:50 ./opt/yad/locale/it/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/pt_BR/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/pt_BR/LC_MESSAGES/
-rw-r--r-- tele/tele     32355 2017-12-13 15:50 ./opt/yad/locale/pt_BR/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/ru/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/ru/LC_MESSAGES/
-rw-r--r-- tele/tele     42978 2017-12-13 15:50 ./opt/yad/locale/ru/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/sk/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/sk/LC_MESSAGES/
-rw-r--r-- tele/tele     24079 2017-12-13 15:50 ./opt/yad/locale/sk/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/uk/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/uk/LC_MESSAGES/
-rw-r--r-- tele/tele     43117 2017-12-13 15:50 ./opt/yad/locale/uk/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/zh_TW/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/locale/zh_TW/LC_MESSAGES/
-rw-r--r-- tele/tele     19200 2017-12-13 15:50 ./opt/yad/locale/zh_TW/LC_MESSAGES/yad.mo
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/man/
drwxr-xr-x tele/tele         0 2017-12-13 15:50 ./opt/yad/man/man1/
-rw-r--r-- tele/tele     41446 2017-12-13 15:50 ./opt/yad/man/man1/yad.1
-rwxr-xr-x tele/tele    216352 2017-12-13 15:50 ./opt/yad/yad
```

- Zobacz na uprawnienia aby zwykły użytkowniknie mógł napisać pliku
- Oraz żeby każdy plik był zainstalowany tam gdzie Ty chcesz.


9. Zainstaluj gotowy pakiet  yad
```
$ su -c 'dpkg -i yad_0.40.0-1_amd64.deb'
```


10. Skonfiguruj zmienną $PATH.

- Dla użytkownika root edytuj plik /etc/profile
z konta root.
```
if [ "`id -u`" -eq 0 ]; then
  PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
  PATH="$PATH:/opt/yad"
else
  PATH="/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games"
fi
export PATH
```

Odśwież zmienną $PATH by móc odrazu ją używać
```
# source /etc/profile
```

Czy zmienna się zmieniła zmieniała, możesz sprawdzić.
```
# echo $PATH
```

- Dla zwykłego użytkownika dodaj na końcu pliku ~/.bashrc
z konta użytkownika:
```
if [ -d "/opt/yad/" ] ; then
 PATH="$PATH:/opt/yad"
fi
```

Tutaj niestety nie wiem jak załadować ponownie **~/.bashrc,**
więc musisz zrestartować swój komputer.


**Gotowe !**
I już możesz się cieszyć nową wersją yad.


