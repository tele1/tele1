

## From User Cron

[cron time] [export DISPLAY=:0] ; [command or path to script]

**Example:**

```
* * * * * export DISPLAY=:0  ; xmessage -center -buttons Ok:0 "Hello world"
```


## From Root Cron

[cron time] [export DISPLAY=:0] ; [sudo -u user_name or su user_name] [command or path to script]

**Example:**

```
* * * * * export DISPLAY=:0  ; sudo -u tele xmessage -center -buttons Ok:0 "Hello world"
```




#### Warning:

If you run script at computer startup, for example:

```
@reboot /your/script
```

And command or script does not show GUI, try add time, for example:

```
@reboot sleep 120 && /your/script
```
