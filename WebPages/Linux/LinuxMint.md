

One of the linux mint images is based on the ubuntu distribution.
Sometimes you may find internet connections.


network-manager-config-connectivity-ubuntu
```
NetworkMa  TCP user:38812->32.121.122.34.bc.googleusercontent.com:http (SYN_SENT)
```




From "lsof -i" command
```
http  TCP user:35566->kudan.canonical.com:http (ESTABLISHED)
http  TCP user:37308->actiontoad.canonical.com:http (ESTABLISHED)
http  TCP user:35180->aerodent.canonical.com:http (ESTABLISHED)
http  TCP user:50222->mx.sygnow.net:http (SYN_SENT)
```

From "pstree" command
```
|-mintUpdate(2240)-+-sudo(95631)---mint-refresh-ca(95632)-+-gpgv(95644)
                                      |-http(95636)
                                      |-http(95637)
                                      |-http(95638)
                                      |-http(95639)
                                      `-store(95876)

```

And we see mintupdate

**You should check**
https://www.howtogeek.com/349844/how-to-stop-ubuntu-from-collecting-data-about-your-pc/
https://www.omgubuntu.co.uk/2018/02/ubuntu-data-collection-opt-out
https://ubuntu.com/blog/a-first-look-at-desktop-metrics
https://www.omgubuntu.co.uk/2017/09/disable-network-connectivity-checking-ubuntu-17-10
https://askubuntu.com/questions/993253/is-networkmanager-sending-http-requests-to-googleusercontent-com/1341377#1341377
https://forums.linuxmint.com/viewtopic.php?f=90&t=273558&p=1498037&hilit=mx.sygnow.net#p1498037
