---
title: Funzioni integrate e aiuto
teaching: 15
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare lo scopo delle funzioni.
- Chiamare correttamente le funzioni integrate di Python.
- Annidare correttamente le chiamate alle funzioni integrate.
- Usare la guida per visualizzare la documentazione delle funzioni integrate.
- Descrivere correttamente le situazioni in cui si verificano SyntaxError e NameError.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso usare le funzioni integrate?
- Come posso scoprire cosa fanno?
- Che tipo di errori possono verificarsi?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usare i commenti per aggiungere documentazione ai programmi.

```python
# Questa frase non è eseguita ma solo una descrizione
adjustment = 0.5   # Nemmeno questo, tutto quello che si trova dopo  '#' viene ignorato.
```

## Una funzione può accettare zero o più argomenti.

- Abbiamo già visto alcune funzioni, ora diamo un'occhiata più da vicino.
- Chiamiamo argomento il valore che si passa a una funzione quando la si utilizza
- `len` prende solo un argomento.
- `int`, `str` e `float` creano un nuovo valore a partire da uno esistente.
- `print` può essere chiamata senza argomenti o più
- `print` senza argomenti stampa una riga vuota.
  - Bisogna sempre usare le parentesi, anche senza argomenti, in modo che Python sappia
    che si sta chiamando una funzione.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Ogni funzione restituisce qualcosa.

- Ogni funzione eseguita produce un risultato.
- Se la funzione non ha un risultato utile da restituire, di solito restituisce il
  valore speciale `None`. `None` è un oggetto Python che ritorna ogni volta che
  non c'è un valore.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

## Le funzioni incorporate di uso comune includono `max`, `min` e `round`.

- Usare `max` per trovare il valore maggiore di uno o più valori.
- Usare `min` per trovare il minore.
- Entrambi funzionano su stringhe di caratteri e numeri.
  - "Max" e "Min" usano (0-9, A-Z, a-z) per confrontare le lettere.

```python
print(max(1, 2, 3))
print(min('a', 'A', '0'))
```

```output
3
0
```

## Le funzioni possono essere seguite solo con alcuni o combinazioni di argomenti.

- A `max` e `min` deve essere dato almeno un argomento.
  - "La richiesta di un massino di un insieme vuoto" è una domanda senza senso.
- E devono essere dati oggetti che possono essere confrontati in modo significativo.

```python
print(max(1, 'a'))
```

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Le funzioni possono avere valori predefiniti per alcuni argomenti.

- `round` arrotonda un numero float.
- Per impostazione predefinita, arrotonda con zero cifre decimali.

```python
round(3.712)
```

```output
4
```

- Possiamo specificare il numero di cifre decimali che desideriamo come argomento.

```python
round(3.712, 1)
```

```output
3.7
```

## Le funzioni collegate agli oggetti sono chiamate metodi

- Le funzioni possono assumere un’altra forma, che sarà comune negli episodi dedicati a pandas.
- I metodi hanno le parentesi come le funzioni, ma vengono dopo la variabile.
- Alcuni metodi sono utilizzati per operazioni interne a Python e sono contrassegnati da
  doppie sottolineature.

```python
my_string = 'Hello world!'  # creazione di un oggetto stringa

print(len(my_string))       # la funzione len prende una stringa come argomento e restituisce la sua lunghezza

print(my_string.swapcase()) # chiamata al metodo swapcase sull'oggetto my_string

print(my_string.__len__())  # chiamata diretta al metodo interno __len__, usato da len(my_string)

```

```output
12
hELLO WORLD!
12
```

- Potreste anche vederli concatenati. Funzionano da sinistra a destra.

print(my_string.isupper())          # Non tutte le lettere sono maiuscole
print(my_string.upper())            # Questo converte tutte le lettere in maiuscole

print(my_string.upper().isupper())  # Ora tutte le lettere sono maiuscole
```

```output
False
HELLO WORLD
True
```

## Usare la funzione integrata `help` per ottenere aiuto per una funzione.

- Ogni funzione incorporata ha una documentazione online.

```python
help(round)
```

```output
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.

    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

## Il Jupyter notebook offre due modi per ottenere aiuto.

- Opzione 1: posizionare il cursore vicino al punto in cui viene invocata la funzione in
  una cella (cioè il nome della funzione o i suoi parametri),
  - Tenere premuto <kbd>Shift</kbd> e premere <kbd>Tab</kbd>.
  - Eseguire questa operazione più volte per espandere le informazioni restituite.
- Opzione 2: Digitare il nome della funzione in una cella con un punto interrogativo.
  Quindi eseguire la cella.

## Python segnala un errore di sintassi quando non riesce a capire il sorgente di un programma.

- Non prova nemmeno a eseguire il programma se non può essere analizzato.

```python
# Dimenticato di chiudere le virgolette.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# Un extra '='.
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Osservate più da vicino il messaggio di errore:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- Il messaggio indica un problema sulla prima riga dell'input ("riga 1").
  - In questo caso la sezione "ipython-input" del nome del file ci dice che stiamo
    lavorando con l'input di IPython, l'interprete Python usato da Jupyter Notebook.
- La parte `-6-` del nome del file indica che l'errore si è verificato nella cella 6 del
  nostro Notebook.
- La prossima è la riga di codice problematica, che indica il problema con un puntatore
  `^`.

## Python segnala un errore di runtime quando qualcosa va storto durante l'esecuzione di un programma. {#runtime-error}

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
```

- Correggere gli errori di sintassi leggendo il codice sorgente e gli errori di runtime
  tracciando l'esecuzione del programma.

::::::::::::::::::::::::::::::::::::::: challenge

## Che cosa succede quando

1. Spiegate in termini semplici l'ordine delle operazioni nel seguente programma: quando
   avviene l'addizione, quando avviene la sottrazione, quando viene chiamata ogni
   funzione, ecc.
2. Qual è il valore finale di `radiance`?

```python
radiance = 1.0
radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
```

::::::::::::::: solution

## Soluzione

1. Ordine delle operazioni:
  1. `1.1 * radiance = 1.1`
  2. `1.1 - 0.5 = 0.6`
  3. `min(radiance, 0.6) = 0.6`
  4. `2.0 + 0.6 = 2.6`
  5. `max(2.1, 2.6) = 2.6`
2. alla fine, `radiance = 2.6`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Individuare la differenza

1. Prevedere cosa stamperà ciascuna delle funzioni `print` del programma qui sotto.
2. `max(len(rich), poor)` viene eseguito o produce un messaggio di errore? Se viene
   eseguito, il suo risultato ha senso?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

::::::::::::::: solution

## Soluzione

```python
print(max(easy_string))
```

```output
c
```

```python
print(max(rich, poor))
```

```output
tin
```

```python
print(max(len(rich), len(poor)))
```

```output
4
```

`max(len(rich), poor)` lancia un TypeError. Questo si trasforma in `max(4, 'tin')` e,
come abbiamo detto prima, una stringa e un intero non possono essere confrontati in modo
significativo.

```error 
TypeError                                 Traceback (most recent call last)
<ipython-input-65-bc82ad05177a> in <module>
----> 1 max(len(rich), poor)

TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Perché no?

Perché `max` e `min` non restituiscono `None` quando sono chiamati senza argomenti?

::::::::::::::: solution

## Soluzione

`max` e `min` restituiscono TypeErrors in questo caso perché non è stato fornito il
numero corretto di parametri. Se restituisse solo `None`, l'errore sarebbe molto più
difficile da rintracciare, perché probabilmente verrebbe memorizzato in una variabile e
utilizzato più avanti nel programma, per poi lanciare un errore di runtime.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ultimo carattere di una stringa

Se Python inizia a contare da zero e `len` restituisce il numero di caratteri di una
stringa, quale espressione indice otterrà l'ultimo carattere della stringa `name`?
(Nota: vedremo un modo più semplice per farlo in un episodio successivo)

::::::::::::::: solution

## Soluzione

`name[len(name) - 1]`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Esplora la documentazione di Python!

La [documentazione ufficiale di Python](https://docs.python.org/3/) è probabilmente la
fonte più completa di informazioni sul linguaggio. È disponibile in diverse lingue e
contiene molte risorse utili. La pagina [Built-in
Functions](https://docs.python.org/3/library/functions.html) contiene un catalogo di
tutte queste funzioni, comprese quelle che abbiamo trattato in questa lezione. Alcune di
queste sono più avanzate e non necessarie al momento, ma altre sono molto semplici e
utili.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Usare i commenti per aggiungere documentazione ai programmi.
- Una funzione può accettare zero o più argomenti.
- Le funzioni incorporate di uso comune includono `max`, `min` e `round`.
- Le funzioni possono funzionare solo per determinate combinazioni di argomenti.
- Le funzioni possono avere valori predefiniti per alcuni argomenti.
- Usare la funzione integrata `help` per ottenere aiuto per una funzione.
- Il Jupyter notebook offre due modi per ottenere aiuto.
- Ogni funzione restituisce qualcosa.
- Python segnala un errore di sintassi quando non riesce a capire il sorgente di un
  programma.
- Python segnala un errore di runtime quando qualcosa va storto durante l'esecuzione di
  un programma.
- Correggere gli errori di sintassi leggendo il codice sorgente e gli errori di runtime
  tracciando l'esecuzione del programma.

::::::::::::::::::::::::::::::::::::::::::::::::::



