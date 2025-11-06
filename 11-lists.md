---
title: Elenchi
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare perché i programmi hanno bisogno di collezioni di valori.
- Scrivere programmi che creino elenchi semplici, li indicizzino, li suddividano (slice) e li modifichino tramite assegnazioni o chiamate a metodi.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come si possono memorizzare più valori?
  
::::::::::::::::::::::::::::::::::::::::::::::::::

## Un elenco memorizza molti valori in un'unica struttura.

- Fare calcoli con un centinaio di variabili chiamate `pressure_001`, `pressure_002`, ecc. sarebbe almeno altrettanto lento che farli a mano.
- Utilizzare un *elenco* per memorizzare molti valori insieme.
  - Racchiuso tra parentesi quadre `[...]`.
  - Valori separati da virgole `,`.
- Usare `len` per scoprire quanti valori ci sono in un elenco.

```python
pressures = [0.273, 0.275, 0.277, 0.275, 0.276]
print('pressures:', pressures)
print('length:', len(pressures))
```

```output
pressures: [0.273, 0.275, 0.277, 0.275, 0.276]
length: 5
```

## Usare l'indice di un elemento per recuperarlo da un elenco.

- Come le stringhe.

```python
print('zeroth item of pressures:', pressures[0])
print('fourth item of pressures:', pressures[4])
```

```output
zeroth item of pressures: 0.273
fourth item of pressures: 0.276
```

## I valori di un elenco possono essere sostituiti tramite assegnazione

- Utilizzare un'espressione di indice a sinistra dell'assegnazione per sostituire un valore.

```python
pressures[0] = 0.265
print('pressures is now:', pressures)
```

```output
pressures is now: [0.265, 0.275, 0.277, 0.275, 0.276]
```

## L'aggiunta di elementi a un elenco ne aumenta la lunghezza

- Usare `list_name.append` per aggiungere elementi alla fine di un elenco.

```python
primes = [2, 3, 5]
print('primes is initially:', primes)
primes.append(7)
print('primes has become:', primes)
```

```output
primes is initially: [2, 3, 5]
primes has become: [2, 3, 5, 7]
```

- `append` è un *metodo* delle liste.
  - È simile a una funzione, ma associato a un particolare oggetto.
- Usare `object_name.method_name` per chiamare i metodi.
  - Questo stile ricorda volutamente il modo in cui ci si riferisce agli elementi in una libreria.
- Nel corso della trattazione incontreremo altri metodi delle liste.
  - Utilizzare `help(list)` per un'anteprima.
- `extend` è simile a `append`, ma consente di combinare due elenchi. Ad esempio:

```python
teen_primes = [11, 13, 17, 19]
middle_aged_primes = [37, 41, 43, 47]
print('primes is currently:', primes)
primes.extend(teen_primes)
print('primes has now become:', primes)
primes.append(middle_aged_primes)
print('primes has finally become:', primes)
```

```output
primes is currently: [2, 3, 5, 7]
primes has now become: [2, 3, 5, 7, 11, 13, 17, 19]
primes has finally become: [2, 3, 5, 7, 11, 13, 17, 19, [37, 41, 43, 47]]
```

Si noti che mentre `extend` mantiene la struttura "piatta" dell'elenco, l, aggiungere un elenco a un altro fa sì che l’ultimo elemento di `primes` ssia a sua volta un elenco, non un intero.
Gli elenchi possono contenere valori di qualsiasi tipo; sono quindi possibili elenchi di elenchi.

## Usare `del` per rimuovere completamente un elemento da una lista.

- Si usa `del list_name[index]` per rimuovere un elemento da una lista (nell'esempio, 9
  non è un numero primo) e quindi accorciarlo.
- `del` non è una funzione o un metodo, ma un’istruzione del linguaggio.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
```

```output
primes before removing last item: [2, 3, 5, 7, 9]
primes after removing last item: [2, 3, 5, 7]
```

## La lista vuota non contiene valori.

- Utilizzare `[]` da solo per rappresentare una lista che non contiene valori.
  - "Lo zero della lista"
- Utile come punto di partenza per la raccolta di valori (che vedremo nel [prossimo
  episodio](12-for-loops.md)).

## Le liste possono contenere valori di tipi diversi.

- Una singola lista può contenere numeri, stringhe e qualsiasi altra cosa.

```python
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
```

## Le stringhe di caratteri possono essere indicizzate come le liste.

- Ottenere singoli caratteri da una stringa di caratteri utilizzando gli indici tra
  parentesi quadre.

```python
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
```

```output
zeroth character: c
third character: b
```

## Le stringhe di caratteri sono immutabili.

- Non è possibile modificare i caratteri di una stringa dopo la sua creazione.
  - *Immutabile*: non può essere modificato dopo la creazione.
  - Al contrario, le liste sono *mutabili*: possono essere modificati sul posto.
- Python considera la stringa come un singolo valore con parti, non come un insieme di
  valori.

```python
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

- Le liste e le stringhe di caratteri sono entrambi *collezioni*.

## L'indicizzazione oltre la fine dell'insieme è un errore.

- Python segnala un `IndexError` se si tenta di accedere a un valore che non esiste.
  - Questo è un tipo di [errore di runtime] (04-built-in.md).
  - Non può essere rilevato durante l'analisi del codice perché l'indice potrebbe essere calcolato in base ai dati.

```python
print('99th element of element is:', element[99])
```

```output
IndexError: string index out of range
```

::::::::::::::::::::::::::::::::::::::: challenge

## Riempire gli spazi vuoti

Riempite gli spazi vuoti in modo che il programma sottostante produca l'output mostrato.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

::::::::::::::: solution

## Soluzione

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Quanto è grande una fetta?

Se `start` e `stop` sono entrambi numeri interi non negativi, quanto è lunga la lista
`values[start:stop]`?

::::::::::::::: solution

## Soluzione

L'elenco `values[start:stop]` ha fino a `stop - start` elementi. Per esempio,
`values[1:4]` ha i 3 elementi `values[1]`, `values[2]` e `values[3]`. Perché "fino a"?
Come abbiamo visto in [episodio 2] (02-variables.md), se `stop` è maggiore della
lunghezza totale della lista `values`, otterremo comunque una lista, ma sarà più corta
del previsto.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Da stringhe a liste e viceversa

Dato questo:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. Cosa fa `list('some string')`?
2. Cosa genera `'-'.join(['x', 'y', 'z'])`?

::::::::::::::: solution

## Soluzione

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list)
   converte una stringa in un elenco contenente tutti i suoi caratteri.
2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) restituisce una
   stringa che è la *concatenazione* di ogni elemento di stringa dell'elenco e aggiunge
   il separatore tra ogni elemento della lista. Il risultato è `x-y-z`. Il separatore
   tra gli elementi è la stringa che fornisce questo metodo.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lavorare con la fine

Cosa stampa il seguente programma?

```python
element = 'helium'
print(element[-1])
```

1. Come interpreta Python un indice negativo?
2. Se un elenco o una stringa ha N elementi, qual è l'indice più negativo che può essere usato con sicurezza e quale posizione rappresenta tale indice?
3. Se `values` è una lista, cosa fa `del values[-1]`?
4. Come si possono visualizzare tutti gli elementi tranne l'ultimo senza cambiare
   `values`? (Suggerimento: è necessario combinare l'affettatura e l'indicizzazione
   negativa)

::::::::::::::: solution

## Soluzione

Il programma stampa `m`.

1. Python interpreta un indice negativo come se partisse dalla fine (invece che
   dall'inizio). L'ultimo elemento è `-1`.
2. L'ultimo indice che può essere usato con sicurezza con un elenco di N elementi è
   l'elemento `-N`, che rappresenta il primo elemento.
3. `del values[-1]` rimuove l'ultimo elemento della lista.
4. `values[:-1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Passaggio attraverso una lista

Cosa stampa il seguente programma?

```python
element = 'fluorine'
print(element[::2])
print(element[::-1])
```

1. Se scriviamo una fetta come `low:high:stride`, cosa fa `stride`?
2. Quale espressione selezionerebbe tutti gli elementi pari di un insieme?

::::::::::::::: solution

## Soluzione

il programma stampa

```python
furn
eniroulf
```

1. `stride` è la dimensione della fetta.
2. La slice `1::2` seleziona tutti gli elementi pari di un insieme: inizia con
   l'elemento `1` (che è il secondo elemento, dato che l'indicizzazione inizia da `0`),
   prosegue fino alla fine (dato che non viene dato `end`) e utilizza una dimensione di
   passo di `2` (cioè seleziona ogni secondo elemento).

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Limiti di fetta

Cosa stampa il seguente programma?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

::::::::::::::: solution

## Soluzione

```output
lithium

```

La prima istruzione stampa l'intera stringa, poiché la fetta va oltre la lunghezza
totale della stringa. La seconda istruzione restituisce una stringa vuota, perché la
fetta va "fuori dai limiti" della stringa.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ordinamento e ordinamento

Cosa stampano questi due programmi? In termini semplici, spiegare la differenza tra
`sorted(letters)` e `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

::::::::::::::: solution

## Soluzione

Il programma A stampa

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

Il programma B stampa

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` restituisce una copia ordinata della lista `letters` (l'elenco
originale `letters` rimane invariato), mentre `letters.sort()` ordina la lista `letters` sul posto e non restituisce nulla.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Copiare (o no)

Cosa stampano questi due programmi? In termini semplici, spiegare la differenza tra `new= old` e `new = old[:]`.

```python
# Program A
old = list('gold')
new = old      # simple assignment
new[0] = 'D'
print('new is', new, 'and old is', old)
```

```python
# Program B
old = list('gold')
new = old[:]   # assigning a slice
new[0] = 'D'
print('new is', new, 'and old is', old)
```

::::::::::::::: solution

## Soluzione

Il programma A stampa

```output
new is ['D', 'o', 'l', 'd'] and old is ['D', 'o', 'l', 'd']
```

Il programma B stampa

```output
new is ['D', 'o', 'l', 'd'] and old is ['g', 'o', 'l', 'd']
```

`new = old` rende `new` un riferimento all'elenco `old`; `new` e `old` puntano allo
stesso oggetto.

`new = old[:]` crea comunque un nuovo oggetto elenco `new` contenente tutti gli elementi dell'elenco `old`; `new` e `old` sono oggetti diversi.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Una lista memorizza molti valori in un'unica struttura.
- Utilizzare l'indice di un elemento per recuperarlo da una lista.
- I valori delle liste possono essere sostituiti assegnandoli.
- L'aggiunta di elementi a una lista lo allunga.
- Usare `del` per rimuovere completamente gli elementi da una lista.
- Una lista vuota non contiene valori.
- Le liste possono contenere valori di tipi diversi.
- Le stringhe di caratteri possono essere indicizzate come le liste.
- Le stringhe di caratteri sono immutabili.
- L'indicizzazione oltre la fine dell'insieme è un errore.

::::::::::::::::::::::::::::::::::::::::::::::::::



