# Linux cmds
#### find
```sh
find . -mtime -3  # Modification Time < 3 Tage
find . -mtime +2  # Modification Time > 2 Tage
find . -mtime -2 -exec mv "{}" /dest/dir \; # Mv all files older Than 2 days to /dest/dir
```

#### Other
```sh
sed -i 's/foo/bar/g' # find and replace

awk '{print $1}'

uniq 	# remove duplicates

wc -l Zeilen zaehlen

grep -i "suche case InSenSitIV"

sed -i 's/old-text/new-text/g' fileToEdit.txt
```


