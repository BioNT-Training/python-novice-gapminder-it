---
title: Le biblioteche
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare cosa sono le librerie software e perché i programmatori le creano e le usano.
- Scrivere programmi che importano e utilizzano moduli della libreria standard di
  Python.
- Trovare e leggere la documentazione della libreria standard in modo interattivo
  (nell'interprete) e online.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come si può utilizzare il software scritto da altri?
- Come posso scoprire cosa fa questo software?

::::::::::::::::::::::::::::::::::::::::::::::::::

## La maggior parte della potenza di un linguaggio di programmazione è nelle sue librerie.

- Una *libreria* è una raccolta di file (chiamati *moduli*) che contiene funzioni
  utilizzabili da altri programmi.
  - Può contenere anche valori di dati (ad esempio, costanti numeriche) e altro.
  - I contenuti della libreria dovrebbero essere correlati, ma non c'è modo di farlo
    rispettare.
- La [libreria standard][stdlib] di Python è un'ampia suite di moduli fornita con Python
  stesso.
- Molte altre librerie sono disponibili su [PyPI][pypi] (l'indice dei pacchetti Python).
- Vedremo più avanti come scrivere nuove librerie.

::::::::::::::::::::::::::::::::::::::::: callout

## Librerie e moduli

Una libreria è un insieme di moduli, ma i termini sono spesso usati in modo
intercambiabile, soprattutto perché molte librerie sono costituite da un solo modulo,
quindi non preoccupatevi se li mischiate.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Un programma deve importare un modulo di libreria prima di utilizzarlo.

- Usare `import` per caricare un modulo di libreria nella memoria di un programma.
- quindi fare riferimento agli elementi del modulo come `module_name.thing_name`.
  - Python usa `.` per indicare "parte di".
- Utilizzo di `math`, uno dei moduli della libreria standard:

```python
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
```

```output
pi is 3.141592653589793
cos(pi) is -1.0
```

- Bisogna fare riferimento a ogni elemento con il nome del modulo.
  - `math.cos(pi)` non funziona: il riferimento a `pi` non "eredita" in qualche modo il
    riferimento della funzione a `math`.

## Usare `help` per conoscere il contenuto di un modulo di libreria.

- funziona come l'aiuto per una funzione.

```python
help(math)
```

```output
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
```

## Importare elementi specifici da un modulo di libreria per abbreviare i programmi.

- Usare `from ... import ...` per caricare solo elementi specifici da un modulo di
  libreria.
- quindi fare riferimento ad essi direttamente senza il nome della libreria come
  prefisso.

```python
from math import cos, pi

print('cos(pi) is', cos(pi))
```

```output
cos(pi) is -1.0
```

## Creare un alias per un modulo di libreria quando lo si importa per accorciare i programmi.

- Usare `import ... as ...` per dare a una libreria un breve *alias* durante
  l'importazione.
- quindi fare riferimento agli elementi della libreria usando questo nome abbreviato.

```python
import math as m

print('cos(pi) is', m.cos(m.pi))
```

```output
cos(pi) is -1.0
```

- comunemente usato per le librerie usate di frequente o con nomi lunghi.
  - Ad esempio, la libreria di plottaggio `matplotlib` è spesso indicata con l'alias
    `mpl`.
- Ma può rendere i programmi più difficili da capire, poiché i lettori devono imparare
  gli alias del programma.

::::::::::::::::::::::::::::::::::::::: challenge

## Esplorazione del modulo matematico

1. Quale funzione del modulo `math` si può usare per calcolare una radice quadrata
   *senza* usare `sqrt`?
2. Poiché la libreria contiene questa funzione, perché esiste `sqrt`?

::::::::::::::: solution

## Soluzione

1. Usando `help(math)` vediamo che abbiamo `pow(x,y)` in aggiunta a `sqrt(x)`, quindi
   potremmo usare `pow(x, 0.5)` per trovare una radice quadrata.

2. La funzione `sqrt(x)` è probabilmente più leggibile di `pow(x, 0.5)`
   nell'implementazione delle equazioni. La leggibilità è una pietra miliare della buona
   programmazione, quindi ha senso fornire una funzione speciale per questo specifico
   caso comune.

Inoltre, il design della libreria `math` di Python ha origine nello standard C, che
include sia `sqrt(x)` che `pow(x,y)`, quindi un po' di storia della programmazione si
ritrova nei nomi delle funzioni di Python.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Individuazione del modulo giusto

Si vuole selezionare un carattere casuale da una stringa:

```python
bases = 'ACTTGCTTGAC'
```

1. Quale modulo della [libreria standard][stdlib] potrebbe aiutarvi?
2. Quale funzione scegliereste da quel modulo? Ci sono alternative?
3. Provate a scrivere un programma che utilizzi la funzione.

::::::::::::::: solution

## Soluzione

Il [modulo random][randommod] sembra poter essere utile.

La stringa ha 11 caratteri, ognuno dei quali ha un indice posizionale da 0 a 10. Si
possono usare le funzioni
[`random.randrange`](https://docs.python.org/3/library/random.html#random.randrange) o
[`random.randint`](https://docs.python.org/3/library/random.html#random.randint) per
ottenere un numero intero casuale compreso tra 0 e 10, e poi selezionare il carattere
`bases` a quell'indice:

```python
from random import randrange

random_index = randrange(len(bases))
print(bases[random_index])
```

o in modo più compatto:

```python
from random import randrange

print(bases[randrange(len(bases))])
```

Forse avete trovato la funzione
[`random.sample`](https://docs.python.org/3/library/random.html#random.sample)? Consente
una digitazione leggermente inferiore, ma potrebbe essere un po' più difficile da capire
leggendo:

```python
from random import sample

print(sample(bases, 1)[0])
```

Si noti che questa funzione restituisce un elenco di valori. Impareremo a conoscere gli
elenchi in [episodio 11] (11-lists.md).

La soluzione più semplice e breve è la funzione
[`random.choice`](https://docs.python.org/3/library/random.html#random.choice) che fa
esattamente quello che vogliamo:

```python
from random import choice

print(choice(bases))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Esempio di programmazione del puzzle (problema di Parson)

Riorganizzare le seguenti istruzioni in modo da stampare una base di DNA casuale e il
suo indice nella stringa. Non tutte le istruzioni sono necessarie. Sentitevi liberi di
usare/aggiungere variabili intermedie.

```python
bases="ACTTGCTTGAC"
import math
import random
___ = random.randrange(n_bases)
___ = len(bases)
print("random base ", bases[___], "base index", ___)
```

::::::::::::::: solution

## Soluzione

```python
import math 
import random
bases = "ACTTGCTTGAC" 
n_bases = len(bases)
idx = random.randrange(n_bases)
print("random base", bases[idx], "base index", idx)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Quando è disponibile l'aiuto?

Quando un vostro collega digita `help(math)`, Python segnala un errore:

```error
NameError: name 'math' is not defined
```

Cosa ha dimenticato di fare il vostro collega?

::::::::::::::: solution

## Soluzione

Importazione del modulo matematico (`import math`)



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importazione con gli alias

1. Riempire gli spazi vuoti in modo che il programma sottostante stampi `90.0`.
2. Riscrivere il programma in modo che usi `import` *senza* `as`.
3. Quale forma trovate più facile da leggere?

```python
import math as m
angle = ____.degrees(____.pi / 2)
print(____)
```

::::::::::::::: solution

## Soluzione

```python
import math as m
angle = m.degrees(m.pi / 2)
print(angle)
```

può essere scritto come

```python
import math
angle = math.degrees(math.pi / 2)
print(angle)
```

Dal momento che avete appena scritto il codice e avete familiarità con esso, potreste
trovare la prima versione più facile da leggere. Ma quando si cerca di leggere un enorme
pezzo di codice scritto da qualcun altro, o quando si torna al proprio enorme pezzo di
codice dopo diversi mesi, i nomi non abbreviati sono spesso più facili, a meno che non
ci siano chiare convenzioni di abbreviazione.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ci sono molti modi per importare le librerie!

abbinare le seguenti istruzioni di stampa alle chiamate di libreria appropriate.

Comandi di stampa:

1. `print("sin(pi/2) =", sin(pi/2))`
2. `print("sin(pi/2) =", m.sin(m.pi/2))`
3. `print("sin(pi/2) =", math.sin(math.pi/2))`

Chiamate di libreria:

1. `from math import sin, pi`
2. `import math`
3. `import math as m`
4. `from math import *`

::::::::::::::: solution

## Soluzione

1. Chiamate di libreria 1 e 4. Per fare riferimento direttamente a `sin` e `pi` senza il
   nome della libreria come prefisso, è necessario usare l'istruzione `from ... import
   ...`. Mentre la chiamata di libreria 1 importa specificamente le due funzioni `sin` e
   `pi`, la chiamata di libreria 4 importa tutte le funzioni del modulo `math`.
2. Chiamata alla biblioteca 3. In questo caso, `sin` e `pi` sono indicati con il nome
   abbreviato di libreria `m` invece di `math`. La chiamata di libreria 3 fa esattamente
   questo usando la sintassi `import ... as ...`: crea un alias per `math` sotto forma
   di nome abbreviato `m`.
3. Chiamata di libreria 2. Qui `sin` e `pi` sono indicati con il normale nome di
   libreria `math`, quindi è sufficiente la normale chiamata `import ...`.

**Nota:** sebbene la chiamata di libreria 4 funzioni, importare tutti i nomi da un
modulo usando un'importazione con caratteri jolly è [sconsigliato][pep8-imports], in
quanto rende poco chiaro quali nomi del modulo sono usati nel codice. In generale, è
meglio rendere le importazioni il più specifiche possibile e importare solo ciò che il
codice utilizza. Nella chiamata di libreria 1, la dichiarazione `import` ci dice
esplicitamente che la funzione `sin` è importata dal modulo `math`, ma la chiamata di
libreria 4 non fornisce questa informazione.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importazione di elementi specifici

1. Riempire gli spazi vuoti in modo che il programma sottostante stampi `90.0`.
2. Trovate questa versione più facile da leggere rispetto alle precedenti?
3. Perché i programmatori non dovrebbero usare sempre questa forma di `import`?

```python
____ math import ____, ____
angle = degrees(pi / 2)
print(angle)
```

::::::::::::::: solution

## Soluzione

```python
from math import degrees, pi
angle = degrees(pi / 2)
print(angle)
```

Molto probabilmente questa versione è più facile da leggere, perché è meno densa. La
ragione principale per non usare questa forma di importazione è quella di evitare
scontri di nomi. Per esempio, non si importerebbe `degrees` in questo modo se si volesse
usare anche il nome `degrees` per una propria variabile o funzione. O se si importasse
anche una funzione chiamata `degrees` da un'altra libreria.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lettura dei messaggi di errore

1. Leggete il codice qui sotto e cercate di identificare gli errori senza eseguirlo.
2. Eseguite il codice e leggete il messaggio di errore. Di che tipo di errore si tratta?

```python
from math import log
log(0)
```

::::::::::::::: solution

## Soluzione

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-1-d72e1d780bab> in <module>
      1 from math import log
----> 2 log(0)

ValueError: math domain error
```

1. Il logaritmo di `x` è definito solo per `x > 0`, quindi 0 è fuori dal dominio della
   funzione.
2. Si ottiene un errore del tipo `ValueError`, che indica che la funzione ha ricevuto un
   valore di argomento inappropriato. Il messaggio aggiuntivo "errore del dominio
   matematico" chiarisce il problema.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

[stdlib]: https://docs.python.org/3/library/
[pypi]: https://pypi.python.org/pypi/
[randommod]: https://docs.python.org/3/library/random.html
[pep8-imports]: https://pep8.org/#imports


:::::::::::::::::::::::::::::::::::::::: keypoints

- La maggior parte della potenza di un linguaggio di programmazione è nelle sue
  librerie.
- Un programma deve importare un modulo di libreria per poterlo utilizzare.
- Usare `help` per conoscere il contenuto di un modulo di libreria.
- Importazione di elementi specifici da una libreria per abbreviare i programmi.
- Creare un alias per una libreria quando la si importa per abbreviare i programmi.

::::::::::::::::::::::::::::::::::::::::::::::::::



