# Lezione 1 / Date

## Basi
Questo semplice script calcola l'età dell'utente:
```bash
#eta.sh
#!/bin/bash
read -p "In che anno sei nato?" annoNascita
annoCorrente=$(date +"%Y") #Formatto la data per avere solo l'anno
eta=$(expr ${annoCorrente} - ${annoNascita})
echo "Allora hai $eta anni!"
#endfile

$ ./eta.sh
> In che anno sei nato? 2005
> Allora hai 20 anni!
```
