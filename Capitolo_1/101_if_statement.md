# If statement
[🏠 Home page](./../readme.md)
## Utilizzo base
Come in altri linguaggi, il costrutto if, serve per eseguire del codice a più vie a dipendenza della condizione.
Esempio:
```bash
#!/bin/bash

function verifyArgsNumber {
    test $1 -eq 1
}

if ! verifyArgsNumber $#; then
    echo "error"
fi #<-- per chiudere l'if (o qualsiasi costrutto, si scrive il nome al contrario)
```

## Costrutto if ... else
Questo serve per far prendere **o una via, o l'altra**. Se la condizione è falsa (0), verrà eseguito il codice nell'*else*:
```bash
#!/bin/bash

#Function che verifica se un numero è intero
function isInteger {
    R=$(expr $1 + 1 2>/dev/null)
    if test -z "${R}"; then
        return 1 #false
    else
        return 0 #true
    fi
}
```

## Costrutto if .. elif
Come in Java, è possibile usare una struttura if .. else if:
```java
if (<condition>){
    doSomething();
}else if(<other_condition>){
    doOtherThings();
}
```
Questo esempio è in Java, in bash è comunque molto simile:
```bash
#!/bin/bash
if test "$1" = "-v"; then
    echo "EvenOdd version 1.2 beta"
    exit 0
elif ! isInteger $1; then
    echo "I can only evaluate integers!"
else
    mod=$(expr $1 % 2)
    test ${mod} -eq 0 && echo "Even"
    test ${mod} -ne 0 && echo "Odd"
fi
```
### Se eseguito
```bash
$ ./EvenOdd.sh -v
> IsInt version 1.2 beta
$ ./EvenOdd.sh 1.2
> I can only evaluate integers!
$ ./EvenOdd.sh 12
> Even
$ ./EvenOdd.sh 11
> Odd
```

## Condizione con test complesso
Negli esempi precedenti, il test era effettuato da una funzione oppure erano semplici. Esiste anche una versione "più standard" per test più complessi, esempio:
```bash
#!/bin/bash

if [ "$1" = "-v" ]; then
    echo "EvenOdd version 1.2 beta"
    exit 0
elif ! isInteger $1; then
    echo "I can only evaluate integers!"
else
    mod=$(expr $1 % 2)
    test ${mod} -eq 0 && echo "Even"
    test ${mod} -ne 0 && echo "Odd"
fi

```

## Condizioni multiple
È possibile avere più condizioni con AND o OR:
```bash
if [ "$1" = "-v" ] || [ "$1" = "--version" ]; then
    echo "Print version info"
fi

if [ "$#" -eq 1 ] && [ "$1" = "-v" ]; then
    echo "Print version info with strict args number"
fi
```
[🏠 Home page](./../readme.md)