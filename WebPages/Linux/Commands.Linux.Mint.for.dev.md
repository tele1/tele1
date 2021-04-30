

# Useful commands about files and packages on Linux Mint.

__________

## 1.  For search files which are in the repository.  
This means that apt-file download a package database from the internet and looks for the file there.  
This means that this file I don't need have installed.
```
apt-file search file
```


## 2. Allows you to find a package name in the repository.
```
apt-cache search package_name
```


## 3.  For check which package provide /path/to/file , which you have installed.
```
dpkg -S /path/to/file
```


## 4. For check if package is installed.
```
dpkg -l name_package
```


## 5. How find path of application
### 5.1 Command "locate"
Command command **locate** is part of mlocate package.  
Before first use, you need create database from root account.
```
updatedb
```
Then you can use, for example like this with **grep** command
```
locate file_name | grep /bin
```
### 5.2 Command which
If you are using firejail, the path of file may be different 
```
which file_name
```
### 5.3 Command type
If you are using firejail, the path of file may be different 
```
type file_name
```

## 6. How to find the repository of which a package belongs 
```
apt policy package name
```
