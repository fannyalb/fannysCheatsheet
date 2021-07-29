# Linux cmds
#### GROUP BY substring of filename
* Quasi sowas wie `SELECT count(*), SUBSTR(filename, 0, 7) FROM current_dir GROUP BY SUBSTR(filename,0, 7)`

```sh
for dat in $(ls) ; do echo ${dat:0:7} ; done | sort -n | uniq -c
```

#### find
```sh
find . -mtime -3  # Modification Time < 3 Tage
find . -mtime +2  # Modification Time > 2 Tage
find . -mtime -2 -exec mv "{}" /dest/dir \; # Mv all files older Than 2 days to /dest/dir
find  ./ -type d \( -path ./AppData \)  -prune -false -o -name '*.txt' # Alle .txt-Dateien ausser in ./AppData
```
#### awk

```sh
awk '{ print $1, $2 }' inventory-shipped
```

#### Other
```sh
sed -i 's/foo/bar/g' somefile.txt                 # find and replace foo with bar in somefile.txt

cat soefilewithcolumnd | awk '{print $1}'         # Print first Column

uniq 	                                            # remove duplicate lines

wc -l                                             # Zeilen zaehlen

grep -i "suche case InSenSitIV"
```


