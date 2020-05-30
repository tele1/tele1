
# Github dla początkujących - Wysyłanie plików.

Poradnik będzie dotyczył tylko 
kilka bardzo podstawowych rzeczy które powinieneś znać,
by umieć obsługiwać github-a.
Jak chcesz więcej, to poszukaj lepszego poradnika.




## 1. Jak pobrać z github-a by móc edytować kod źródłowy ?
Należy w terminalu wykonać komendę,
która pobierze kod źródłowy, w miejscu w którym znajdujesz się w terminalu

git clone https://github.com/nazwa_uzytkownika/nazwa_projektu


Przykład:

```
git clone https://github.com/tele1/gdi
```


Więcej na:
https://help.github.com/articles/cloning-a-repository/

## 2. Jak uploadować projekt na github ?
Pobrany wcześniej projekt zawiera ukryty folder "bazy zmian" ( .git )
github dzięki temu wie które zmiany należy wysłać.
Żeby uploadować zmiany na githuba,
należy najpierw zaktualizować tą "bazę zmian".

Wchodzimy do katalogu  projektu / kodu źródłowego.
Wykonujemy w terminalu w celu zaktualizowania "bazy zmian".

`git add -A`


Dodajemy komentarz czego zmiany dotyczą.

`git commit -m 'twoj komentarz zmian'`



Wysyłamy do githuba.

`git push https://github.com/nawa_uzytkownika/nazwa_projektu odgalezienie_projektu`


Przykład:

`git push https://github.com/tele1/gdi master`


Gdzie "master" to moje główne wydanie projektu gdi na githubie.
Przy wysyłaniu podajemy login i hasło do serwisu.

W przypadku włączonej weryfikacji dwuetapowej,
żeby móc uploadować projekt,
należy w ustawieniach github-a stworzyć token
( taki rodzaj hasła lub klucza )
i wklejamy go zamiast hasła przy wysyłaniu plików.
Bezpieczniejsze się to nie wydaje, ale tokeny można usuwać i tworzyć w dowolnej chwili.


Więcej możesz znaleść także na
https://help.github.com/categories/creating-cloning-and-archiving-repositories/

Sprawdzaj tam każdy niebieski napis,
 bo mogą one ukrywać dodatkowe strony.

## 3. Zabezpiecz się, czyli weryfikacja dwuetapowa github.
Polega to na tym że przy logowaniu do serwisu
oprócz loginu i hasła musisz podać kod.
Kod jest brany z:

- klucza usb ( " FIDO U2F Security Key " )
https://help.github.com/articles/authenticating-to-github-using-fido-u2f-via-nfc/

- albo aplikacji na telefonie
https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/

- albo wiadomości SMS

- albo " Recovery codes " które należy sobie odrazu wydrukować 
po aktywowaniu weryfikacji dwuetapowej
i przechowywać w bezpiecznym miejscu.

- albo facebook


Więcej tu:
https://help.github.com/articles/about-two-factor-authentication/

## 4. Jak wysyłać na github przy włączonej weryfikacji dwuetapowej.
https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/

To wszystko,
 przyjemnego i bezpiecznego użytkowania z githuba. 


# 5. GitHub Trics 

### 1. Tworzenie nowych folderów w repozytorium przez przeglądarkę.

Kiedy dodajesz nowy plik, spróbuj dodać " / "  
Jeżeli chcesz edytować folder, edytuj całą ścieżkę klikając " Backspace " na klawiaturze.


### 2. Linux Alias

1. Dodaj na końcu pliku .bashrc

```
###########################{
GITGIT(){
if [[ -d ".git" ]] ;then
	git add -A ;  git commit -m 'update'
	DIR_NAME="${PWD##*/}"
	git push https://github.com/your_user_name/${DIR_NAME} master
else
	echo "Folder .git not found to update this `pwd` repository."
fi
}
# Usage: gitupdate name_repository
alias gitupdate='GITGIT'
###########################}
```

2. Zaktualizuj aktualną bazę aliasów.

```
source ~/.bashrc.
```

3. Przetestuj alias

4. Zabezpiecz plik przy pomocy " chattr +i "
