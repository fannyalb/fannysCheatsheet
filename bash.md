# Shell/Bash
## Arrays
```bash
myArray=("This" "is" "an" "array")
for i in "${myArray[@]}"
do
	echo "$i"
done
```
## Pruefe ob Directory existiert
```bash
DIR=/ein/verzeichnis
if [ -d $DIR ] ; then
	echo "$DIR existiert"
fi
```

## Argumente auswerten
```bash
evaluate_args(){
	for i in "$@"
	do
		case $i in
			--debug)
				DEBUG=$TRUE
				shift
				;;
			--db=*)
				DB="${i#*=}"
				shift
				;;
			--dry)
				DRY=$TRUE
				DEBUG=$TRUE
				shift
				;;
		  *)
				usage
				;;
		esac
	done 
}
```
