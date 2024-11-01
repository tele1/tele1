

# Linux Developer Tips

## 1. Convenient editor for writing. 

The best would be IDE (Integrated Development Environment).     
But for example for the language " bash " at this moment I don't know good IDE for the language " bash ". Some people recommend Visual Studio Code, but it also has its drawbacks.

Recently I've been using the **Geany** text editor.

I wrote more in <https://github.com/tele1/tele1.github.io/blob/main/WebPages/Linux/Pluma.md>


## 2. How get help from source code. 

```
./configure --help
```
```
cmake .. --help
```
```
python setup.py --help
```


## 3. Always test in isolation. 

3.1 Usually (not always) apps are built in a virtual machine (for security reasons, for example).


3.2 And apps are packed in packages (for example .deb)

If learning how to pack into .deb is too hard, then you can try
```
checkinstall --install=no
```

3.3 Always try to choose local folder to install than system. Try use prefix option.

For example:
```
./autogen.sh --prefix=/home/your_user_name/bin
```
```
./configure --prefix=your_path_where_app_will_installed 
```
```
cmake .. -DCMAKE_INSTALL_PREFIX=/your/path/when/you/want/install/all/files
```

