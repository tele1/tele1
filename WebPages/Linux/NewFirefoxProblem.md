


# Aktualizacja Firefoxa i znowu coś nie działa, tym razem w wersji 68 ESR.

* Wersja portale ma taki problem, ze maja jakiś problem z dodawaniem nowych bibliotek do niej, wiec trzeba ręcznie doinstalowywać.

* O ile dodano kilka opcji dla użytkowników, to nie da się importować zakładek ze starego Firefoxa. Bynajmniej nie bez zakładania konta Firefox.

Więc jak narazisz swoje prywatne zakładki na upublicznienie w internecie, to się da. Dlaczego?
W jednym z komunikatów o polityce prywatności ze cześć danych  może być gromadzona do celów marketingowych, analizy lub coś w tym stylu.
Więc prawdopodobnie chodzi też o pieniądze.

Jeżeli masz Linuxa,
jeśli nie chcesz się rejestrować nigdzie,
musisz na chwile zainstalować starsza wersje przeglądarki
i eksportować zakładki do pliku HTML.
 https://support.mozilla.org/en-US/kb/export-firefox-bookmarks-to-backup-or-transfer
Plik HTML możesz sobie otworzyć w przeglądarce lub przekonwertować do pliku tekstowego.
ja sobie przekonwertowałem w ten sposob.

```
 cat bookmarks.html | sed -e 's/<A HREF=[^"]*"/<DEL>/g' -e 's/" ADD_DATE/ <DEL/g' -e 's/<[^>]*>//g' > plik.txt 
```

Komenda cat wyświetla plik ( chociaż wystarczyłby tylko sed ).
Druga komenda sed wycina fragment kodu HTML przed linkami.
Trzecia komenda sed wycina fragment kodu HTML za linkami.
Czwarta komenda wycina wszystkie znaczniki HTML i pozostają tylko linki i opisy linków.
