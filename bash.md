@ Shell/Bash

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
