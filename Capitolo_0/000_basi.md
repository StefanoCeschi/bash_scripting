# Lezione 1 / basi

## Creazione script
Gli script bash hanno l'estensione `.sh` e devono avere il seguente header:
```bash
#!/bin/bash
```
Prima di eseguire lo script è necessario modificare i permessi per poter permette *l'esecuzione*: `chmod +x \<file>`.

## Questione di spazi
Prestare attenzione agli spazi! <br>
`valore=3` assegna il valore 3 alla variabile *valore*.
Se invece scrivessi `valore = 3` darebbe il seguente errore:
 ```bash 
 valore: command not found
```

## Variabili
Nello script posso dichiarare/assegnare una variabile in modo molto semplice: <br>
```bash
username=""
read username
echo "$username"
```

## Escaping
Quando si vuole **concatenare una variabile** basta inserirla negli apici:
```bash
echo "Ciao, $nome"
```
Se però si volesse stampare il nome senza sostituirla?
```bash
echo "La variabile \$nome, è: $nome"
```

## Argomenti
Possono essere passati degli `args` in stile Java:
```bash
#args.sh
#!/bin/bash
echo "\$0=$0"
echo "\$1=$1"
echo "\$2=$2"
echo "\$3=$3"
#endfile
```

Quello che questo codice fa è leggere gli argomenti, producendo il seguente output: <br>
```shell
$ ./comando.sh A B C
> $0=../path/relativo/comando.sh
> $1=A
> $2=B
> $3=C
```

## Sostituzione
Posso usare l'output di un comando all'interno di uno script:
```bash
#uname.sh
#!/bin/bash
uname=$(whoami)
echo "Scrivi il tuo nome: "
read name
echo "Ciao, $name! Il tuo username è $uname!"
#endfile

$ whoami
> steceschi

$ ./uname.sh
> Scrivi il tuo nome:
> Ste
> Ciao Ste! Il tuo username è steceschi
```

## Comandi utili
 - read [nome variabile] -> Legge da `stdin`
 - $0, $1, $2, ... -> Argomenti
 - expr \<numero> \<segno> \<numero2> -> serve a fare operazioni matematiche. SOLO CON INTERI

## Ulteriori note
### read
È possibile passare i dati al read tramite la *ridirezione*, esempio:
```bash
#redir.sh
#!/bin/bash
echo "Come ti chiami? "
read $name
echo "Benvenuto, $name"
#endfile

$ echo "Ste" | ./redir.sh
> Benvenuto, Ste
```