# Tools
## iostat
## iotop
## dstat
## atop
## ioping

## Disk performances

To get the read speed 
```
hdparm -t /dev/sdb
```


To get the write speed
```
dd count=1k bs=1M if=/dev/zero of=/media/HD2/test.img
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB) copied, 7.69365 s, 140 MB/s
```
