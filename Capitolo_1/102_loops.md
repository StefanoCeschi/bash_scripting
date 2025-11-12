# Loops
[🏠 Home page](./../readme.md)

I loop servono per ripetere del codice secondo una certa condizione.

## While + shift sugli argomenti
```bash
#!/bin/bash
while [ $# -ne 0 ]; do
    resto=$(expr $1 %2)
    if [ ${resto} -eq 0 ]; then
        echo "${1}: Pari"
    else
        echo "${1}: Dispari"
    fi
    shift
done
```

### Shift
Lo `shift` sposta a sinistra i parametri posizionali, ovvero gli argomenti di uno script, perdendo il primo argomento ad ogni esecuzione. È utile per elaborare gli argomenti in un ciclo, scartando quelli già utilizzati. È possibile specificare un numero per spostare più posizioni contemporaneamente (es. `shift 2`)

## For
Il ciclo for è un ciclo con contatore.
```bash
#Ciclo da 1 a 4 stampando la variabile i
$ for i in $(seq 1 4); do echo "Valore: $i"; done
> Valore: 1
> Valore: 2
> Valore: 3
> Valore: 4

#Ciclo tutti i file che hanno estensione .sh e stampo il nome
$ for f in *.sh; do echo "Script: $f"; done
> Script: example.sh
> Script: example2.sh
> Script: dog.sh
```
### Ciclare gli argomenti di uno script
```bash
for arg in $@; do
    if ! isInt $arg; then
        echo "Number ($arg) not an integer"
    else
        echo evenOdd $arg
    fi
done
```

[🏠 Home page](./../readme.md)