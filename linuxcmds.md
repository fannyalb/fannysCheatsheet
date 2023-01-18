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


#### sed
```sh
# If you want to use variables into the sed,  use double quotes instead of single quotes

sed -i 's/foo/bar/g' somefile.txt                 # find and replace foo with bar in somefile.txt
sudo sed -i "s|^GRUB_DEFAULT=.*$|GRUB_DEFAULT=\"$win_location\"|g" /etc/default/grub
``` 

#### Other
```sh

awk '{print $1}' soefilewithcolumnd               # Print first Column

uniq 	                                            # remove duplicate lines

wc -l                                             # Zeilen zaehlen

grep -i "suche case InSenSitIV"
```

### NGINX Accesslogsuche
 * Relevante Spalten
```sh 
awk '{ print $1, $4, $27, $28, $7}' access.log
```
* Datum besser formatieren `[18/Jan/2023:06:25:04 +0100]` -> `17-01-2023 06:25`
```sh
sed 's/\[17\/Jan\/2023:\([0-9]*\)/17-01-2023 \1/g' access.log | sed -re 's/([0-9]{2}:[0-9]{2}):[0-9]{2} /\1 /g'
