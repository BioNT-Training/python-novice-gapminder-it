---
title: Eseguire cicli su insiemi di dati
teaching: 5
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Essere in grado di leggere e scrivere espressioni di globbing che corrispondono a
  insiemi di file.
- Usare glob per creare elenchi di file.
- Scrivere cicli for per eseguire operazioni sui file dati i loro nomi in un elenco.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come si possono elaborare molti set di dati con un solo comando?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usare un ciclo `for` per elaborare i file con un elenco di nomi.

- Un nome di file è una stringa di caratteri.
- E gli elenchi possono contenere stringhe di caratteri.

```python
import pandas as pd
for filename in ['data/gapminder_gdp_africa.csv', 'data/gapminder_gdp_asia.csv']:
    data = pd.read_csv(filename, index_col='country')
    print(filename, data.min())
```

```output
data/gapminder_gdp_africa.csv gdpPercap_1952    298.846212
gdpPercap_1957    335.997115
gdpPercap_1962    355.203227
gdpPercap_1967    412.977514
⋮ ⋮ ⋮
gdpPercap_1997    312.188423
gdpPercap_2002    241.165877
gdpPercap_2007    277.551859
dtype: float64
data/gapminder_gdp_asia.csv gdpPercap_1952    331
gdpPercap_1957    350
gdpPercap_1962    388
gdpPercap_1967    349
⋮ ⋮ ⋮
gdpPercap_1997    415
gdpPercap_2002    611
gdpPercap_2007    944
dtype: float64
```

## Usare [`glob.glob`](https://docs.python.org/3/library/glob.html#glob.glob) per trovare insiemi di file i cui nomi corrispondono a uno schema.

- In Unix, il termine "globbing" significa "corrispondenza di un insieme di file con uno
  schema".
- Gli schemi più comuni sono:
  - `*` che significa "corrisponde a zero o più caratteri"
  - `?` che significa "corrisponde esattamente a un carattere"
- La libreria standard di Python contiene il modulo
  [`glob`](https://docs.python.org/3/library/glob.html) per fornire funzionalità di
  pattern matching
- Il modulo [`glob`](https://docs.python.org/3/library/glob.html) contiene una funzione,
  chiamata anche `glob`, per la ricerca di pattern di file
- Ad esempio, `glob.glob('*.txt')` corrisponde a tutti i file nella directory corrente i
  cui nomi terminano con `.txt`.
- Il risultato è un elenco (eventualmente vuoto) di stringhe di caratteri.

```python
import glob
print('all csv files in data directory:', glob.glob('data/*.csv'))
```

```output
all csv files in data directory: ['data/gapminder_all.csv', 'data/gapminder_gdp_africa.csv', \
'data/gapminder_gdp_americas.csv', 'data/gapminder_gdp_asia.csv', 'data/gapminder_gdp_europe.csv', \
'data/gapminder_gdp_oceania.csv']
```

```python
print('all PDB files:', glob.glob('*.pdb'))
```

```output
all PDB files: []
```

## Usare `glob` e `for` per elaborare gruppi di file.

- Aiuta molto se i file sono nominati e memorizzati in modo sistematico e coerente, in
  modo che semplici modelli trovino i dati giusti.

```python
for filename in glob.glob('data/gapminder_*.csv'):
    data = pd.read_csv(filename)
    print(filename, data['gdpPercap_1952'].min())
```

```output
data/gapminder_all.csv 298.8462121
data/gapminder_gdp_africa.csv 298.8462121
data/gapminder_gdp_americas.csv 1397.717137
data/gapminder_gdp_asia.csv 331.0
data/gapminder_gdp_europe.csv 973.5331948
data/gapminder_gdp_oceania.csv 10039.59564
```

- Questo include tutti i dati, così come i dati per regione.
- Utilizzare uno schema più specifico negli esercizi per escludere l'intero set di dati.
- Ma si noti che il minimo dell'intero insieme di dati è anche il minimo di uno degli
  insiemi di dati, il che è un bel controllo di correttezza.

::::::::::::::::::::::::::::::::::::::: challenge

## Determinazione delle corrispondenze

Quale di questi file *non* corrisponde all'espressione `glob.glob('data/*as*.csv')`?

1. `data/gapminder_gdp_africa.csv`
2. `data/gapminder_gdp_americas.csv`
3. `data/gapminder_gdp_asia.csv`

::::::::::::::: solution

## Soluzione

1 non corrisponde al glob.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Dimensione minima del file

Modificate questo programma in modo che stampi il numero di record nel file che ha il
minor numero di record.

```python
import glob
import pandas as pd
fewest = ____
for filename in glob.glob('data/*.csv'):
    dataframe = pd.____(filename)
    fewest = min(____, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Si noti che il metodo [`DataFrame.shape()`][shape-method] restituisce una tupla con il
numero di righe e colonne del data frame.

::::::::::::::: solution

## Soluzione

```python
import glob
import pandas as pd
fewest = float('Inf')
for filename in glob.glob('data/*.csv'):
    dataframe = pd.read_csv(filename)
    fewest = min(fewest, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Si potrebbe aver scelto di inizializzare la variabile `fewest` con un numero maggiore
dei numeri con cui si ha a che fare, ma questo potrebbe portare a problemi se si
riutilizza il codice con numeri più grandi. Python consente di utilizzare l'infinito
positivo, che funzionerà indipendentemente dalla grandezza dei numeri. Quali altre
stringhe speciali riconosce la funzione [`float`][float-function]?



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Confronto dei dati

Scrivere un programma che legga i set di dati regionali e tracci il PIL medio pro capite
di ogni regione nel tempo in un unico grafico. Pandas solleva un errore se incontra
colonne non numeriche nel calcolo di un dataframe, quindi potrebbe essere necessario
filtrare tali colonne o dire a pandas di ignorarle.


::::::::::::::: solution

## Soluzione

Questa soluzione costruisce un'utile legenda usando il metodo [stringa
`split`][split-method] per estrarre il `region` dal percorso
'data/gapminder\_gdp\_a\specific\_region.csv'.

```python
import glob
import pandas as pd
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1,1)
for filename in glob.glob('data/gapminder_gdp*.csv'):
    dataframe = pd.read_csv(filename)
    # extract <region> from the filename, expected to be in the format 'data/gapminder_gdp_<region>.csv'.
    # we will split the string using the split method and `_` as our separator,
    # retrieve the last string in the list that split returns (`<region>.csv`), 
    # and then remove the `.csv` extension from that string.
    # NOTE: the pathlib module covered in the next callout also offers
    # convenient abstractions for working with filesystem paths and could solve this as well:
    # from pathlib import Path
    # region = Path(filename).stem.split('_')[-1]
    region = filename.split('_')[-1][:-4]
    # extract the years from the columns of the dataframe 
    headings = dataframe.columns[1:]
    years = headings.str.split('_').str.get(1)
    # pandas raises errors when it encounters non-numeric columns in a dataframe computation
    # but we can tell pandas to ignore them with the `numeric_only` parameter
    dataframe.mean(numeric_only=True).plot(ax=ax, label=region)
    # NOTE: another way of doing this selects just the columns with gdp in their name using the filter method
    # dataframe.filter(like="gdp").mean().plot(ax=ax, label=region)
# set the title and labels
ax.set_title('GDP Per Capita for Regions Over Time')
ax.set_xticks(range(len(years)))
ax.set_xticklabels(years)
ax.set_xlabel('Year')
plt.tight_layout()
plt.legend()
plt.show()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Trattare i percorsi dei file

Il modulo [`pathlib`][pathlib-module] fornisce utili astrazioni per la manipolazione di
file e percorsi, come la restituzione del nome di un file senza l'estensione. Questo è
molto utile quando si esegue il looping di file e directory. Nell'esempio seguente,
creiamo un oggetto `Path` e ne ispezioniamo gli attributi.

```python
from pathlib import Path

p = Path("data/gapminder_gdp_africa.csv")
print(p.parent)
print(p.stem)
print(p.suffix)
```

```output
data
gapminder_gdp_africa
.csv
```

**Consiglio:** Controllare tutti gli attributi e i metodi disponibili sull'oggetto
`Path` con la funzione `dir()`.


::::::::::::::::::::::::::::::::::::::::::::::::::

[shape-method]:
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shape.html
[float-function]: https://docs.python.org/3/library/functions.html#float
[split-method]: https://docs.python.org/3/library/stdtypes.html#str.split
[pathlib-module]: https://docs.python.org/3/library/pathlib.html


:::::::::::::::::::::::::::::::::::::::: keypoints

- Usare un ciclo `for` per elaborare i file dati da un elenco di nomi.
- Usare `glob.glob` per trovare insiemi di file i cui nomi corrispondono a uno schema.
- Usare `glob` e `for` per elaborare gruppi di file.

::::::::::::::::::::::::::::::::::::::::::::::::::



