

# Test prędkości odczytu pendriva.

## Stare USB & Nowe USB

Do testu użyłem  
- **EMTEC** 8GB  nr. Z1467 ( stare, używane USB 2.0 )  
- **SONY** 32GB  nr. D33021 ( nowe USB 3.0 )


Sens testu:  
Test ma na na celu porównanie odczytu  
starego pendriva USB i nowego  
Test może wydawać się zabawny ( po co ? ),  
ale chciałem sprawdzić,  
stąd ten uśmieszek :D


Podczas testu wykorzystano:  
- płyta główna

```
# dmidecode -t 2
dmidecode 2.12
SMBIOS 2.7 present.

Handle 0x0002, DMI type 2, 15 bytes
Base Board Information
 Manufacturer: MSI
 Product Name: Z77A-G43 (MS-7758)
 Version: 1.0
...
```

- system operacyjny

```
$ cat /etc/*-release
...
DISTRIB_DESCRIPTION="UPLOS Linux"
UPLOS release 2017 (UPLOS) for i586
```

Tak, istnieje taki system operacyjny  
a UPLOS to jedna z wielu dystrybucji / rodzajów Linuxa  
jakby ktoś nie wiedział :D




## Czas na testy:

###  SONY

- **włożone do gniazda USB 3.0 w obudowie komputera**

```
# hdparm -t /dev/sdc

/dev/sdc:
 Timing buffered disk reads: 180 MB in  3.03 seconds =  59.49 MB/sec
```

- **włożone do gniazda USB 3.0 z tyłu komputera,**  
czyli bezpośrednio do płyty głównej 

```
# hdparm -t /dev/sdc

/dev/sdc:
 Timing buffered disk reads: 180 MB in  3.03 seconds =  59.46 MB/sec
```

Przy większej ilości testów wydać że prędkość odczytu waha się  
między 59 ~ 63 MB/sec. ( pływa )

Czy miejsce gniazda USB 3.0 ma znaczenie ?  
Z testu wynika, że nie. A jeśli już to bardzo nie wielką.  
Więc dla wygody skupie się na gniazdach 2.0 i 3.0 na obudowie komputera.

- **włożone do gniazda USB 2.0 w obudowie komputera**

```
# hdparm -t /dev/sdc

/dev/sdc:
 Timing buffered disk reads: 104 MB in  3.05 seconds =  34.11 MB/sec
```

Ile kosztował ?  
79,99 zł  w dniu 9.06.2018


### EMTEC

- **włożone do gniazda USB 2.0 w obudowie komputera**

```
# hdparm -t /dev/sdc

/dev/sdc:
 Timing buffered disk reads:  46 MB in  3.01 seconds =  15.29 MB/sec
```

I przy większej ilości testów waha się między 12.9 ~15.2 MB/sec  
 ( częściej 12.9 MB/sec)

- **włożone do gniazda USB 3.0 w obudowie komputera**

```
# hdparm -t /dev/sdc

/dev/sdc:
 Timing buffered disk reads:  48 MB in  3.08 seconds =  15.57 MB/sec
```

Przy większej ilości testów waha się między  13.2 ~ 15.5 MB/sec  
 ( częściej 13.2 MB/sec )



Ile kiedyś mógł kosztować ?  
- nie wiem.


**Wnioski:**  
Nowy pendrive jest około 4x szybszy :D


Jeśli ktoś ma ochotę zgłębić więcej wiedzy może poczytać  
- <https://en.wikipedia.org/wiki/USB>
- przykładowy inny test <https://www.dobreprogramy.pl/wojtekadams/Test-predkosci-odczytuzapisu-pamieci-typu-Pendrive,31224.html>


**Niepotrzebne nie czytać:**  
- Użyty obrazek którego już nie ma jest na licencji: "Free for commercial use"  
i wziąłem z  https://www.iconfinder.com/icons/1325173/emoji_emoticon_happy_joy_laugh_reaction_smile_icon  
- Podczas testu wszyscy i wszystko przeżyło i nikt nie ucierpiał :D  
Mam nadzieje także że nikt się nie urazi czytając mój test.  
- Post nie był sponsorowany w jakikolwiek sposób.





