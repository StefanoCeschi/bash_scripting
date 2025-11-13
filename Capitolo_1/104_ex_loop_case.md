# Esempio script completo (000 - 103)

[🏠 Home page](./../readme.md)

### fileSearch.sh
```bash
#!/bin/bash

directory=$1
if [ -z "${directory}" ]; then
    directory="."
fi

for el in $(ls $directory); do
    info=$(ls -ld $directory/$el | cut -d' ' -f1)
    case ${info} in
        d*)
            echo "Directory ${el}" #se inizia per d
            echo "Tipo: directory";;
        b*)
            echo "File: ${el}" #se inizia per b
            echo "Tipo: periferica a blocchi (disco)";;
        c*)
            echo "File: ${el}" # se inizia per c
            echo "Tipo: Periferica a caratteri";;
        *)
            echo "File: ${el}" #tutto il resto (come un default)
            echo "Tipo: file";;
    esac
    owner=$(stat -c"%U" ${directory}/${el})
    group=$(stat -c"%G" ${directory}/${el})
    echo "Proprietario: ${owner}"
    echo "Gruppo: ${group}"
    echo ""
done
```