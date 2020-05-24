

# Virtualbox



    Błąd przy montowaniu dysku .vdi z Manjaro do Debiana. 
```
Cannot register the hard disk '/media/tele/MachinLos32/los.test.vdi' 
{4cdf9833-8a84-484f-90d4-8a58cefd7dcd}
 because a hard disk '/run/media/tele/MachinLos32/los.test.vdi'
 with UUID {4cdf9833-8a84-484f-90d4-8a58cefd7dcd} 
already exists.
```


1. Dla porządku skopiuj sobie maszyny ( choć nie jest to konieczne )
do

**/home/nazwa_użytkownika/VirtualBox VMs/**


2. Popraw ścieżki w 
 /home/nazwa_użytkownika/VirtualBox VMs/nazwa_maszyny.vbox-prev
przy pomocy edytora tekstowego
z " /run/media " na " /media " 

3. Znajdź dyski .vdi ,
 otwórz terminal w tamtym miejscu i wykonaj komendę
```
VBoxManage internalcommands sethduuid *
```

lub ( jeśli w katalogu jest więcej niż 1 dysk )
```
VBoxManage internalcommands sethduuid nazwa_dysku.vdi
```

Przykład: 
```
$ VBoxManage internalcommands sethduuid los.test.vdi

    UUID changed to: 84af6d95-12c2-4ed2-8631-17a3da613aa9 
```


To wszystko, gotowe!

