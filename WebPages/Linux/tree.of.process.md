
```
$ pstree -p | grep firefox
           |               |               |                    |-mate-panel(1970)-+-firejail(9589)---firejail(9592)---firefox-bin(+


$ pstree -ps 9592
systemd(1)───lightdm(1281)───lightdm(1793)───mate-session(1825)───mate-panel(1970)───firejail(9589)───firejail(959+


$ reset ; pstree -p 9592
firejail(9592)───firefox-bin(9601)─┬─Isolated Web Co(11338)─┬─{Isolated Web Co}(11342)
                                   │                        ├─{Isolated Web Co}(11343)
                                   │                        ├─{Isolated Web Co}(11344)
                                   │                        ├─{Isolated Web Co}(11345)
                                   │                        ├─{Isolated Web Co}(11346)
                                   │                        ├─{Isolated Web Co}(11347)
                                   │                        ├─{Isolated Web Co}(11348)
                                   │                        ├─{Isolated Web Co}(11349)
                                   │                        ├─{Isolated Web Co}(11350)

$ ps -eo size,pid,user,command --sort -size |     awk '{ hr=$1/1024 ; printf("%13.2f Mb ",hr) } { for ( x=2 ; x<=NF ; x++ ) { printf("%s ",$x) } print "" }' |    cut -d "" -f2 | cut -d "-" -f1 | grep firefox | awk '{ sum += $1 } END { print sum }'
5316.81


$ pstree -p | grep min
           |-mate-terminal(25639)-+-bash(25645)
           |                      |-bash(25831)---min(25837)-+-min(25840)---min(25878)-+-min(25910)
           |                      |                          |                         |-{min}(25911)
           |                      |                          |                         |-{min}(25912)
...


$ ps -eo size,pid,user,command --sort -size |     awk '{ hr=$1/1024 ; printf("%13.2f Mb ",hr) } { for ( x=2 ; x<=NF ; x++ ) { printf("%s ",$x) } print "" }' |    cut -d "" -f2 | cut -d "-" -f1 | grep min 
       742.48 Mb 26001 user /home/user/Download/test/min_1.23.0_amd64/usr/lib/min/min 
       430.82 Mb 25885 user /home/user/Download/test/min_1.23.0_amd64/usr/lib/min/min 
       381.68 Mb 25878 user /home/user/Download/test/min_1.23.0_amd64/usr/lib/min/min 
       351.72 Mb 26238 user /home/user/Download/test/min_1.23.0_amd64/usr/lib/min/min 
       332.89 Mb 25837 user /home/user/Download/test/min_1.23.0_amd64/usr/lib/min/min 
...


$ ps -eo size,pid,user,command --sort -size |     awk '{ hr=$1/1024 ; printf("%13.2f Mb ",hr) } { for ( x=2 ; x<=NF ; x++ ) { printf("%s ",$x) } print "" }' |    cut -d "" -f2 | cut -d "-" -f1 | grep min | awk '{ sum += $1 } END { print sum }'
3359.83

```

"grep firefox" can also display e.g. the file /firefox/file opened in the text editor.
So the measurement will not always be correct


Used:
1.  <https://stackoverflow.com/questions/131303/how-can-i-measure-the-actual-memory-usage-of-an-application-or-process>
2.  <https://stackoverflow.com/questions/2702564/how-can-i-quickly-sum-all-numbers-in-a-file>

