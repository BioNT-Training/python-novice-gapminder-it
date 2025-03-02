---
title: Stile di programmazione
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Fornire valide giustificazioni per le regole di base dello stile di codifica.
- Riformulare i programmi di una pagina per renderli più leggibili e giustificare le
  modifiche.
- Utilizzare gli standard di codifica della comunità Python (PEP-8).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso rendere i miei programmi più leggibili?
- Come la maggior parte dei programmatori formatta il proprio codice?
- Come possono i programmi controllare il proprio funzionamento?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Stile di codifica

Uno stile di codifica coerente aiuta gli altri (compreso il nostro futuro) a leggere e
capire il codice più facilmente. Il codice viene letto molto più spesso di quanto non
venga scritto e, come afferma lo [Zen of
Python](https://www.python.org/dev/peps/pep-0020), "La leggibilità conta". Python ha
proposto uno stile standard attraverso una delle sue prime Python Enhancement Proposals
(PEP), [PEP8](https://www.python.org/dev/peps/pep-0008).

Alcuni punti da evidenziare:

- documentare il codice e assicurarsi che siano chiare le ipotesi, gli algoritmi
  interni, gli input e gli output previsti, ecc
- utilizzare nomi di variabili chiari e semanticamente significativi
- usare gli spazi bianchi, *non* le tabulazioni, per indentare le righe (le tabulazioni
  possono causare problemi in diversi editor di testo, sistemi operativi e sistemi di
  controllo delle versioni)

## Seguire lo stile standard di Python nel codice.

- [PEP8](https://www.python.org/dev/peps/pep-0008): una guida allo stile di Python che
  tratta argomenti come il nome delle variabili, l'indentazione del codice, la struttura
  delle dichiarazioni `import`, ecc. L'adesione al PEP8 facilita la lettura e la
  comprensione del codice da parte degli altri sviluppatori Python, che possono così
  capire come dovrebbero essere i loro contributi.
- Per verificare la conformità del codice alla PEP8, si può usare l'applicazione
  [pycodestyle](https://pypi.org/project/pycodestyle/) e strumenti come [black code
  formatter](https://github.com/psf/black) possono formattare automaticamente il codice
  in modo da renderlo conforme alla PEP8 e a pycodestyle (esiste anche un formattatore
  per quaderni Jupyter [nb\_black](https://github.com/dnanhkhoa/nb_black)).
- Alcuni gruppi e organizzazioni seguono linee guida di stile diverse dalla PEP8. Per
  esempio, la [Google style guide on
  Python](https://google.github.io/styleguide/pyguide.html) contiene raccomandazioni
  leggermente diverse. Google ha scritto un'applicazione che può aiutare a formattare il
  codice secondo il suo stile o quello della PEP8, chiamata
  [yapf](https://github.com/google/yapf/).
- Per quanto riguarda lo stile di codifica, la chiave è la *coerenza*. Scegliete uno
  stile per il vostro progetto, che sia PEP8, lo stile di Google o qualcos'altro, e fate
  del vostro meglio per assicurarvi che voi e tutti gli altri con cui collaborate lo
  rispettiate. La coerenza all'interno di un progetto ha spesso un impatto maggiore
  rispetto al particolare stile utilizzato. Uno stile coerente renderà il vostro
  software più facile da leggere e da capire per gli altri e per il vostro futuro.

## Usare le asserzioni per controllare gli errori interni.

Le asserzioni sono un metodo semplice ma potente per assicurarsi che il contesto in cui
il codice viene eseguito sia quello previsto.

```python
def calc_bulk_density(mass, volume):
    '''Return dry bulk density = powder mass / powder volume.'''
    assert volume > 0
    return mass / volume
```

Se l'asserzione è `False`, l'interprete Python solleva un'eccezione di runtime
`AssertionError`. Il codice sorgente dell'espressione fallita viene visualizzato come
parte del messaggio di errore. Per ignorare le asserzioni nel codice, eseguire
l'interprete con lo switch '-O' (optimize). Le asserzioni devono contenere solo semplici
controlli e non devono mai modificare lo stato del programma. Ad esempio, un'asserzione
non dovrebbe mai contenere un'assegnazione.

## Usare i docstring per fornire un aiuto integrato.

Se la prima cosa in una funzione è una stringa di caratteri non assegnata direttamente a
una variabile, Python la allega alla funzione, accessibile tramite la funzione di aiuto
integrata. Questa stringa che fornisce la documentazione è nota anche come *docstring*.

```python
def average(values):
    "Return average of values, or None if no values are supplied."

    if len(values) == 0:
        return None
    return sum(values) / len(values)

help(average)
```

```output
Help on function average in module __main__:

average(values)
    Return average of values, or None if no values are supplied.
```

::::::::::::::::::::::::::::::::::::::::: callout

## Stringhe multilinea

Spesso si usano stringhe *multilinee* per la documentazione. Queste iniziano e finiscono
con tre caratteri di virgolette (singole o doppie) e terminano con tre caratteri
corrispondenti.

```python
"""This string spans
multiple lines.

Blank lines are allowed."""
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cosa verrà mostrato?

Evidenziate le righe del codice sottostante che saranno disponibili come guida in linea.
Ci sono righe che dovrebbero essere rese disponibili, ma non lo saranno? Alcune linee
produrranno un errore di sintassi o un errore di runtime?

```python
"Find maximum edit distance between multiple sequences."
# This finds the maximum distance between all sequences.

def overall_max(sequences):
    '''Determine overall maximum edit distance.'''

    highest = 0
    for left in sequences:
        for right in sequences:
            '''Avoid checking sequence against itself.'''
            if left != right:
                this = edit_distance(left, right)
                highest = max(highest, this)

    # Report.
    return highest
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Documento questo

Usate i commenti per descrivere e aiutare gli altri a capire sezioni o singole linee di
codice potenzialmente poco intuitive. Sono particolarmente utili a chiunque abbia
bisogno di capire e modificare il codice in futuro, compreso voi stessi.

Usate i docstring per documentare gli input accettabili e gli output attesi di un metodo
o di una classe, il suo scopo, le assunzioni e il comportamento previsto. I docstring
vengono visualizzati quando un utente invoca il metodo incorporato `help` sul metodo o
sulla classe.

Trasformate il commento della funzione seguente in una docstring e verificate che `help`
la visualizzi correttamente.

```python
def middle(a, b, c):
    # Return the middle value of three.
    # Assumes the values can actually be compared.
    values = [a, b, c]
    values.sort()
    return values[1]
```

::::::::::::::: solution

## Soluzione

```python
def middle(a, b, c):
    '''Return the middle value of three.
    Assumes the values can actually be compared.'''
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Pulire il codice

1. Leggete questo breve programma e cercate di prevedere cosa fa.
2. Eseguitelo: quanto è stata accurata la vostra previsione?
3. Riformulare il programma per renderlo più leggibile. Ricordatevi di eseguirlo dopo
   ogni modifica per assicurarvi che il suo comportamento non sia cambiato.
4. Confrontate la vostra riscrittura con quella del vostro vicino. Che cosa avete fatto
   di uguale? Cosa avete fatto di diverso e perché?

```python
n = 10
s = 'et cetera'
print(s)
i = 0
while i < n:
    # print('at', j)
    new = ''
    for j in range(len(s)):
        left = j-1
        right = (j+1)%len(s)
        if s[left]==s[right]: new = new + '-'
        else: new = new + '*'
    s=''.join(new)
    print(s)
    i += 1
```

::::::::::::::: solution

## Soluzione

Ecco una soluzione.

```python
def string_machine(input_string, iterations):
    """
    Takes input_string and generates a new string with -'s and *'s
    corresponding to characters that have identical adjacent characters
    or not, respectively.  Iterates through this procedure with the resultant
    strings for the supplied number of iterations.
    """
    print(input_string)
    input_string_length = len(input_string)
    old = input_string
    for i in range(iterations):
        new = ''
        # iterate through characters in previous string
        for j in range(input_string_length):
            left = j-1
            right = (j+1) % input_string_length  # ensure right index wraps around
            if old[left] == old[right]:
                new = new + '-'
            else:
                new = new + '*'
        print(new)
        # store new string as old
        old = new     

string_machine('et cetera', 10)
```

```output
et cetera
*****-***
----*-*--
---*---*-
--*-*-*-*
**-------
***-----*
--**---**
*****-***
----*-*--
---*---*-
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Seguire lo stile standard di Python nel codice.
- Usare i docstring per fornire un aiuto incorporato.

::::::::::::::::::::::::::::::::::::::::::::::::::



