# Shell/Bash

## Prepend to Cmdline args

```bash
cmd argument1 argument2 "$@"
```

## Braces, Brackets, Parantheses
* Bei `if` fuer nur 1 boolsche Variable GAR KEINE KLAMMERN
* `[ ]` : Single brackets are used for comparison operations. In the past [ was a command like the unix test command.
* `[[ ]]`: Double brackets are also used for comparisons, but they expose a richer syntax which enables more testing and comparison operations
* `( )`: Single parenthesis call a sub-shell
* `(( ))`: Double parenthesis are used for arithmetic (demonstrated below)
* `{ }`: Single Braces can be used to:
Unambiguously identify variables
Define a sequence of commands for the current shell context

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
