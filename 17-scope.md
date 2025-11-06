---
title: Ambito della variabile
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Identificare le variabili locali e globali.
- Identificare i parametri come variabili locali.
- Leggere un traceback e determinare il numero di file, funzione e riga in cui si è
  verificato l'errore, il tipo di errore e il messaggio di errore.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come funzionano le chiamate di funzione?
- Come posso determinare dove si sono verificati gli errori?

::::::::::::::::::::::::::::::::::::::::::::::::::

## L'ambito di una variabile è la parte del programma che può "vedere" quella variabile.

- Ci sono solo tanti nomi sensati per le variabili.
- Le persone che usano le funzioni non dovrebbero preoccuparsi dei nomi delle variabili usati dall'autore della funzione.
- Chi scrive funzioni non dovrebbe preoccuparsi di quali nomi di variabili usa il
  chiamante della funzione.
- La parte di un programma in cui una variabile è visibile è chiamata il suo *scope*.

```python
pressure = 103.9

def adjust(t):
    temperature = t * 1.43 / pressure
    return temperature
```

- `pressure` è una variabile *globale*.
  - Definita al di fuori di una particolare funzione.
  - Visibile ovunque.
- `t` e `temperature` sono *variabili locali* in `adjust`.
  - Definita nella funzione.
  - Non visibile nel programma principale.
  - Ricordate: un parametro di funzione è una variabile a cui viene automaticamente
    assegnato un valore quando la funzione viene chiamata.

```python
print('adjusted:', adjust(0.9))
print('temperature after call:', temperature)
```

```output
adjusted: 0.01238691049085659
```

```error
Traceback (most recent call last):
  File "/Users/swcarpentry/foo.py", line 8, in <module>
    print('temperature after call:', temperature)
NameError: name 'temperature' is not defined
```

::::::::::::::::::::::::::::::::::::::: challenge

## Uso delle variabili locali e globali

Traccia i valori di tutte le variabili di questo programma durante la sua esecuzione.
(Usare '---' come valore delle variabili prima e dopo la loro esistenza)

```python
limit = 100

def clip(value):
    return min(max(0.0, value), limit)

value = -22.5
print(clip(value))
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lettura dei messaggi di errore

Leggete il traceback qui sotto e identificate quanto segue:

1. Quanti livelli ha il traceback?
2. Qual è il nome del file in cui si è verificato l'errore?
3. Qual è il nome della funzione in cui si è verificato l'errore?
4. Su quale numero di riga di questa funzione si è verificato l'errore?
5. Qual è il tipo di errore?
6. Qual è il messaggio di errore?

```error
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-2-e4c4cbafeeb5> in <module>()
      1 import errors_02
----> 2 errors_02.print_friday_message()

/Users/ghopper/thesis/code/errors_02.py in print_friday_message()
     13
     14 def print_friday_message():
---> 15     print_message("Friday")

/Users/ghopper/thesis/code/errors_02.py in print_message(day)
      9         "sunday": "Aw, the weekend is almost over."
     10     }
---> 11     print(messages[day])
     12
     13

KeyError: 'Friday'
```

::::::::::::::: solution

## Soluzione

1. Tre livelli.
2. `errors_02.py`
3. `print_message`
4. Riga 11
5. `KeyError`. Questi errori si verificano quando si cerca di cercare una chiave che non esiste (di solito in una struttura di dati come un dizionario). Per maggiori informazioni su `KeyError` e su altre eccezioni integrate, consultare i [Python docs](https://docs.python.org/3/library/exceptions.html#KeyError).
6. `KeyError: 'Friday'`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- L'ambito di una variabile è la parte del programma che può "vedere" quella variabile.

::::::::::::::::::::::::::::::::::::::::::::::::::



