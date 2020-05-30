

# bash - Debugowanie skryptów
 
Jednym z bardziej denerwujących rzeczy w bash-u jest brak odpowiedniego debugowania.  
Na przykład zapomnieliśmy dodać gdzieś cudzysłowia.

```
./plik --help
+ ./plik --help
./plik: linia 464: nieoczekiwany EOF podczas poszukiwania pasującego `"'
./plik: linia 476: błąd składni: nieoczekiwany koniec pliku  
```


I nie możemy znaleść gdzie ...  
I co teraz ? 


Możemy się wspomóc tym  
 <http://wiki.bash-hackers.org/scripting/debuggingtips>  
lub tym  
  <http://linuxcommand.org/wss0100.php>  
 ale to nie wiele pomoże.

 Przy założeniu że w każdej linii liczba cudzysłowi powinna być  parzysta to można sobie napisać komende która  
* po pierwsze, pokaże tylko znaki cudzysłowia w każdej linii  
* po drugie numer linii.

Przykład:

```
cat plik | sed 's/[^"]//g' | cat -n | grep "\""
```


I otrzymamy przykładowo coś takiego

```
   227 ""
   234 ""
   237 ""
   245 ""
   246 ""
   258 ""
   263 ""
   268 ""
   273 "
   290 ""
   293 """"
   295 ""
   299 ""
```

I dzięki temu prawie odrazu widzimy gdzie brakuje cudzysłowia.  
Albo jeszcze dokładniej, choć może nie zawsze szybciej

```
cat plik | sed 's/[^"]//g' | awk '{ print length }' | cat -n | grep "[13579]$"

   273 1
```


Czyli komenda nam zwróciła numer linii  
  oraz nieparzystą liczbę wystąpień cudzysłowia.  
Dzięki temu wiemy że w linii 273 znajduje się tylko 1 cudzysłów.


