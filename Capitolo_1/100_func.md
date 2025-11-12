## Funzioni
Come per molti linguaggi, anche in bash sono presenti le funzioni (aka metodi / sottoprogrammi).
<br>
Riprendendo il programma che calcola se un numero fosse pari o dispari (vedi `002_expr_test.md`):

```bash
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
```
Questo script contiene codice ripetuto, **cosa che *non* va bene**! <br>
Per questo in questo capitolo si vedrà come sistemarlo.

### Diachiarazione funzione
È molto simile a JavaScript:

```bash
function nomeFunction{
    echo "HelloFunction!"
}
```

### Richiamare una funzione e parametri
Non è possibile *dichiarare* dei parametri, è poerò possibile *passarglieli* tramite il **$**, un po' come gli argomenti di uno script:

```bash
function sayHi{
    echo "Hi $0!"
}

sayHi "Marco"
```

## Esempio
```bash
#!/bin/bash

# funzione per uscire da programma con parametro n. exit
function mostraErroreEsci{
    echo "utilizzo: $0 <numero>" >$2
    exit $1
}
function verificaNumeroArgomenti{
    test $1 -eq 1 # con boolean il return sarà il risultato (0 se true)

    # default return 0
}

# Verifica argomenti != 1, nel caso esegue solo la prima riga.
verificaNumeroArgomentiErrato $# || mostraErroreEsci 1

# Verifica se parametro -v nel caso ritorno versione
test "${1}" = "-v" && echo "$0 v1.0" && exit 0 

# v1 Verifica argomento != <String> + exit su 2 linee
expr $1 + 1 &>/dev/null || echo "Utilizzo: $0 <numero>" >&2
expr $1 + 1 &>/dev/null || mostraErroreEsci 2

# v2 Verifica argomento != <String> + exit su 1 linea
test -z "$(expr $1 + 1)" && echo "Utilizzo: $0 <numero>" >&2 && mostraErroreEsci 2

resto=$(expr $1 % 2)
test ${resto} -eq 0 && echo "Pari"
test ${resto} -ne 0 && echo "Dispari"
```