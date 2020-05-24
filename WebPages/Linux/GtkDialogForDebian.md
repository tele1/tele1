

# Compile Gtkdialog on Debian 8.8




## Info:
-  GtkDialog lets your bash script run in GUI (it looks like GTK, QT ).  
Created by " Puppy Linux " developers
(  designed for linux distributions )

- Gtkdialog not exist now for Debian,
 so you need compile from source code if you want have

- Examples: 
http://xpt.sourceforge.net/techdocs/language/gtkdialog/gtkde02-GtkdialogExamples/single/


## Tutorials:
1. Examples:
 http://xpt.sourceforge.net/techdocs/language/gtkdialog/gtkde02-GtkdialogExamples/single/

2. Examples inside sorce code:
 .... /gtkdialog-master/examples/

3. How it works:
 http://murga-linux.com/puppy/viewtopic.php?p=274035#274035

4. How it works:
 http://xpt.sourceforge.net/techdocs/language/gtkdialog/gtkde03-GtkdialogUserManual/

5.  Bigger examples
https://code.google.com/archive/p/gtkdialog/downloads

6. Wiki ( all commands )
http://01micko.com/reference/

7. Some example exist inside PCLinuxOS magazine
http://pclosmag.com/html/Issues/200910/page21.html



## How compile and install GtkDialog on Debian.

1. Install dependencies
( you can from terminal, from root like this )
```
apt-get install automake libglib2.0-dev  libgtk2.0-dev byacc  libvte-dev flex libbison-dev libglade2-dev
```


info:

libglib2.0-dev provide gthread


If you have error and can not something find ( file ),
 you can try find from user account
```
apt-file -l search file_name
```



2. Download source code from
https://github.com/01micko/gtkdialog


3. Unpack file and  go to files ( gtkdialog-master folder )


4. Run script from terminal
which will check dependency

```
./autogen.sh --prefix=/home/your_user_name/bin
```


Info:

Default paths for install apps from source code are /bin/ /lib
and for install this app you need root,
this is not safe, We suggest install to user path,
 for example to /home/user_name/bin/
so I used it in option " --prefix=/home/your_user_name/bin " .
 then you can install with user permissions.

It will looks like this after install :
```
 /home/tele/bin/
├── bin
│   └── gtkdialog
└── share
    ├── icons
    │   └── hicolor
    │       ├── 32x32
    │       │   └── apps
    │       │       └── gtkdialog.png
    │       └── icon-theme.cache
    └── info
        ├── dir
        └── gtkdialog.info

7 directories, 5 files
```

If you want have 1 folder for 1 app inside ~/bin folder, for example:
```
 /home/tele/bin/ 
├── gtkdialog  
│         └── ...
├── next app
│         └── ...
└── next app
           └── ...
```

try change all paths in this tutorial,
from  " /home/your_user_name/bin "
to       " /home/your_user_name/bin/gtkdialog "
 

5. Compile
```
make
```


6. If you don't have any errors,
now you can install ( and do not use root ! )
```
make install
```


Your  app will be installed to
> " /home/user_name/bin/bin/gtkgialog "


7. How run this app ?

Your system know default paths for apps,
 for example   /bin/ , /usr/bin/ , /usr/local/bin/
but don't know your path.
For this you need edit for example ~/.profile file.

Open ~/.profile with text editor and change
```
~/.profile
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```

to
```
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin/" ] ; then
    PATH="$HOME/bin:$HOME/bin/bin:$PATH"
fi
```


Info:

$HOME and ~/ and /home/user_name/ this is the same.
added path here it is " :$HOME/bin/bin " , there exist gtkdialog app.


and refresh current shell with command
```
source ~/.profile
```


 Test from terminal ...
```
$ gtkdialog -v
gtkdialog version 0.8.4 release (C) 2003-2007 Laszlo Pere, 2011-2012 Thunor
Built with support for: GTK+ 2.
```


Working !  :-)

Now you can run any bash script with gtkdialog.
And if you will want remove this gtkdialog,
 just remove folder /home/user_name/bin .
That's all.



*Edited 28.05.2017*

Other way, when we need build app for use from root.
For this I tried build .deb package.
( added path /root/.profile and /home/use/bin/ not working for "su" )

So, like above ...

1. Install dependencies from root.
```
apt-get install automake libglib2.0-dev  libgtk2.0-dev byacc  libvte-dev flex libbison-dev libglade2-dev checkinstall
```


2. Compile from user.
```
make
```


3. Build .deb package with checkinstall.
```
checkinstall --install=no
```


My settings inside:
```
This package will be built according to these values: 

0 -  Maintainer: [ tele@tele ]
1 -  Summary: [ GtkDialog lets your bash script run in gui. ]
2 -  Name:    [ gtkdialog ]
3 -  Version: [ 0.8.4 ]
4 -  Release: [ 1 ]
5 -  License: [ GPL ]
6 -  Group:   [ checkinstall ]
7 -  Architecture: [ amd64 ]
8 -  Source location: [ gtkdialog-0.8.4 ]
9 -  Alternate source location: [  ]
10 - Requires: [ libgtk2.0-0 libglade2-0 ]
11 - Provides: [ gtkdialog ]
12 - Conflicts: [  ]
13 - Replaces: [  ]
```


 4. Install .deb package from root
```
dpkg -i gtkdialog_0.8.4-1_amd64.deb
```

And ready :-) .

