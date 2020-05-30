

# bash - Liczenie plikow i folderow.
 
## 1.  Jak policzyc pliki i foldery w danym folderze ?

Komenda ls wyswietli zarowno pliki jak i katalogi.  
- No ale jak to policzyc ?   
Z pomoca przyjdzie nam " wc -l "

```
$ ls  | wc -l
38
```

37 to ilosc naszych plikow i folderow w folderze w ktorym wpisalismy ta komende.  
- Jak to ? Ale tam bylo tylko 13 linii.  
- W tym przypadku to specjalnie podzielono linie w takie 3 kolumny, taki tryb widoku.

```
  |      -   to potok, wynik polecen przed tym znakiem
               zostanie wykorzystany do polecen za tym znakiem
               http://pl.wikipedia.org/wiki/Potok        
          -   znak taki mozna zrobic  przytrzymujac klawisze
             Shift  + \  
  wc    -  to komenda zliczajaca  -l  linie 
```

### TIP:

Komenda **find** także wyszuka Ci pliki.  
Zaletą bash jest to że możesz różnymi komendami rozwiązać zadanie :-)


## 2.  Jak policzyc pliki i foldery w danym folderze, ale razem z ukrytymi ?

Nalezy dodac  opcje -a ,  
Nalezy jednak wziasc cos pod uwage...


#### Przyklad:

W folderze mam:  
1 folder , 5 plikow widocznych , 1 plik ukryty  
co daje razem 7 wszystkiego, zobaczmy czy tak bedzie ...

Pokazuje 9 plikow, w tym ./ i ../ cos takiego (foldery),  
wypadaloby sie tego jakos pozbyc.  
- Moze od tych 9 odjac 2 ?

  OK :-)

W bashu dzialania arytmetyczne wykonujemy w nawiasach kwadratowych $[ ] ,  
 aby nie bylo bledu skladni oraz zeby bash znal kolejnosc wykonywanych zadan wypadaloby  
ls -a | wc -l umiescic w takim $( ) nawiasie, a potem od tego odjac 2

```
[gg@localhost Documents]$ echo $[ $(ls -a | wc -l) ]
9
[gg@localhost Documents]$ echo $[ $(ls -a | wc -l) -2 ]
7
```

echo dalem celowo inaczej terminal / konsola   
bedzie szukac takiej komendy, w tym przypadku liczby.


## 3. Jak policzyc tylko pliki lub foldery ?

- Zeby tego dokonac trzeba pierw rozpoznac ktora z wymienionych   
       nazw jest plikiem, a ktora katalogiem.

       Ktos powie ze katalogi maja na koncu " / " i sa innego koloru  
       Sluszna uwaga ... ale nalezy wziasc pod uwage:  
       *      pliki moga zawierac znak / choc moze i nie na koncu  
       *      kolory skladni zaleza od ustawien w danym systemie   

      Wiecej opcji ls znajdziemy wpisujac w terminalu ls 

```
ls --help
```

oraz

```
man ls
```

     nas zainteresuje opcja " -l "

```
$ ls -l 
total 43264
-rw-rw-r--  1 gg   gg   683872 Oct 10 22:13 111.plt
-rw-rw-r--  1 gg   gg     9463 Oct 10 22:13 111.svg
-rw-rw-r--  1 gg   gg      822 Nov 24 01:09 a
drwxrwxr-x  2 gg   gg     4096 Oct 22 01:57 aRPM/
drwxrwxr-x  3 root gg     4096 Nov 20 11:14 b-RPM/
```

- Opcja " -l " daje bardziej szczegolowe informacje o plikach i folderach. 
- Jesli piewszym znakiem jest " d " to oznacza on katalog (directory), 
- Jesli kreska " - " to oznacza on  plik.
             
     Wiecej informacji o tych atrybutach mozna znalesc w sieci:  
                 <www.cybertech.net.pl/atrybuty>  
                 <http://linoxide.com/howto-show-file-attributes-in-linux/>

- Ale jak wyciagnac z tego te informacje tylko te ktore chcemy ?  
Jesli chcemy zobaczyc tylko widoczne pliki

```
$ ls -l | grep -v "^d"
total 212
-rw-rw-r-- 1 gg gg 20788 Jan  3 21:22 ls wc l.png
-rw-rw-r-- 1 gg gg  2378 Dec  2 23:36 MumbleAutomaticCertificateBackup.p12
-rw-rw-r-- 1 gg gg 35136 Jan  4 00:09 plush-tux_17-208012958.jpg
-rw-rw-r-- 1 gg gg 92442 Oct 11 08:25 pluskwa.odt
-rw-rw-r-- 1 gg gg 51622 Nov 27 00:57 sad.odt
```

```
grep "tekst" - pokaze nam linie tylko zawierare slowo tekst.
       grep -v "tekst" - pokaze tylko linie ktore nie zawieraja slowa tekst.
       grep -v "^d" -  pokaze linie ktore nie zawieraja w pierwszym znaku
                               litery d , znak ^ jest wyrazeniem regularnym.
```

<http://jakilinux.org/konsola/wyszukiwanie-wyrazenia-regularne/>



Komenda " wc -l " by nam te linie ladnie policzyla, ale komenda " ls -l "  
pokazuje rowniez " total 212 " a to nie jest plik ani katalog.

Moze odejmiemy jedna linie ?  
Ok, wiec damy to najpierw w $( ) a potem odejmiemy 1  
i damy wszystko w nawias $[ ] aby obliczylo. 

```
]$ echo $[ $(ls -l | grep -v "^d" | wc -l) -1 ]
5
```

 Dziala i liczy jak trzeba :-).


>              Takie wyciaganie / edytowanie  informacji z wiekszej ilosci 
>              danych nazywane jest rowniez parsowaniem.


## 4. Jak policzyc tylko pliki lub foldery razem z ukrytymi ?

      Oczywiscie dodajesz a do ls ( ls -la ) jak w pkt.2   
      ale najpierw prztestuj kazde z polecen jak to bedzie dzialac.

 Musisz zwrocic uwage na ./ ../ przy wyniku ls,  
jak bedziesz chcial policzyc linie przy pomocy polecenia wc -l .

Policzmy sobie pliki + pliki ukryte:

```
$ ls -la | grep "^-"
-rw-rw-r--  1 gg gg     0 Jan  4 16:52 .bo
-rw-rw-r--  1 gg gg 20788 Jan  3 21:22 ls wc l.png
-rw-rw-r--  1 gg gg  2378 Dec  2 23:36 MumbleAutomaticCertificateBackup.p12
-rw-rw-r--  1 gg gg 35136 Jan  4 00:09 plush-tux_17-208012958.jpg
-rw-rw-r--  1 gg gg 92442 Oct 11 08:25 pluskwa.odt
-rw-rw-r--  1 gg gg 51622 Nov 27 00:57 sad.odt

$ ls -la | grep "^-" | wc -l
6
```

Policzmy sobie foldery + foldery ukryte: 

```
$ ls -la | grep "^d"
drwxr-xr-x  3 gg gg  4096 Jan  6 04:47 ./
drwxr-xr-x 81 gg gg  4096 Jan  6 02:10 ../
drwxrwxr-x  2 gg gg  4096 Jan  4 17:06 tt/

$ echo $[ $(ls -la | grep "^d" | wc -l) -2 ]
1
```

        Jedna z pieknych rzeczy w bashu sa jego mozliwosci,
        a dokladniej mnogosc sposobow na rozwiazanie problemu.
        Przykladowo grep "^-"  i grep -v "^d" moge stosowac zamiennie:

```
$ ls -la | grep "^-"
-rw-rw-r--  1 gg gg     0 Jan  4 16:52 .bo
-rw-rw-r--  1 gg gg 20788 Jan  3 21:22 ls wc l.png
-rw-rw-r--  1 gg gg  2378 Dec  2 23:36 MumbleAutomaticCertificateBackup.p12
-rw-rw-r--  1 gg gg 35136 Jan  4 00:09 plush-tux_17-208012958.jpg
-rw-rw-r--  1 gg gg 92442 Oct 11 08:25 pluskwa.odt
-rw-rw-r--  1 gg gg 51622 Nov 27 00:57 sad.odt

$ ls -la | grep -v "^d" 
total 220
-rw-rw-r--  1 gg gg     0 Jan  4 16:52 .bo
-rw-rw-r--  1 gg gg 20788 Jan  3 21:22 ls wc l.png
-rw-rw-r--  1 gg gg  2378 Dec  2 23:36 MumbleAutomaticCertificateBackup.p12
-rw-rw-r--  1 gg gg 35136 Jan  4 00:09 plush-tux_17-208012958.jpg
-rw-rw-r--  1 gg gg 92442 Oct 11 08:25 pluskwa.odt
-rw-rw-r--  1 gg gg 51622 Nov 27 00:57 sad.odt
```

```
       grep "^-"        pokazuje linie z pierwszym znakiem - , czyli pliki
       grep -v "^d"   pokazuje linie inne niz z pierwszym znakiem d , 
                              a poniewaz oprocz d jest tylko - , czyli pliki.
```


## 5. Jak policzyc pliki i foldery w danym folderze i jego podfolderach ?  


Najpierw sobie przetestuje na katalogu "Documents"  
Zaczne od sprawdzenia ile mam plikow w katalogu i podkatalogu tt. 

```
$ tree 
.
├── libaudit.so.0 -> libaudit.so.0.0.0
├── ls wc l.png
├── MumbleAutomaticCertificateBackup.p12
├── plush-tux_17-208012958.jpg
├── pluskwa.odt
├── sad.odt
└── tt
    ├── libaudit.so.0 -> libaudit.so.0.0.0
    └── MumbleAutomaticCertificateBackup.p12

1 directory, 8 files
```

Tree ladnie wyswietlilo strukture, ale nie kazdy przeciez musi   
  miec zainstalowane tree.   
W kazdym razie wyraznie pokazuje ze mam  
 1 katalog i 8 plikow (6 + 2 w katalogu tt).

```
$ ls -R
.:
libaudit.so.0@  MumbleAutomaticCertificateBackup.p12  pluskwa.odt  tt/
ls wc l.png     plush-tux_17-208012958.jpg            sad.odt

./tt:
libaudit.so.0@  MumbleAutomaticCertificateBackup.p12

$ echo $[ $(ls -R | wc -l) -3 ]
9
```

Mam 9 razem plikow i folderow razem.  
- Skad wielem opcje -R ?
Ta opcje znajdziemy zapoznajac sie z pomocami po wpisaniu polecen

>        man ls   

oraz 

>        ls --help


Policzmy sobie ile plikow i folderow razem mam w systemie :-)  
  - W tym celu trzeba przejsc do katalogu glownego.  
  - Zrobie to z pod root abym mial dostep do kazdego katalogu.  
  - Dodam jeszcze polecenie time w celu pokazania czasu ile zajelo  liczenie. 

```
# cd /

# time echo $[ $(ls -R | wc -l) -3 ]
ls: reading directory ./proc/3531/net: Invalid argument
ls: reading directory ./proc/3531/task/3531/net: Invalid argument
ls: reading directory ./proc/3549/net: Invalid argument
ls: reading directory ./proc/3549/task/3549/net: Invalid argument
1157503

real 1m14.513s
user 0m1.892s
sys 0m4.358s
```

1 157 503 plikow i folderow razem (nie liczac ukrytych),  
    liczenie tego zajelo ponad minute. 

Jezeli artykul zawiera błedy, niedoskonałości to daj znać.


