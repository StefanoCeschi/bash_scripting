# Le stringhe
[🏠 Home page](./../readme.md)
## Operazioni
Avendo le seguenti stringhe: 
- `msg="Ciao!"`
- `fn1=Sasso.tar.gz`

Possono essere eseguite le seguenti operazioni:

- Lunghezza: `${#msg}`
- Substring: `${msg:3}` -> `o!`
- Substring: `${msg:1:2}` -> `ia`
- Sostituzione: `${msg/ia/IA}`  -> `cIAo!`
- Sostuzione (tutte le occorrenze): `${msg//o/O}` -> `CiaO!`
- Sostituzione con *globbing*: `${msg/[a-z]/[A-Z]}` -> `CIAO!`  
- Rimozione (occorrenza più corta da **sx**): `${msg#C?a}` -> `o!`
- Rimozione (occorrenza più lunga da **sx**): `${msg##C?a}` -> `o!`
- Rimozione (occorrenza più corta da **dx**): `${fn1%.*}` -> `Sasso.tar`
- Rimozione (occorrenza più lunga da **dx**): `${fn1%%.*}` -> `Sasso`
- To Upper Case (prima lettera): `${msg^}` -> `Ciao!`
- To Upper Case: `${msg^^}` -> `CIAO!`
- To lower case (prima lettera): `${msg,}` -> `ciao!`
- To lower case: `${msg,,}` -> `ciao!`
- Inversione del caso (prima): `${msg~}` -> `ciao!` 
- Inversione del caso (tutte): `${msg~~}` -> `cIAO!` 

[🏠 Home page](./../readme.md)