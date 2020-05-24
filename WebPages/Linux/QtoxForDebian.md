

# How get new qtox for Debian ?

------------

## Info: 
    *QTox is a new kind of instant messaging.*

------------
 
## How get new qtox for Debian ?

  I will try to show how to easily compile from the source code and install qtox for Debian.
This is a guide for more advanced users, 
because 
- this is not easy
- always install checked packages from the Debian repository for security.

And here is problem, Debian not support Qtox. 




## How start ?

### 1. Download qtox source code.

https://github.com/qTox/qTox

on website find "releases" bookmark and click.
And download the latest source code tar.gz . For me today, this is v1.13.0


### 2. Compile source code.
 In theory
```
$ mkdir build
$ cd build
$ cmake ..
$ make
```

But not this time,
I will do a little differently,
I will install the package in the home directory.


First unpack qTox-1.13.0.tar.gz
Go inside qTox-1.13.0 folder
from terminal in folder qTox-1.13.0
 ( watch tutorials if you don't know how something )


copy each command separately,  paste, edit and run.

```
mkdir -p /home/your_user_name/NIC/
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/home/your_user_name/NIC/ ..
```

First command will create folder NIC

...  second will create "build" folder

...  third will go to build folder

... Last command "cmake"will check installed dependencies ( header files, *.h )  needed to compile source code.
If you see any error, read and install needed dependencies from Synaptic.
In Debian most needed dependencies for compile with headers 
will have name " *-dev " ( on other than Debian may have " *-devel " )
   Something else,
I added also path where I want install ready package,
then I may easily remove the package
 after " make install " command.
And ... this will ~/home directory,
 so I don't need use root account to install files. 


### Warning !
Everything what you have in your home directory,
it can be read or overwritten by a malicious program.
So some applications you can run from sandbox
or install and run from other user account with appropriate permissions.



### INFO:
```
$HOME or " ~ "  --> this is path to your home directory
write in terminal  " mkdir --help " then 
"man mkdir" for more info about this command ( with " q " key, you can exit )
$  --> You see it from user account
#  --> You see this from root accout, 
don't use root, if you don't need for own security

This is example, when I wrote
"your_user_name"
you need change this to own user name from /home/ path.
```


Error with  sqlcipher
```
- Checking for one of the modules 'libswscale'
-- LIBSWSCALE LIBRARY_DIRS:
-- LIBSWSCALE INCLUDE_DIRS: /usr/include/x86_64-linux-gnu
-- LIBSWSCALE CFLAGS_OTHER:
-- LIBSWSCALE LIBRARIES:    swscale
-- LIBSWSCALE found
-- Checking for one of the modules 'sqlcipher'
CMake Error at cmake/Dependencies.cmake:73 (message):
  SQLCIPHER package, library or framework not found
Call Stack (most recent call first):
  cmake/Dependencies.cmake:105 (search_dependency)
  CMakeLists.txt:80 (include)
```

This is exmaple when you need install libsqlcipher-dev from Synaptic.

This time for me this is more important.

I don't know what you did before,
but I had ( long time ago ) problem run new Qtox,
problem was with new libsqlcipher0  3.2.0-2

```
[22:13:38.547 UTC] core/core.cpp:270 : Debug: Loading user profile
[22:13:38.547 UTC] core/core.cpp:132 : Warning: Core starting with IPv6 disabled. LAN discovery may not work properly.
[22:13:38.627 UTC] persistence/db/rawdatabase.cpp:572 : Warning: Failed to prepare statement "SELECT count(*) FROM sqlite_master" with error 26
[22:13:38.627 UTC] persistence/db/rawdatabase.cpp:181 : Warning: Database is unusable, check that the password is correct
[22:13:38.628 UTC] persistence/db/rawdatabase.cpp:116 : Debug: Couldn't create the backup of the database, won't upgrade
```

so I installed previous version libsqlcipher0  3.2.0-1.1~bpo80+1
from jessie-backports repository and I pinned package. 
This is solution, when you want update system with out this package.

```
 Now I tested, Qtox-1.13.0 working with 
  libsqlcipher0  3.2.0-1.1~bpo80+1
  libsqlcipher0  3.4.1-1
but not with 
  libsqlcipher0  3.2.0-2
```




## How install other version package ?
I use Debian 9.2 stretch
```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Debian
Description: Debian GNU/Linux 9.2 (stretch)
Release: 9.2
Codename: stretch
```


And first I need undo things which I did before.
 I pinned libsqlcipher0  3.2.0-1
```
$ cat /var/lib/synaptic/preferences
Package: libsqlcipher0
Pin: version 3.2.0-1.1~bpo80+1
Pin-Priority: 1001
```


I can remove file or "comment out" with " # " this lines inside file.

```
$ cat /var/lib/synaptic/preferences
#Package: libsqlcipher0
#Pin: version 3.2.0-1.1~bpo80+1
#Pin-Priority: 1001
```

After this in Synaptic I can install other libsqlcipher version.
But this is not all.
Next thing, what I need do, this is  
in /etc/apt/sources.list
  comment with "#" all working repositories
  and uncomment ( remove "#" )  repository 
from where we want download libsqlcipher.


For example:
repository which which I comment
```
# deb http://httpredir.debian.org/debian/ stretch main contrib non-free
```

( if you want use older package, you should "pin" before system update )

and repository which I added
 for libsqlcipher0  3.2.0-1.1~bpo80+1
```
deb http://ftp.debian.org/debian jessie-backports main
```

or
for libsqlcipher0  3.4.1-1
```
deb http://ftp.pl.debian.org/debian/ buster non-free main contrib
```

then I can refresh Synaptic and download libsqlcipher-dev which I want.


### Something else ...  only info ...
I use this repository
```
deb http://deb.debian.org/debian/ stable main contrib non-free
```

instead
```
deb http://httpredir.debian.org/debian/ stretch main contrib non-free
```

because I wanted have  " Debian rolling release "
I'm not sure now, but new repository I get probably from
https://debgen.simplylinux.ch/
... if you want also use.




When the cmake script finishes checking dependency successfully,
 the final part will look like this ...
```
-- GTK found
-- FILTERAUDIO not found
-- not using filteraudio, libfilteraudio not found
-- CMAKE_C_FLAGS: 
-- CMAKE_CXX_FLAGS:  -std=c++11 -fno-exceptions -fno-rtti -Wstrict-overflow -Wstrict-aliasing -Werror -fstack-protector-all -Wstack-protector -pthread -pthread
-- Configuring done
-- Generating done
-- Build files have been written to: /home/tele/Pulpit/test/Qtox/qTox-1.13.0/build
```

After that, you can edit /etc/apt/sources.list again
for activate stable repository, and disable others.



Then we will start compiling source code.
```
$ make
```


When the make finishes compiling source code successfully,
the final part will look like this ...
```
[ 99%] Built target test_posixsignalnotifier_automoc
Scanning dependencies of target test_posixsignalnotifier
[ 99%] Building CXX object CMakeFiles/test_posixsignalnotifier.dir/test/platform/posixsignalnotifier_test.cpp.o
[100%] Building CXX object CMakeFiles/test_posixsignalnotifier.dir/test_posixsignalnotifier_automoc.cpp.o
[100%] Linking CXX executable test_posixsignalnotifier
[100%] Built target test_posixsignalnotifier
```




### 3. Install source code. 
 
You can do it in two ways

- install with " make install " command,

minuses this solution ...
* you will have to manually delete files only.
pros this solution...
* if you will install to one folder, it's not hard remove files
* if you will install somewhere to ~/home , you don't need use root account.

 - or build .deb package, then after install you can remove from Synaptic.



 Because I don't know how build professional .deb package,
 and I do not have enough time,
 So I used simple, not professional, tool for this ( checkinstall ).
( if you don't have  checkinstall, you can install )


Run command from terminal ...
```
$ checkinstall --install=no
```


After that command I choose
```
The package documentation directory ./doc-pak does not exist. 
Should I create a default set of package docs?  [y]: n
```


And I changed ...
```
This package will be built according to these values: 

0 -  Maintainer: [ tele ]
1 -  Summary: [ A New Kind of Instant Messaging ]
2 -  Name:    [ qtox ]
3 -  Version: [ 1.13.0 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL v3 ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ amd64 ]
8 -  Source location: [ build ]
9 -  Alternate source location: [  ]
10 - Requires: [  ]
11 - Provides: [ qtox ]
12 - Conflicts: [  ]
13 - Replaces: [  ]

Enter a number to change any of them or press ENTER to continue: 
```


Then, you can see files when will be installed ...
 or not, and finish build .deb package.
```
/home
/home/tele
/home/tele/NIC
/home/tele/NIC/bin
/home/tele/NIC/bin/qtox
/home/tele/NIC/share
/home/tele/NIC/share/appdata
/home/tele/NIC/share/appdata/qTox.appdata.xml
/home/tele/NIC/share/applications
/home/tele/NIC/share/applications/qtox.desktop
/home/tele/NIC/share/icons
/home/tele/NIC/share/icons/hicolor
/home/tele/NIC/share/icons/hicolor/128x128
/home/tele/NIC/share/icons/hicolor/128x128/apps
/home/tele/NIC/share/icons/hicolor/128x128/apps/qtox.png
...

You probably don't want them to be included in the package.
Do you want me to list them?  [n]: n
```

```
**********************************************************************

 Done. The new package has been saved to

 /home/tele/Pulpit/test/Qtox/qTox-1.13.0/build/qtox_1.13.0-1_amd64.deb
 You can install it in your system anytime using: 

      dpkg -i qtox_1.13.0-1_amd64.deb

**********************************************************************
```

Then install .deb package from root.



### 3. Run app.
You can run app from terminal like this 
>   /home/tele/NIC/bin/qtox
or 
>  ./qtox
but this is not comfortable. So I created icon on Desktop 
( for Mate, graphic environment )
which inside text editor looks like this ...
```
#!/usr/bin/env xdg-open

[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Icon[pl_PL]=mate-panel-launcher
Name[pl_PL]=QTox
Exec=/home/tele/NIC/bin/qtox
Comment[pl_PL]=qTox is a powerful Tox client.
Name=QTox
Comment=QTox is a powerful Tox client.
Icon=/home/tele/NIC/share/icons/hicolor/scalable/apps/qtox.svg
```

Right click on the desktop, click " create activator " 
 fill in the empty fields
and you should have similar file like above.


And it has such permissions ...
```
$ ls -l | grep QTox
-rwxr-xr-x  1 tele tele     321 lis 29 01:49 QTox.desktop
```

if you need, you can change like this ...
```
$ chmod 755 qtox.desktop
```



For help with permissions you can use 
https://www.thepcmanwebsite.com/chmod_calculator.shtml




**That's all, I hope your new Qtox works and you're happy.**
**Have a nice day !**




*Date of publication*
*30 November 2017*
