# Shell/Bash

## Redirection
Two key things to notice: > means redirection operator, where we open a file and 2 integer stands for stderr file descriptor; in fact this is exactly how POSIX standard for shell language defines redirection.
For simple `>` redirection, the `1` integer is implied for stdout, i.e. `echo Hello World > /dev/null` is just the same as `echo Hello World 1>/dev/null`. Note, that the integer or redirection operator cannot be quoted, otherwise shell doesn't recognize them as such, and instead treats as literal string of text. As for spacing, it's important that integer is right next to redirection operator, but file can either be next to redirection operator or not, i.e. `command 2>/dev/null` and `command 2> /dev/null` will work just fine.

Redirect stdout to one file and stderr to another file:
```sh
command > out 2>error
```

Redirect stdout to a file (>out), and then redirect stderr to stdout (2>&1):
```sh
command >out 2>&1
```

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
