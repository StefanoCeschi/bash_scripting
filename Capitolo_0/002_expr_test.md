## Il comando expr
Questo comando serve per calcolare espressioni matematiche, visto che non è possibile eseguirle direttamente in shell.

```bash
$ expr 3 + 3
> 6
```

### Nota bene
Questo comando funziona **solo** con numeri interi!

## Il comando test
Questo comando viene usato per eseguire dei test su delle variabili:
- = (uguale per le stringhe)
- -eq (uguale per i numeri)
- -ge (\>=)
- -le (\<=)
- -lt (\<)
- -gt (\>)
- != (!= per le stringhe)
- -ne (!= per numeri)
- -ot (più vecchio di [sui file])
- -n (verifica che la lungh. della stringa non sia 0)
- -z (verifica che la lungh. della sringa sia 0)

### Come usarlo
Questo comando viene usato in *concatenazione* con altri comandi, esempio:
```bash
$ test 1 -eq 1 && echo "OK"
> OK
$ test "ciao" = "ciao2" && echo "OK"
> 
$ test
```

### Attenzione
Il parametro -n è un po' particolare: <br>
Se uso una variabile che non esiste ritorna **sempre** `true`!
```bash
$ echo $uname
> 
$ test -n $uname && echo "Ok"
> Ok
```

## Script di esempio
```bash
#evenOdd.sh----

#!/bin/bash
#If $1 is not given
test $# -ne 1 && echo "Use: $0 <number>" >&2 && exit 1

#Check and give result
R=$(expr $1 + 1 2>/dev/null)
test -z "${R}" && echo "Use: $0 <number>" >&2 && exit 2

#Calculate
mod=$(expr $1 % 2)
test ${mod} -eq 0 && echo "Even"
test ${mod} -ne 0 && echo "Odd"


#endfile----

$ ./evenOdd.sh 4
> Even
$ ./evenOdd.sh 3
> Odd
$ ./evenOdd.sh
> Use: ./evenOdd.sh <number>
$ ./evenOdd.sh sasso
> Use: ./evenOdd.sh <number>
```