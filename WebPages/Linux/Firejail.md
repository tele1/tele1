


# Blocking application access to the Internet. 

```
firejail --net=none app_name
```

# Blocking access to folders except one.

```
firejail --noprofile --whitelist=/path/to/folder app_name
```


# Video
Firejail Sandbox  - Firejail HowTo: Disable Network Access  
[![ Firejail Sandbox  - Firejail HowTo: Disable Network Access ](https://firejail.files.wordpress.com/2018/04/hb-x11-xephyr.png?w=625&h=482)](https://www.youtube.com/watch?v=xuMxRx0zSfQ " Firejail Sandbox")


# The default launch of the application in the sandbox

From root account   
Turn on - creating symbolic links.
```
firecfg
```

Turn off - removing symbolic links 
```
firecfg --clean
```

# Documentation 
1.  <https://firejail.wordpress.com/documentation-2/basic-usage/>  
2.  <https://wiki.archlinux.org/index.php/Firejail>  