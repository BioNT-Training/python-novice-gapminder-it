---
title: Condizionali
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Scrivere correttamente programmi che utilizzano istruzioni if e else e semplici
  espressioni booleane (senza operatori logici).
- Tracciare l'esecuzione di condizionali non annidati e di condizionali all'interno di
  loop.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come possono i programmi fare cose diverse per dati diversi?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usare le istruzioni `if` per controllare se un blocco di codice viene eseguito o meno.

- Un'istruzione `if` (più propriamente chiamata istruzione *condizionale*) controlla se
  un blocco di codice viene eseguito o meno.
- La struttura è simile a quella di un'istruzione `for`:
  - La prima riga si apre con `if` e termina con i due punti
  - Il corpo contenente una o più istruzioni è indentato (di solito di 4 spazi)

```python
mass = 3.54
if mass > 3.0:
    print(mass, 'is large')

mass = 2.07
if mass > 3.0:
    print (mass, 'is large')
```

```output
3.54 is large
```

## Le condizioni sono spesso utilizzate all'interno dei cicli.

- Non ha molto senso usare una condizione quando si conosce il valore (come sopra).
- Ma è utile quando abbiamo una collezione da elaborare.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
```

```output
3.54 is large
9.22 is large
```

## Usare `else` per eseguire un blocco di codice quando una condizione `if` è *non* vera.

- `else` può essere usato dopo un `if`.
- Permette di specificare un'alternativa da eseguire quando il ramo `if` non viene
  preso.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is large
1.86 is small
1.71 is small
```

## Usare `elif` per specificare test aggiuntivi.

- Si possono fornire diverse scelte alternative, ognuna con il proprio test.
- Usate `elif` (abbreviazione di "else if") e una condizione per specificare queste
  condizioni.
- Sempre associato a un `if`.
- Deve precedere il `else` (che è il "catch all").

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 9.0:
        print(m, 'is HUGE')
    elif m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is HUGE
1.86 is small
1.71 is small
```

## Le condizioni sono testate una volta, in ordine.

- Python passa attraverso i rami della condizione in ordine, testando ciascuno di essi a
  turno.
- L'ordine è importante.

```python
grade = 85
if grade >= 90:
    print('grade is A')
elif grade >= 80:
    print('grade is B')
elif grade >= 70:
    print('grade is C')
```

```output
grade is B
```

- Non torna automaticamente indietro e rivaluta se i valori cambiano.

```python
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
```

```output
adjusting velocity
```

- Spesso si usano le condizioni in un ciclo per "evolvere" i valori delle variabili.

```python
velocity = 10.0
for i in range(5): # execute the loop 5 times
    print(i, ':', velocity)
    if velocity > 20.0:
        print('moving too fast')
        velocity = velocity - 5.0
    else:
        print('moving too slow')
        velocity = velocity + 10.0
print('final velocity:', velocity)
```

```output
0 : 10.0
moving too slow
1 : 20.0
moving too slow
2 : 30.0
moving too fast
3 : 25.0
moving too fast
4 : 20.0
moving too slow
final velocity: 30.0
```

## Creare una tabella che mostri i valori delle variabili per tracciare l'esecuzione di un programma.

<table>
  <tr>   <td><strong>i</strong></td>   <td>0</td>   <td>.</td>   <td>1</td>   <td>.</td>   <td>2</td>   <td>.</td>   <td>3</td>   <td>.</td>   <td>4</td>   <td>.</td>
  </tr>
  <tr>   <td><strong>velocity</strong></td>   <td>10.0</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>   <td>.</td>   <td>25.0</td>   <td>.</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>
  </tr>
</table>

- Il programma deve avere un'istruzione `print` *fuori* dal corpo del ciclo per mostrare
  il valore finale di `velocity`, poiché il suo valore viene aggiornato dall'ultima
  iterazione del ciclo.

::::::::::::::::::::::::::::::::::::::::: callout

## Relazioni composte con `and`, `or` e parentesi

Spesso si vuole che una combinazione di cose sia vera. È possibile combinare le
relazioni all'interno di una condizione utilizzando `and` e `or`. Continuando l'esempio
precedente, si supponga di avere

```python
mass     = [ 3.54,  2.07,  9.22,  1.86,  1.71]
velocity = [10.00, 20.00, 30.00, 25.00, 20.00]

i = 0
for i in range(5):
    if mass[i] > 5 and velocity[i] > 20:
        print("Fast heavy object.  Duck!")
    elif mass[i] > 2 and mass[i] <= 5 and velocity[i] <= 20:
        print("Normal traffic")
    elif mass[i] <= 2 and velocity[i] <= 20:
        print("Slow light object.  Ignore it")
    else:
        print("Whoa!  Something is up with the data.  Check it")
```

Come per l'aritmetica, si possono e si devono usare le parentesi ogni volta che c'è una
possibile ambiguità. Una buona regola generale è quella di usare *sempre* le parentesi
quando si mescolano `and` e `or` nella stessa condizione. Cioè, invece di:

```python
if mass[i] <= 2 or mass[i] >= 5 and velocity[i] > 20:
```

scrivere una di queste:

```python
if (mass[i] <= 2 or mass[i] >= 5) and velocity[i] > 20:
if mass[i] <= 2 or (mass[i] >= 5 and velocity[i] > 20):
```

in modo che sia perfettamente chiaro a un lettore (e a Python) cosa si intende
veramente.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tracciamento dell'esecuzione

Cosa stampa questo programma?

```python
pressure = 71.9
if pressure > 50.0:
    pressure = 25.0
elif pressure <= 50.0:
    pressure = 0.0
print(pressure)
```

::::::::::::::: solution

## Soluzione

```output
25.0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Valori di taglio

Riempite gli spazi vuoti in modo che questo programma crei un nuovo elenco contenente
zeri dove i valori dell'elenco originale erano negativi e uno dove i valori dell'elenco
originale erano positivi.

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = ____
for value in original:
    if ____:
        result.append(0)
    else:
        ____
print(result)
```

```output
[0, 1, 1, 1, 0, 1]
```

::::::::::::::: solution

## Soluzione

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = []
for value in original:
    if value < 0.0:
        result.append(0)
    else:
        result.append(1)
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Elaborazione di piccoli file

Modificate questo programma in modo che elabori solo i file con meno di 50 record.

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    ____:
        print(filename, len(contents))
```

::::::::::::::: solution

## Soluzione

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    if len(contents) < 50:
        print(filename, len(contents))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Inizializzazione

Modificate questo programma in modo che trovi i valori più grandi e più piccoli
dell'elenco, indipendentemente dall'intervallo di valori originario.

```python
values = [...some test data...]
smallest, largest = None, None
for v in values:
    if ____:
        smallest, largest = v, v
    ____:
        smallest = min(____, v)
        largest = max(____, v)
print(smallest, largest)
```

Quali sono i vantaggi e gli svantaggi dell'uso di questo metodo per trovare l'intervallo
dei dati?

::::::::::::::: solution

## Soluzione

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None and largest is None:
        smallest, largest = v, v
    else:
        smallest = min(smallest, v)
        largest = max(largest, v)
print(smallest, largest)
```

Se si scrive `== None` invece di `is None`, funziona anche quello, ma i programmatori
Python scrivono sempre `is None` a causa del modo speciale in cui funziona `None` nel
linguaggio.

Si può sostenere che un vantaggio dell'uso di questo metodo sarebbe quello di rendere il
codice più leggibile. Tuttavia, uno svantaggio è che questo codice non è efficiente
perché all'interno di ogni iterazione del ciclo `for`, ci sono altri due cicli che
eseguono due numeri ciascuno (le funzioni `min` e `max`). Sarebbe più efficiente iterare
su ogni numero una sola volta:

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None or v < smallest:
        smallest = v
    if largest is None or v > largest:
        largest = v
print(smallest, largest)
```

Ora abbiamo un ciclo, ma quattro test di confronto. Ci sono due modi per migliorarlo
ulteriormente: utilizzare un numero minore di confronti in ogni iterazione, oppure
utilizzare due cicli che contengono ciascuno un solo test di confronto. La soluzione più
semplice è spesso la migliore:

```python
values = [-2,1,65,78,-54,-24,100]
smallest = min(values)
largest = max(values)
print(smallest, largest)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utilizzare le istruzioni `if` per controllare se un blocco di codice viene eseguito o
  meno.
- Le condizioni sono spesso utilizzate all'interno dei cicli.
- Usare `else` per eseguire un blocco di codice quando una condizione `if` è *non* vera.
- Usare `elif` per specificare test aggiuntivi.
- Le condizioni vengono verificate una volta, in ordine.
- Creare una tabella che mostri i valori delle variabili per tracciare l'esecuzione di
  un programma.

::::::::::::::::::::::::::::::::::::::::::::::::::



