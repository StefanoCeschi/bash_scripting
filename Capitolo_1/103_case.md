# Costrutto `case`

[🏠 Home page](./../readme.md)

Il `case` è similo allo `switch` ma con delle particolarità, tra cui il confronto a *pattern-matching*.

### Esempio
```bash
case ${info} in
    d*) #se inizia per "d"
        echo "Directory ${el}";;
    b*)
        echo "Periferica a blocchi (disco): ${el}";;
    c*)
        echo "Periferica a caratteri: ${el}";;
    *)
        echo "File: ${el}";;
esac
```