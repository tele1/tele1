


# Zabezpieczenie plików przed zapisem przy pomocy chattr (immutable)

<blockquote>
i - uniemożliwia wykonywanie operacji na pliku (edycja, zmiana nazwy, kasowanie, tworzenie dowiązań) wszystkim użytkownikom systemu - także superużytkownikowi (root). Opcja ta może być ustawiana lub zdejmowana przez roota.
</blockquote>

#### Przykład jak zabezpieczyć plik **.bashrc** w katalogu domowym.

1. Sprawdzamy plik
```sh
$ ls -la
razem 344
drwxr-xr-x 25 x x  4096 maj 29 20:25 ./
drwxr-xr-x  4 root root  4096 kwi  7 16:03 ../
-rw-------  1 x x 44454 maj 29 18:55 .bash_history
-rw-r--r--  1 x x   220 mar 27 00:48 .bash_logout
-rw-r--r--  1 x x  4377 maj 29 20:25 .bashrc

$ lsattr .bashrc
--------------e--- .bashrc
```

2. Z konta root zabezpieczamy plik.

```sh
# chattr +i .bashrc
```

3. Sprawdzamy plik

```sh
$ ls -la
razem 344
drwxr-xr-x 25 x x  4096 maj 29 20:25 ./
drwxr-xr-x  4 root root  4096 kwi  7 16:03 ../
-rw-------  1 x x 44454 maj 29 18:55 .bash_history
-rw-r--r--  1 x x   220 mar 27 00:48 .bash_logout
-rw-r--r--  1 x x  4377 maj 29 20:25 .bashrc

$ lsattr .bashrc
----i---------e--- .bashrc
```

4. Jeśli chciałbyś cofnąć zmiany / odznaczyć atrybut pliku 
Z konta root

```sh
# chattr -i .bashrc
```


:)
