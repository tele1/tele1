

# Bash - zmienne.



- Typowa zmienna
```
$nazwa
```


- Przypisanie czegos do zmiennej.
```
a=$(ls)
```

  Tutaj wynik komendy ls zostal przypisany do zmiennej $a


- Wyswietlenie zmiennej w terminalu
```
echo "$a"
```


 Cudzysow ma tutaj podwojne znaczenie,

    po pierwsze ciagi znakow oddzielone spacja zazwyczaj pisze sie w cudzyslowie,

    a po drugie gdyby dac wynik bez cudzyslowia, zawartosc wyswietlilaby sie tylko w 1 linii.


- Zapis szczegolny
  Jesli musimy uzyc zmiennej bez spacji np. $a i ona koliduje z innymi znakami to mozna ja jeszcze zapisac tak
```
${a}
```


- Przekierowanie zmiennej
```
a=$(ls)
i=4
c=$(awk 'NR=='$i <<< "$a")
```


a = nazwy katalogów lub plików
i = 4
c = 4 piersze katalogi lub pliki ze zmiennej $a

 W tym przykladzie w ostatniej linii ( w zmiennej $c )
 <<< "$a" zostalo podane zamiast sciezki do pliku
czyli jest to przekierowanie zawartosci zmiennej  $a do awk,
zamiast zawartosci pliku.

Awk natomiast pokaze tylko to co w linii o numerze $i ,
czyli pokaze tylko zawartosc 4 linii ze zmiennej $a i wynik bedzie przypisany zmiennej $c .


### Przyklad:

```
    # ścieżka do katalogów z *.rpm
    a1="/home/uzytkownik/moja/sciezka"

    # lista katalogow i plikow ścieżki $a1
    a=$(ls "$a1")

    # wystarczy usunąć "#", żeby zobaczyć co kryje się za zmienną $a
    #echo "$a"

    # liczymy wszystkie katalogi i pliki
    b=$(echo "$a" | wc -l)

    echo "-----------------"
    echo "Lini jest $b"
    echo "-----------------"

    # petla for wykona sie tyle ile jest 
    # razem katalogow i plików
        for i in `seq 1 $b`
        do
            # linia
            echo "$i"

            # nazwa folderu
            c=$(awk 'NR=='$i <<< "$a")

            # szukanie plików z końcówką .rpm
            d=$(find "$a1" -regex ".*.rpm")   

            # zapisanie listy plików do zmiennej $e
            if [ "$e" = "" ]; then
                e=$(echo "${d}")
            else
                e=$(echo -e "$e \n${d}")
            fi
        done

    # Pokaze wszytkie pliki .rpm ze znalezionych pod katalogow, katalogu $a1
    echo "$e"
```

Przykład pokazuje jak operować danymi bez zapisywania do pliku.
Może się także przydać do bardziej zaawansowanych rzeczy na plikach i folderach, aczkolwiek nie należy go traktować tylko do wyszukiwania plików,
ponieważ tylko do wyszukania plików lub katalogów wystarczy komenda find i jej opcje wyszukiwania.

___________________________________________________________

Edytowane:
W przykładzie wkradł się mały  błąd ...

```
echo "$a" | wc -l
```

wc liczy prawidłowo dopóki ma cokolwiek do liczenia,
problem się pojawi gdy zmienna $a będzie pusta.
```
$ echo "" | wc -l
1
```


Winne temu jest echo które pozostawia po sobie pustą linię
i wc je zlicza.


Jak zaradzić ?
- Można nie używać echo
```
ls "$a1" | wc -l
```

- Można usunąć puste linie
http://stackoverflow.com/questions/16414410/delete-empty-lines-using-sed

```
$ echo "" | grep "\S" | wc -l
0
```

```
$ echo "" | sed '/^$/d' | wc -l
0
```


