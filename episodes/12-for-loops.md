---
title: Per i cicli
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare a cosa servono normalmente i cicli **for**.
- Tracciare l'esecuzione di un ciclo semplice (non annidato) e indicare correttamente i
  valori delle variabili in ogni iterazione.
- Scrivere cicli **for** che utilizzano lo schema Accumulator per aggregare valori.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso fare in modo che un programma faccia molte cose contemporaneamente?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Un ciclo *for* esegue i comandi una volta per ogni valore di un insieme.

- Fare calcoli sui valori di un elenco uno per uno è doloroso come lavorare con
  `pressure_001`, `pressure_002`, ecc.
- Un ciclo *for* dice a Python di eseguire alcune istruzioni una volta per ogni valore
  di una lista, di una stringa di caratteri o di un altro insieme.
- "per ogni cosa in questo gruppo, fare queste operazioni"

```python
for number in [2, 3, 5]:
    print(number)
```

- Questo ciclo `for` è equivalente a:

```python
print(2)
print(3)
print(5)
```

- E l'output del ciclo `for` è:

```output
2
3
5
```

## Un ciclo `for` è composto da un insieme, una variabile del ciclo e un corpo.

```python
for number in [2, 3, 5]:
    print(number)
```

- L'insieme, `[2, 3, 5]`, è quello su cui viene eseguito il ciclo.
- Il corpo, `print(number)`, specifica cosa fare per ogni valore dell'insieme.
- La variabile del ciclo, `number`, è quella che cambia a ogni *iterazione* del ciclo.
  - La "cosa corrente".

## La prima riga del ciclo `for` deve terminare con i due punti e il corpo deve essere indentato.

- I due punti alla fine della prima riga indicano l'inizio di un *blocco* di istruzioni.
- Python usa l'indentazione piuttosto che `{}` o `begin`/`end` per mostrare il
  *nesting*.
  - Qualsiasi rientro coerente è legale, ma quasi tutti usano quattro spazi.

```python
for number in [2, 3, 5]:
print(number)
```

```error
IndentationError: expected an indented block
```

- L'indentazione è sempre significativa in Python.

```python
firstName = "Jon"
  lastName = "Smith"
```

```error
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName = "Smith"
    ^
IndentationError: unexpected indent
```

- Questo errore può essere risolto rimuovendo gli spazi extra all'inizio della seconda
  riga.

## Le variabili di loop possono essere chiamate in qualsiasi modo.

- Come tutte le variabili, le variabili del ciclo sono:
  - Create su richiesta.
  - Senza senso: i loro nomi possono essere qualsiasi cosa.

```python
for kitten in [2, 3, 5]:
    print(kitten)
```

## Il corpo di un ciclo può contenere molte istruzioni.

- Ma nessun ciclo dovrebbe essere lungo più di qualche riga.
- È difficile per gli esseri umani tenere a mente pezzi di codice più grandi.

```python
primes = [2, 3, 5]
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
```

```output
2 4 8
3 9 27
5 25 125
```

## Usare `range` per iterare su una sequenza di numeri.

- La funzione built-in [`range`](https://docs.python.org/3/library/stdtypes.html#range)
  produce una sequenza di numeri.
  - *Non* un elenco: i numeri sono prodotti su richiesta per rendere più efficiente il
    looping su intervalli di grandi dimensioni.
- `range(N)` sono i numeri 0..N-1
  - Esattamente gli indici legali di un elenco o di una stringa di caratteri di
    lunghezza N

```python
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
```

```output
a range is not a list: range(0, 3)
0
1
2
```

## Lo schema Accumulatore trasforma molti valori in uno.

- Uno schema comune nei programmi è quello di:
  1. Inizializza una variabile *accumulatore* a zero, alla stringa vuota o all'elenco
     vuoto.
  2. Aggiorna la variabile con i valori di un insieme.

```python
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
```

```output
55
```

- Leggere `total = total + (number + 1)` come:
  - aggiunge 1 al valore corrente della variabile del ciclo `number`.
  - Aggiungetelo al valore corrente della variabile accumulatore `total`.
  - Assegna questo valore a `total`, sostituendo il valore corrente.
- Dobbiamo aggiungere `number + 1` perché `range` produce 0..9, non 1..10.

::::::::::::::::::::::::::::::::::::::: challenge

## Classificazione degli errori

Un errore di indentazione è un errore di sintassi o un errore di runtime?

::::::::::::::: solution

## Soluzione

Un IndentationError è un errore di sintassi. I programmi con errori di sintassi non
possono essere avviati. Un programma con un errore di runtime verrà avviato, ma in
determinate condizioni verrà lanciato un errore.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tracciamento dell'esecuzione

Creare una tabella che mostri i numeri delle righe che vengono eseguite durante
l'esecuzione di questo programma e i valori delle variabili dopo l'esecuzione di ogni
riga.

```python
total = 0
for char in "tin":
    total = total + 1
```

::::::::::::::: solution

## Soluzione

| Line no | Variables            |
| ------- | -------------------- |
| 1       | total = 0            |
| 2       | total = 0 char = 't' |
| 3       | total = 1 char = 't' |
| 2       | total = 1 char = 'i' |
| 3       | total = 2 char = 'i' |
| 2       | total = 2 char = 'n' |
| 3       | total = 3 char = 'n' |

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Inversione di una stringa

Riempite gli spazi vuoti del programma sottostante in modo che stampi "nit" (l'inverso
della stringa di caratteri originale "tin").

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

::::::::::::::: solution

## Soluzione

```python
original = "tin"
result = ""
for char in original:
    result = char + result
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Pratica di Accumulazione

Riempite gli spazi vuoti in ciascuno degli esercizi seguenti per produrre il risultato
indicato.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

::::::::::::::: solution

## Soluzione

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```

:::::::::::::::::::::::::

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

::::::::::::::: solution

## Soluzione

```python
lengths = []
for word in ["red", "green", "blue"]:
    lengths.append(len(word))
print(lengths)
```

:::::::::::::::::::::::::

```python
# Cooncatenare le parole: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

::::::::::::::: solution

## Soluzione

```python
words = ["red", "green", "blue"]
result = ""
for word in words:
    result = result + word
print(result)
```

:::::::::::::::::::::::::

**Creare un acronimo:** Partendo dalla lista `["red", "green", "blue"]`, creare
l'acronimo `"RGB"` usando un ciclo for.

**Consiglio:** Potrebbe essere necessario utilizzare un metodo stringa per formattare
correttamente l'acronimo.

::::::::::::::: solution

## Soluzione

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0].upper()
print(acronym)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Somma cumulativa

Riordinate e indentate correttamente le righe di codice sottostanti in modo da stampare
una lista con la somma cumulativa dei dati. Il risultato dovrebbe essere `[1, 3, 5,
10]`.

```python
cumulative.append(total)
for number in data:
cumulative = []
total = total + number
total = 0
print(cumulative)
data = [1,2,2,5]
```

::::::::::::::: solution

## Soluzione

```python
total = 0
data = [1,2,2,5]
cumulative = []
for number in data:
    total = total + number
    cumulative.append(total)
print(cumulative)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Errori di identificazione del nome della variabile

1. Leggete il codice qui sotto e cercate di identificare gli errori *senza* eseguirlo.
2. Eseguite il codice e leggete il messaggio di errore. Che tipo di `NameError` pensate
   che sia? Si tratta di una stringa senza virgolette, di una variabile scritta male o
   di una variabile che avrebbe dovuto essere definita ma non lo è stata?
3. Correggere l'errore.
4. Ripetete i passi 2 e 3, finché non avete risolto tutti gli errori.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

::::::::::::::: solution

## Soluzione

- I nomi delle variabili Python sono sensibili alle maiuscole e alle minuscole: `number`
  e `Number` si riferiscono a variabili diverse.
- La variabile `message` deve essere inizializzata come una stringa vuota.
- Vogliamo aggiungere la stringa `"a"` a `message`, non la variabile indefinita `a`.

```python
message = ""
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:
        message = message + "a"
    else:
        message = message + "b"
print(message)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Identificazione degli errori degli elementi

1. Leggete il codice qui sotto e cercate di identificare gli errori *senza* eseguirlo.
2. Eseguite il codice e leggete il messaggio di errore. Di che tipo di errore si tratta?
3. Correggere l'errore.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

::::::::::::::: solution

## Soluzione

Questa lista ha 4 elementi e l'indice per accedere all'ultimo elemento della lista è
`3`.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[3])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Un ciclo *for* esegue i comandi una volta per ogni valore di un insieme.
- Un ciclo `for` è composto da un insieme, una variabile del ciclo e un corpo.
- La prima riga del ciclo `for` deve terminare con i due punti e il corpo deve essere
  indentato.
- L'indentazione è sempre significativa in Python.
- Le variabili del loop possono essere chiamate in qualsiasi modo (ma si consiglia
  vivamente di dare un nome significativo).
- Il corpo di un ciclo può contenere molte istruzioni.
- Usare `range` per iterare su una sequenza di numeri.
- Lo schema Accumulatore trasforma molti valori in uno.

::::::::::::::::::::::::::::::::::::::::::::::::::



