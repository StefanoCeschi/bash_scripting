# Espressioni Regolari (`RegEx`)

[🏠 Home page](./../readme.md)

## Introduzione
Una `RegEx` è una stringa che permette di eseguire un match in una stringa. Quindi tramite un'*espressione* è possible validare - esempio - un indirizzo email.

## Pattern

### Base
In JavaScript, le espressioni regolari hanno la forma:
/\<espressione>/\<flags>

I flags disponibili:

 - g  = global (trova tutte le occorrenze)
 - i  = ignore case (case–insensitive)
 - m  = multiline (^ e $ funzionano per ogni riga)
 - s  = dotAll (. cattura anche newline)
 - u  = unicode (supporto UTF-16 più completo, abilita \p{})
 - y  = sticky (match solo dalla posizione corrente)
 - d  = indices (restituisce anche le posizioni [start, end])

! Attenzione: questa sintassi è valida SOLO in JavaScript

---

### Espressioni
 - `a`: corrispondenza con il carattere `a`
 - `abc`: corrispondenza con la sequenza `abc`
 - `[abc]`: un carattere tra `a`, `b`, `c`
 - `[^abc]`: un carattere diverso da `a`, `b`, `c`
 - `[a-fxyz]`: un carattere da `a` a `f` OPPURE uno tra `x`, `y`, `z`
   (attenzione: non esiste un intervallo "xyz", sono tre caratteri)
 - `\d`: digit (`[0-9]`)
 - `\D`: non-digit (`[^0-9]`)
 - `\w`: alfanumerici + underscore (`[A-Za-z0-9_]`)
 - `\W`: tutto ciò che NON è \w (`[^A-Za-z0-9_]`)
 - `\s`: spazi bianchi (spazio, tab, newline, ecc.)
 - `\S`: carattere non di spazio bianco
 - `.`: qualsiasi carattere tranne il newline (a meno che non ci sia il flag `s`)
 - `\b`: word boundary (ma in JS funziona solo con caratteri ASCII/underscore)
 - `\B`: non-word boundary (stesse limitazioni di \b)
 - `\A`: inizio stringa (NON valido in JS)
 - `\Z`: fine stringa (NON valido in JS)
 - `^`: inizio riga (o inizio stringa senza flag m)
 - `$`: fine riga (o fine stringa senza flag m)

---

### Quantificatori
 - `•?`      : • è opzionale (0 o 1 volta)
 - `•+`      : • una o più volte (greedy)
 - `•*`      : • zero o più volte (greedy)
 - `•+?`     : • una o più volte (lazy)
 - `•*?`     : • zero o più volte (lazy)
 - `•??`     : 0 o 1 volta (lazy)
 - `•{N}`    : esattamente N volte
 - `•{N,M}`  : da N a M volte
 - `•{N,}`   : almeno N volte
 - `•{,M}`   : al massimo M volte (NON standard → usare `•{0,M}`)
 - `▲|◆`     : alternativa, "▲ oppure ◆"
 - `( … )`   : gruppo (catturante)
 - `(?: … )` : gruppo NON catturante

---

### Greedy vs Lazy (Quantificatori)
I quantificatori nelle regex possono comportarsi in due modi:

#### GREEDY (predefinito)
Sono i quantificatori normali: `*`, `+`, `?`, `{n,m}`, `{n,}`, ecc.

Comportamento:
 - cercano di prendere **il massimo possibile**
 - poi, solo se necessario, "restituiscono" caratteri (backtracking)
 - sono il comportamento di default in TUTTE le regex

Esempio:
  Pattern:   `a.+c`
  Testo:     `abbbbbc c`
  Risultato: matcha fino all'ULTIMA `c`

Il `.+` è greedy → si espande il più possibile, poi si ferma quando trova una `c` che chiude il match.


#### LAZY (o NON-GREEDY)
Versioni "pigre" dei quantificatori: `*?`, `+?`, `??`, `{n,m}?`, `{n,}?`

Comportamento:
 - cercano di prendere **il minimo possibile**
 - poi, solo se necessario, si espandono
 - vengono usati quando vuoi il match più corto

Esempio:
  Pattern:   `a.+?c`
  Testo:     `abbbbbc c`
  Risultato: matcha fino ALLA PRIMA `c`

Qui `.+?` prende il minimo indispensabile per chiudere il match.


#### Sintesi:
 - Greedy → "prendo tutto, poi vedo se va bene"
 - Lazy   → "prendo il minimo, poi allargo"

---

### Esempi comuni di regex (con spiegazione e match attesi)

#### 1) Email semplice
Regex: `/[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$/i`

Matcha esempi tipo:
 - mario.rossi@gmail.com
 - info@azienda.it
 - supporto@open-source.org

Non matcha:
 - mario@@gmail.com
 - email SENZA dominio
 - testo senza @


#### 2) Numero di telefono italiano (10 cifre)
Regex: `/\b\d{10}\b/`

Matcha:
 - 3928475610
 - 0551234567

Non matcha:
 - 12345
 - 123 456 7890
 - 1999 (è troppo corto)


#### 3) Numero di telefono formattato con spazi
Regex: `/\b\d{3} \d{3} \d{4}\b/`

Matcha:
 - 345 678 9012
 - 555 123 4567

Non matcha:
 - 3456789012
 - 555 1234 567


#### 4) Parole di 4 lettere
Regex: `/\b\w{4}\b/`

Matcha:
 - casa
 - mare
 - test

Non matcha:
 - cane! (il ! tronca la parola)
 - gatti (5 lettere)
 - io (2 lettere)


#### 5) Parole che finiscono in “are”
Regex: `/\b\w+are\b/`

Matcha:
 - cantare
 - programmare
 - imparare

Non matcha:
 - cane
 - area
 - ar


#### 6) Data nel formato GG-MM-AAAA
Regex: `/\b\d{2}-\d{2}-\d{4}\b/`

Matcha:
 - 01-01-2020
 - 31-12-1999

Non matcha:
 - 1-01-2020
 - 01/01/2020


#### 7) Solo numeri (una o più cifre)
Regex: `/^\d+$/`

Matcha:
 - 12345
 - 007
 - 999999

Non matcha:
 - 12a34
 - " 123 "
 - 123.45


#### 8) Codice postale USA (5 cifre)
Regex: `/^\d{5}$/`

Matcha:
 - 90210
 - 10001

Non matcha:
 - 1234
 - 123456
 - 12 345


#### 9) URL semplice (http/https)
Regex: `/(https?):\/\/[^\s]+/`

Matcha:
 - http://example.com
 - https://www.sito.it/page?id=5

Non matcha:
 - www.google.com (manca http)
 - ftp://server (altro protocollo)


#### 10) Solo lettere (ASCII)
Regex: `/^[A-Za-z]+$/`

Matcha:
 - Hello
 - test
 - RegEx

Non matcha:
 - caffè (accento → non ASCII)
 - hello123
 - _test


#### 11) Parole che iniziano con una maiuscola
Regex: `/\b[A-Z][a-z]*\b/`

Matcha:
 - Marco
 - Italia
 - Computer

Non matcha:
 - MARCO
 - marco
 - 3DPrinter


#### 12) Catturare contenuto tra virgolette
Regex: `/\"(.*?)\"/g` (lazy)

Matcha:
 - "ciao"
 - "test di esempio"

Non matcha:
 - ciao"test"

---

[🏠 Home page](./../readme.md)