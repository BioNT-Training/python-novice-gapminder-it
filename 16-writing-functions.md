---
title: Funzioni di scrittura
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Spiegare e identificare la differenza tra definizione di funzione e chiamata di
  funzione.
- Scrivete una funzione che prende un piccolo numero fisso di argomenti e produce un
  unico risultato.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso creare le mie funzioni?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Scomporre i programmi in funzioni per renderli più comprensibili.

- Gli esseri umani possono tenere nella memoria di lavoro solo pochi elementi alla
  volta.
- Comprendere idee più grandi/più complicate comprendendo e combinando pezzi.
  - Componenti di una macchina.
  - Lemmi per la dimostrazione di teoremi.
- Le funzioni hanno lo stesso scopo nei programmi.
  - *Incapsula* la complessità in modo da poterla trattare come un'unica "cosa".
- consente anche il *riutilizzo*.
  - Scrivere una volta, usare molte volte.

## Definire una funzione usando `def` con un nome, dei parametri e un blocco di codice.

- Iniziare la definizione di una nuova funzione con `def`.
- Seguito dal nome della funzione.
  - Deve rispettare le stesse regole dei nomi delle variabili.
- Allora *parametri* tra parentesi.
  - parentesi vuote se la funzione non riceve input.
  - Ne parleremo in dettaglio tra poco.
- Poi i due punti.
- Poi un blocco di codice rientrato.

```python
def print_greeting():
    print('Hello!')
    print('The weather is nice today.')
    print('Right?')
```

## Definire una funzione non la fa funzionare.

- Definire una funzione non la fa funzionare.
  - Come assegnare un valore a una variabile.
- Deve chiamare la funzione per eseguire il codice che contiene.

```python
print_greeting()
```

```output
Hello!
```

## Gli argomenti di una chiamata di funzione sono abbinati ai suoi parametri definiti.

- Le funzioni sono più utili quando possono operare su dati diversi.
- Specificare i *parametri* quando si definisce una funzione.
  - Questi diventano variabili quando la funzione viene eseguita.
  - Sono assegnati gli argomenti della chiamata (cioè i valori passati alla funzione).
  - Se non si nominano gli argomenti quando li si usa nella chiamata, gli argomenti
    saranno abbinati ai parametri nell'ordine in cui questi sono definiti nella
    funzione.

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

Oppure, possiamo dare un nome agli argomenti quando chiamiamo la funzione, il che ci
permette di specificarli in qualsiasi ordine e aggiunge chiarezza al sito di chiamata;
altrimenti, mentre si legge il codice, si potrebbe dimenticare se il secondo argomento è
il mese o il giorno, ad esempio.

```python
print_date(month=3, day=19, year=1871)
```

```output
1871/3/19
```

- Via [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705): `()`
  contiene gli ingredienti della funzione mentre il corpo contiene la ricetta.

## Le funzioni possono restituire un risultato al loro chiamante usando `return`.

- Usare `return ...` per restituire un valore al chiamante.
- Può verificarsi in qualsiasi punto della funzione.
- Ma le funzioni sono più facili da capire se si presenta `return`:
  - All'inizio per gestire casi speciali.
  - Alla fine, con un risultato finale.

```python
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
```

```python
a = average([1, 3, 4])
print('average of actual values:', a)
```

```output
average of actual values: 2.6666666666666665
```

```python
print('average of empty list:', average([]))
```

```output
average of empty list: None
```

- Ricorda: [ogni funzione restituisce qualcosa](04-built-in.md).
- Una funzione che non restituisce esplicitamente un valore `return` restituisce
  automaticamente `None`.

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

```output
1871/3/19
result of call is: None
```

::::::::::::::::::::::::::::::::::::::: challenge

## Identificare gli errori di sintassi

1. Leggete il codice qui sotto e cercate di identificare gli errori *senza* eseguirlo.
2. Eseguite il codice e leggete il messaggio di errore. È un `SyntaxError` o un
   `IndentationError`?
3. Correggere l'errore.
4. Ripetere i punti 2 e 3 finché non si sono risolti tutti gli errori.

```python
def another_function
  print("Syntax errors are annoying.")
   print("But at least python tells us about them!")
  print("So they are usually not too hard to fix.")
```

::::::::::::::: solution

## Soluzione

```python
def another_function():
  print("Syntax errors are annoying.")
  print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Definizione e utilizzo

Cosa stampa il seguente programma?

```python
def report(pressure):
    print('pressure is', pressure)

print('calling', report, 22.5)
```

::::::::::::::: solution

## Soluzione

```output
calling <function report at 0x7fd128ff1bf8> 22.5
```

Una chiamata di funzione ha sempre bisogno di parentesi, altrimenti si ottiene
l'indirizzo di memoria dell'oggetto funzione. Quindi, se volessimo chiamare la funzione
denominata report e assegnarle il valore 22,5, potremmo chiamare la funzione nel modo
seguente

```python
print("calling")
report(22.5)
```

```output
calling
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ordine delle operazioni

1. Cosa c'è di sbagliato in questo esempio?

  ```python
  result = print_time(11, 37, 59)

  def print_time(hour, minute, second):
     time_string = str(hour) + ':' + str(minute) + ':' + str(second)
     print(time_string)
  ```

2. Dopo aver risolto il problema di cui sopra, spiegare perché eseguire questo esempio
   di codice:

  ```python
  result = print_time(11, 37, 59)
  print('result of call is:', result)
  ```

dà questo risultato:

  ```output
  11:37:59
  result of call is: None
  ```

3. Perché il risultato della chiamata è `None`?

::::::::::::::: solution

## Soluzione

1. Il problema dell'esempio è che la funzione `print_time()` viene definita *dopo* che
   la funzione è stata chiamata. Python non sa come risolvere il nome `print_time`,
   poiché non è ancora stato definito, e solleverà un `NameError`, ad esempio
   `NameError: name 'print_time' is not defined`

2. La prima riga di output `11:37:59` è stampata dalla prima riga di codice, `result =
   print_time(11, 37, 59)` che lega il valore restituito dall'invocazione `print_time`
   alla variabile `result`. La seconda riga proviene dalla seconda chiamata di stampa
   per stampare il contenuto della variabile `result`.

3. `print_time()` non restituisce esplicitamente `return` un valore, quindi restituisce
   automaticamente `None`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Incapsulamento

Compilate gli spazi vuoti per creare una funzione che prenda come argomento un singolo
nome di file, carichi i dati nel file denominato dall'argomento e restituisca il valore
minimo in quei dati.

```python
import pandas as pd

def min_in_data(____):
    data = ____
    return ____
```

::::::::::::::: solution

## Soluzione

```python
import pandas as pd

def min_in_data(filename):
    data = pd.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Trovare il primo

Riempite gli spazi vuoti per creare una funzione che prenda come argomento un elenco di
numeri e restituisca il primo valore negativo dell'elenco. Cosa fa la funzione se
l'elenco è vuoto? E se l'elenco non contiene numeri negativi?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

::::::::::::::: solution

## Soluzione

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

Se a questa funzione viene passata una lista vuota o una lista con tutti valori
positivi, essa restituisce `None`:

```python
my_list = []
print(first_negative(my_list))
```

```output
None
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Chiamato per nome

Prima abbiamo visto questa funzione:

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)
```

Abbiamo visto che possiamo chiamare la funzione usando *argomenti con nome*, in questo
modo:

```python
print_date(day=1, month=2, year=2003)
```

1. Che cosa stampa `print_date(day=1, month=2, year=2003)`?
2. Quando avete visto una chiamata di funzione come questa?
3. Quando e perché è utile chiamare le funzioni in questo modo?

::::::::::::::: solution

## Soluzione

1. `2003/2/1`
2. Abbiamo visto esempi di utilizzo di *argomenti con nome* quando si lavora con la
   libreria pandas. Per esempio, quando si legge un set di dati usando `data =
   pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')`, l'ultimo
   argomento `index_col` è un argomento con nome.
3. L'uso di argomenti con nome può rendere il codice più leggibile, poiché dalla
   chiamata di funzione si può vedere quale nome hanno i diversi argomenti all'interno
   della funzione. Inoltre, può ridurre le possibilità di passare gli argomenti
   nell'ordine sbagliato, poiché utilizzando argomenti con nome l'ordine non ha
   importanza.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Incapsulamento di un blocco Se/Stampa

Il codice seguente viene eseguito su una stampante di etichette per uova di gallina. Una
bilancia digitale comunicherà al computer la massa di un uovo di gallina (in grammi) e
il computer stamperà un'etichetta.

```python
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass)

    # egg sizing machinery prints a label
    if mass >= 85:
        print("jumbo")
    elif mass >= 70:
        print("large")
    elif mass < 70 and mass >= 55:
        print("medium")
    else:
        print("small")
```

Il blocco if che classifica le uova potrebbe essere utile in altre situazioni, quindi
per evitare di ripeterlo, potremmo ripiegarlo in una funzione, `get_egg_label()`.
Rivedendo il programma per utilizzare la funzione si otterrebbe questo:

```python
# revised version
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass, get_egg_label(mass))

```

1. Creare una definizione di funzione per `get_egg_label()` che funzioni con il
   programma rivisto sopra. Si noti che il valore di ritorno della funzione
   `get_egg_label()` sarà importante. L'esempio di output del programma precedente
   sarebbe `71.23 large`.
2. Un uovo sporco potrebbe avere una massa superiore a 90 grammi e un uovo rovinato o
   rotto probabilmente avrà una massa inferiore a 50 grammi. Modificare la funzione
   `get_egg_label()` per tenere conto di queste condizioni di errore. Un esempio di
   output potrebbe essere `25 too light, probably spoiled`.

::::::::::::::: solution

## Soluzione

```python
def get_egg_label(mass):
    # egg sizing machinery prints a label
    egg_label = "Unlabelled"
    if mass >= 90:
        egg_label = "warning: egg might be dirty"
    elif mass >= 85:
        egg_label = "jumbo"
    elif mass >= 70:
        egg_label = "large"
    elif mass < 70 and mass >= 55:
        egg_label = "medium"
    elif mass < 50:
        egg_label = "too light, probably spoiled"
    else:
        egg_label = "small"
    return egg_label
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Analisi dei dati incapsulati

Si supponga che sia stato eseguito il seguente codice:

```python
import pandas as pd

data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col=0)
japan = data_asia.loc['Japan']
```

1. Completare le affermazioni seguenti per ottenere il PIL medio del Giappone negli anni
   riportati per il 1980.

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // ____)
  avg = (japan.loc[gdp_decade + ___] + japan.loc[gdp_decade + ___]) / 2
  ```

2. Astrarre il codice precedente in un'unica funzione.

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
      ____
      ____
      ____
      return avg
  ```

3. Come generalizzereste questa funzione se non sapeste in anticipo quali anni specifici
   sono presenti come colonne nei dati? Per esempio, se avessimo anche i dati degli anni
   che terminano con 1 e 9 per ogni decennio? (Suggerimento: utilizzate le colonne per
   filtrare quelle che corrispondono al decennio, invece di enumerarle nel codice)

::::::::::::::: solution

## Soluzione

1. Il PIL medio del Giappone negli anni riportati per gli anni '80 è calcolato con:

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // 10)
  avg = (japan.loc[gdp_decade + '2'] + japan.loc[gdp_decade + '7']) / 2
  ```

2. che codifica come funzione è:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      avg = (c.loc[gdp_decade + '2'] + c.loc[gdp_decade + '7'])/2
      return avg
  ```

3. Per ottenere la media degli anni in questione, è necessario eseguire un ciclo su di
   essi:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      total = 0.0
      num_years = 0
      for yr_header in c.index: # c's index contains reported years
          if yr_header.startswith(gdp_decade):
              total = total + c.loc[yr_header]
              num_years = num_years + 1
      return total/num_years
  ```

La funzione può ora essere chiamata da:

```python
avg_gdp_in_decade('Japan','asia',1983)
```

```output
20880.023800000003
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Simulazione di un sistema dinamico

In matematica, un [sistema dinamico](https://en.wikipedia.org/wiki/Dynamical_system) è
un sistema in cui una funzione descrive la dipendenza temporale di un punto in uno
spazio geometrico. Un esempio canonico di sistema dinamico è la [mappa
logistica](https://en.wikipedia.org/wiki/Logistic_map), un modello di crescita che
calcola una nuova densità di popolazione (tra 0 e 1) in base alla densità attuale. Nel
modello, il tempo assume valori discreti 0, 1, 2, ...

1. Definire una funzione chiamata `logistic_map` che prende due input: `x`, che
   rappresenta la popolazione attuale (al tempo `t`), e un parametro `r = 1`. Questa
   funzione deve restituire un valore che rappresenta lo stato del sistema (popolazione)
   al tempo `t + 1`, utilizzando la funzione di mappatura:

`f(t+1) = r * f(t) * [1 - f(t)]`

2. Utilizzando un ciclo `for` o `while`, iterare la funzione `logistic_map` definita
   nella parte 1, partendo da una popolazione iniziale di 0,5, per un periodo di tempo
   `t_final = 10`. Memorizzate i risultati intermedi in una lista, in modo da
   accumulare, al termine del ciclo, una sequenza di valori che rappresentano lo stato
   della mappa logistica al tempo `t = [0,1,...,t_final]` (11 valori in totale).
   Stampate questo elenco per vedere l'evoluzione della popolazione.

3. Incapsulate la logica del vostro ciclo in una funzione chiamata `iterate` che prende
   la popolazione iniziale come primo input, il parametro `t_final` come secondo input e
   il parametro `r` come terzo input. La funzione deve restituire un elenco di valori
   che rappresentano lo stato della mappa logistica al tempo `t = [0,1,...,t_final]`.
   Eseguire la funzione per i periodi `t_final = 100` e `1000` e stampare alcuni dei
   valori. La popolazione sta tendendo verso uno stato stazionario?

::::::::::::::: solution

## Soluzione

1. 
  ```python
  def logistic_map(x, r):
      return r * x * (1 - x)
  ```

2. 
  ```python
  initial_population = 0.5
  t_final = 10
  r = 1.0
  population = [initial_population]

  for t in range(t_final):
      population.append( logistic_map(population[t], r) )
  ```

3. 
  ```python
  def iterate(initial_population, t_final, r):
      population = [initial_population]
      for t in range(t_final):
          population.append( logistic_map(population[t], r) )
      return population

  for period in (10, 100, 1000):
      population = iterate(0.5, period, 1)
      print(population[-1])
  ```

  ```output
  0.06945089389714401
  0.009395779870614648
  0.0009913908614406382
  ```

La popolazione sembra avvicinarsi allo zero.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Utilizzo di funzioni con condizionali in Pandas

Le funzioni contengono spesso dei condizionali. Ecco un breve esempio che indica in
quale quartile si trova l'argomento in base ai valori codificati a mano per i punti di
taglio del quartile.

```python
def calculate_life_quartile(exp):
    if exp < 58.41:
        # This observation is in the first quartile
        return 1
    elif exp >= 58.41 and exp < 67.05:
        # This observation is in the second quartile
       return 2
    elif exp >= 67.05 and exp < 71.70:
        # This observation is in the third quartile
       return 3
    elif exp >= 71.70:
        # This observation is in the fourth quartile
       return 4
    else:
        # This observation has bad data
       return None

calculate_life_quartile(62.5)
```

```output
2
```

Questa funzione verrebbe tipicamente utilizzata all'interno di un ciclo `for`, ma Pandas
ha un modo diverso e più efficiente per fare la stessa cosa, ovvero *applicare* una
funzione a un dataframe o a una parte di esso. Ecco un esempio, utilizzando la
definizione precedente.

```python
data = pd.read_csv('data/gapminder_all.csv')
data['life_qrtl'] = data['lifeExp_1952'].apply(calculate_life_quartile)
```

C'è molto in questa seconda riga, quindi esaminiamola pezzo per pezzo. Sul lato destro
di `=` iniziamo con `data['lifeExp']`, che è la colonna del dataframe chiamata `data`
etichettata `lifExp`. Utilizziamo la `apply()` per fare ciò che dice, applicare la
`calculate_life_quartile` al valore di questa colonna per ogni riga del dataframe.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- scomporre i programmi in funzioni per facilitarne la comprensione.
- Definire una funzione usando `def` con un nome, dei parametri e un blocco di codice.
- Definire una funzione non la fa funzionare.
- Gli argomenti di una chiamata di funzione sono abbinati ai suoi parametri definiti.
- Le funzioni possono restituire un risultato al chiamante usando `return`.

::::::::::::::::::::::::::::::::::::::::::::::::::



