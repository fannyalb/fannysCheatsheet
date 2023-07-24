# Linux cmds
### GROUP BY substring of filename
* Quasi sowas wie `SELECT count(*), SUBSTR(filename, 0, 7) FROM current_dir GROUP BY SUBSTR(filename,0, 7)`

```sh
for dat in $(ls) ; do echo ${dat:0:7} ; done | sort -n | uniq -c
```

### find
```sh
find . -mtime -3  # Modification Time < 3 Tage
find . -mtime +2  # Modification Time > 2 Tage
find . -mtime -2 -exec mv "{}" /dest/dir \; # Mv all files older Than 2 days to /dest/dir
find  ./ -type d \( -path ./AppData \)  -prune -false -o -name '*.txt' # Alle .txt-Dateien ausser in ./AppData
```
### awk

```sh
awk '{ print $1, $2 }' inventory-shipped
```


### sed
#### Replace foo with bar in somefile.txt
```sh
sed -i 's/foo/bar/g' somefile.txt                 # find and replace foo with bar in somefile.txt
```

#### Variables in sed
```sh
# If you want to use variables into the sed,  use double quotes instead of single quotes
sudo sed -i "s|^GRUB_DEFAULT=.*$|GRUB_DEFAULT=\"$win_location\"|g" /etc/default/grub
```

#### Join 2 lines after a pattern

```sh
sed -n '/pattern/ {s/.*//; N; N; s/\n//g; p;}'
```

* `/pattern/` matches pattern and executes the brace block `{ }`.
* `s/.*//` deletes pattern from pattern space, a shorter but more obscure way of getting rid of pattern is to exchange pattern space and hold space with the x command.
* `N` takes next line from input file and appends it to pattern space.
* `s/[\r\n]//g` removes all newlines and carriage returns from pattern space.
* `p` prints pattern space.
* A slightly shorter solution for combining 3 lines is:
  ```sh
  sed -n '/pattern/ {x; N; N; s/\n//g; p;}'
  ```

### Other
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
