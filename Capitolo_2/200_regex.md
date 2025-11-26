# Espressioni Regolari (`RegEx`)

## Introduzione
Una `RegEx` è una stringa che permette di eseguire un match in una stringa. Quindi tramite un'*espressione* è possible validare - esempio - un indirizzo email.

## Pattern

### Testo usato negli esempi
> *"Era una mattina nebbiosa quando la classe I1A si ritrovò catapultata nel misterioso Regno delle Espressioni Regolari.
Il primo ostacolo fu attraversare il Villaggio degli Email, dove ogni casa aveva un cartello con scritte strane come alice.wonderland@fantasy.com, marco.rossi@scuola.it, heidi@alpi.ch, info@open-source.org e karl.schmidt@berlin.de. «Se non scrivete la formula giusta, non potrete passare!» urlò il guardiano, un vecchio punto interrogativo che si grattava la testa. Dopo vari tentativi, gli studenti riuscirono a trovare la magia corretta e il portale si aprì con un suono di campanelli. Tutti esultarono.
Proseguendo, arrivarono nella Foresta dei Numeri, dove gli alberi avevano inciso sui tronchi strani codici come 345 678 9012, 1234567890, 987 654 3210 e 555 123 4567. Tra le radici spuntavano anche anni misteriosi: 1999, 2025, 1984, 3000. Per uscire, dovevano catturare solo i numeri di telefono di dieci cifre, ignorando gli anni. Dopo mille tentativi, la foresta si illuminò di luce verde e il sentiero si aprì.*"

### Base
Tutte le espressioni devono avere questa base: `/<espr>/[flags]`, dove i flags possono essere:
 - g  = global (trova tutte le occorrenze)
 - i  = ignore case (case–insensitive)
 - m  = multiline (^ e $ funzionano per ogni riga)
 - s  = dotAll (. cattura anche newline)
 - u  = unicode (supporto UTF-16 completo)
 - y  = sticky (match solo dalla posizione corrente)
 - d  = indices (restituisce le posizioni dettagliate)

### Espressioni
 - `a`: corrispondenza con il *carattere* `a`
 - `abc`: corrispondenza con la *sequenza* `abc`
 - `[abc]`: corrispondenza con *un carattere* tra `a`, `b`, `c`
 - `[^abc]`: corrispondenza con *un carattere **diverso*** da `a`, `b`, `c`
 - `[a-f xyz]`: corrispondenza con i *caratteri* tra `a–f` oppure tra `x`, `y`, `z`
 - `\d`: corrispondenza con i *digit* (0–9) → equivalente a `[0-9]`
 - `\D`: corrispondenza **diversa** dai digit → equivalente a `[^0-9]`
 - `\w`: corrispondenza con caratteri *alfanumerici* (lettere, numeri, underscore) → `[A-Za-z0-9_]`
 - `\W`: corrispondenza **diversa** da caratteri alfanumerici → `[^A-Za-z0-9_]`
 - `\s`: corrispondenza con gli *spazi bianchi* (spazio, tab, newline, ecc.)
 - `.`: qualsiasi carattere (uno solo), **tranne `\n`** a meno che non si usi il flag `s`
 - `\b`: **word boundary**, confine tra *carattere di parola* e *non di parola*
 - `\B`: **non-word boundary**, posizione che **non** è un confine di parola

### Usati come condizione
- `\S`: corrispondenza **diversa** dagli *spazi bianchi*
- `\A`: inizio della stringa (in Python/PCRE; in JS si usa `^`)
- `\Z`: fine della stringa (in Python/PCRE; in JS si usa `$`)

### Altri casi
 - `are?`: `ar` è obbligatorio, però matcha ancha `are` (la `e` è facoltativa)
 - `a(re)*`: `a` è obbligatorio. `re` è facoltativo ma può essere ripetuto *n* volte. La parola *imparerete* eseguirebbe un match corretto
 - `a(re)+`: trova "a" seguita da una o più ripetizioni di "re", ma in modalità lazy → prende il MINIMO possibile.