---
title: Tipi di dati e conversione dei tipi
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare le principali differenze tra numeri interi e numeri con la virgola.
- Spiegare le principali differenze tra numeri e stringhe.
- Utilizzare le funzioni integrate per convertire  numeri interi, numeri con la virgola
  mobile e stringhe.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Quali tipi di dati memorizzano i programmi?
- Come posso convertire un tipo in un altro?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Ogni valore ha un tipo.

- Ogni valore in un programma ha un tipo specifico.
- Numero intero (`int`): rappresenta numeri interi positivi o negativi come 3 o -512.
- Numero con la virgola  (`float`): rappresenta numeri reali come 3,14159 o -2,5.
- Stringa di caratteri (solitamente chiamata "stringa", `str`): testo.
  - Scritto tra apici singoli o doppi (purché corrispondano).
  - Le virgolette non vengono stampate quando la stringa viene visualizzata.

## Usare la funzione integrata `type` per trovare il tipo di un valore.

- Usare la funzione integrata `type` per scoprire il tipo di un valore.
- Funziona anche con le variabili.
  - Ma ricordate: il *valore* ha il tipo --- la *variabile* è solo un'etichetta.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
fitness = 'average'
print(type(fitness))
```

```output
<class 'str'>
```

## I tipi controllano quali operazioni (o metodi) possono essere eseguite su un dato valore.

- Il tipo di un valore determina quali operazioni il programma può eseguire su di esso

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## Si possono usare gli operatori "+" e "\*" sulle stringhe.

- "Aggiungendo" stringhe di caratteri le concatena.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

- Moltiplicando una stringa di caratteri per un numero intero *N* si crea una nuova
  stringa che consiste in quella stringa di caratteri ripetuta *N* volte.
  - Poiché la moltiplicazione è un'addizione ripetuta.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Le stringhe hanno una lunghezza (ma i numeri no).

- La funzione integrata `len` conta il numero di caratteri di una stringa.

```python
print(len(full_name))
```

```output
11
```

- Ma i numeri non hanno una lunghezza (nemmeno zero).

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## Deve convertire i numeri in stringhe o viceversa quando opera su di essi. {#convertire-numeri-e-stringhe}

- Non si possono sommare numeri e stringhe.

```python
print(1 + '2')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- Non è consentito perché è ambiguo: `1 + '2'` dovrebbe essere `3` o `'12'`?
- Alcuni tipi possono essere convertiti in altri tipi utilizzando il nome del tipo come
  funzione.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Può mischiare liberamente interi e numeri con la virgola (float) nelle operazioni.

- Gli interi e i numeri con la virgola possono essere usati insieme in aritmetica.
  - Python 3 converte automaticamente gli interi in float quando necessario.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

## Le variabili cambiano valore solo quando viene loro assegnato qualcosa.

- Se una cella di un foglio di calcolo dipende da un'altra e si aggiorna quest'ultima,
  la prima si aggiorna automaticamente.
- Questo non avviene nei linguaggi di programmazione.

```python
variable_one = 1
variable_two = 5 * variable_one
variable_one = 2
print('first is', variable_one, 'and second is', variable_two)
```

```output
first is 2 and second is 5
```

- Il computer legge il valore di `variable_one` quando esegue la moltiplicazione, crea
  un nuovo valore e lo assegna a `variable_two`.
- In seguito, il valore di `variable_two` è impostato sul nuovo valore e *non dipende da
  `variable_one`*, quindi il suo valore non cambia automaticamente quando cambia
  `variable_one`.

::::::::::::::::::::::::::::::::::::::: challenge

## Frazioni

Che tipo di valore è 3,4? Come si fa a scoprirlo?

::::::::::::::: solution

## Soluzione

È un numero con la virgola (spesso abbreviato in "float"). È possibile scoprirlo
utilizzando la funzione integrata `type()`.

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Conversione automatica di tipo

Che tipo di numero è 3,25 + 4?

::::::::::::::: solution

## Soluzione

È un float: i numeri interi vengono automaticamente convertiti in float se necessario.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Scegliere un tipo

Quale tipo di valore (intero, numero con la virgola o stringa di caratteri) usereste
per rappresentare ciascuno dei seguenti elementi? Cercate di dare più di una risposta
valida per ogni problema. Per esempio, nel punto 1, quando avrebbe più senso contare i
giorni con una variabile float piuttosto che con un numero intero?

1. Numero di giorni dall'inizio dell'anno.
2. Tempo trascorso dall'inizio dell'anno a oggi in giorni.
3. Numero di serie di un pezzo di attrezzatura da laboratorio.
4. Età di un campione di laboratorio
5. Popolazione attuale di una città.
6. Popolazione media di una città nel tempo.

::::::::::::::: solution

## Soluzione

Le risposte alle domande sono:

1. Intero, poiché il numero di giorni è compreso tra 1 e 365.
2. Virgola (float), poiché sono richiesti giorni frazionati
3. Stringa se il numero di serie contiene lettere e numeri, altrimenti
   numero intero se il numero di serie è composto solo da numeri
4. Questo varia! Come si definisce l'età di un campione? Giorni interi dalla raccolta
   (intero)? Data e ora (stringa)?
5. Scegliere float per rappresentare la popolazione in grandi
   aggregati (ad esempio, milioni) o i numeri interi per rappresentare la popolazione in
   unità di individui.
6. Numeri con la virgola, poiché è probabile che una media abbia una parte
   frazionaria.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tipi di divisione

In Python 3, l'operatore `//` esegue la divisione intera (numeri interi), l'operatore
`/` esegue la divisione con la virgola e l'operatore `%` (o *modulo*) calcola e
restituisce il resto della divisione intera:

```python
print('5 // 3:', 5 // 3)
print('5 / 3:', 5 / 3)
print('5 % 3:', 5 % 3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

Se `num_subjects` è il numero di soggetti che partecipano a uno studio e
`num_per_survey` è il numero di soggetti che possono partecipare a un singolo sondaggio,
scrivere un'espressione che calcoli il numero di sondaggi necessari per raggiungere
tutti una volta.

::::::::::::::: solution

## Soluzione

Vogliamo il numero minimo di sondaggi che raggiunge tutti una volta, che è il valore
arrotondato per eccesso di `num_subjects/ num_per_survey`. Ciò equivale a eseguire una
divisione per piani con `//` e aggiungere 1. Prima della divisione è necessario
sottrarre 1 dal numero di soggetti per gestire il caso in cui `num_subjects` sia
uniformemente divisibile per `num_per_survey`.

```python
num_subjects = 600
num_per_survey = 42
num_surveys = (num_subjects - 1) // num_per_survey + 1

print(num_subjects, 'subjects,', num_per_survey, 'per survey:', num_surveys)
```

```output
600 subjects, 42 per survey: 15
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Stringhe a numeri

Se possibile, `float()` convertirà una stringa in un numero float e
`int()` convertirà float in un intero:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

Se la conversione non ha senso, viene visualizzato un messaggio di errore.

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Date queste informazioni, cosa ci si aspetta che faccia il seguente programma?

Cosa fa in realtà?

Perché pensate che lo faccia?

```python
print("fractional string to int:", int("3.4"))
```

::::::::::::::: solution

## Soluzione

Cosa ci si aspetta che faccia questo programma? Ci si potrebbe aspettare che il comando `int` di Python 3 converta la stringa "3.4" in 3.4 e un'ulteriore conversione di tipo in 3. Dopotutto, Python 3 compie molte altre magie: non
è forse parte del suo fascino?

```python
int("3.4")
```

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-2-ec6729dfccdc> in <module>
----> 1 int("3.4")
ValueError: invalid literal for int() with base 10: '3.4'
```

Tuttavia, Python 3 lancia un errore. Perché? Forse per coerenza. Se si chiede a Python
di eseguire due typecast consecutivi, è necessario convertirli esplicitamente nel
codice.

```python
int(float("3.4"))
```

```output
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Aritmetica con tipi diversi

Quale delle seguenti operazioni restituirà il numero float `2.0`? Nota: può
esserci più di una risposta giusta.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

::::::::::::::: solution

## Soluzione

Risposta: 1 e 4



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Numeri complessi

Python fornisce numeri complessi, che si scrivono come `1.0+2.0j`. Se `val` è un numero
complesso, si può accedere alle sue parti reali e immaginarie usando la *notazione a
punti* come `val.real` e `val.imag`.

```python
a_complex_number = 6 + 2j
print(a_complex_number.real)
print(a_complex_number.imag)
```

```output
6.0
2.0
```

1. Perché pensate che Python usi `j` invece di `i` per la parte immaginaria?
2. Cosa ci si aspetta che produca `1 + 2j + 3`?
3. Cosa ci si aspetta che sia `4j`? E `4 j` o `4 + j`?

::::::::::::::: solution

## Soluzione

1. I trattamenti matematici standard di solito usano `i` per indicare un numero
   immaginario. Tuttavia, stando a quanto riportato dai media, si trattava di una
   convenzione nata in precedenza nell'ambito dell'ingegneria elettrica, che ora
   rappresenta un'area tecnicamente costosa da modificare. [Stack Overflow fornisce
   ulteriori spiegazioni e discussioni]
   (https://stackoverflow.com/questions/24812444/why-are-complex-numbers-in-python-denoted-with-j-instead-of-i)
2. `(4+2j)`
3. `4j` e `Syntax Error: invalid syntax`. In questi ultimi casi, `j` è considerata una
   variabile e la dichiarazione dipende dal fatto che `j` sia definito e, in tal caso,
   dal valore che gli è stato assegnato.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Ogni valore ha un tipo.
- Usare la funzione integrata `type` per trovare il tipo di un valore.
- I tipi controllano le operazioni che possono essere eseguite sui valori.
- Le stringhe possono essere sommate e moltiplicate.
- Le stringhe hanno una lunghezza (ma i numeri no).
- Deve convertire i numeri in stringhe o viceversa quando opera su di essi.
- Può mescolare liberamente numeri interi e float nelle operazioni.
- Le variabili cambiano valore solo quando viene loro assegnato qualcosa.

::::::::::::::::::::::::::::::::::::::::::::::::::



