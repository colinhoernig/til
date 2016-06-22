# List top 10 largest directories
_06/22/2016_

Every once in a I need a quick way to view, at a glance, the largest directories
in a filesystem.  I've found this command to be very useful.  Make sure GNU/sort \
is installed.

```bash
cd /
du -hsx * | sort -rh | head -10 # you may need sudo
```

```
4.4G  var
668M  usr
92M lib
18M boot
8.7M  bin
8.2M  sbin
7.0M  etc
256K  tmp
236K  run
68K home
```
