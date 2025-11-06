---
title: Lettura di dati tabellari in DataFrames
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Importare la libreria Pandas.
- Utilizzare Pandas per caricare un semplice set di dati CSV.
- Ottenere alcune informazioni di base su un Pandas DataFrame.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come si leggono i dati di una tabella?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Utilizzare la libreria Pandas per eseguire statistiche su dati di una tabella.

- [Pandas](https://pandas.pydata.org/) è una libreria Python molto utilizzata per le
  statistiche, in particolare per leggere e manipolare tabelle.
- Prende in prestito molte caratteristiche dai dataframe di R.
  - Una tabella bidimensionale le cui colonne hanno nomi e potenzialmente tipi di dati
    diversi.
- Caricare Pandas con `import pandas as pd`. L'alias `pd` è comunemente usato per
  riferirsi alla libreria Pandas nel codice.
- Leggere un file di dati CSV (Comma Separated Values) con `pd.read_csv`.
  - L'argomento è il nome del file da leggere.
  - Restituisce un dataframe che può essere assegnato a una variabile

```python
import pandas as pd

data_oceania = pd.read_csv('data/gapminder_gdp_oceania.csv')
print(data_oceania)
```

```output
       country  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
0    Australia     10039.59564     10949.64959     12217.22686
1  New Zealand     10556.57566     12247.39532     13175.67800

   gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
0     14526.12465     16788.62948     18334.19751     19477.00928
1     14463.91893     16046.03728     16233.71770     17632.41040

   gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
0     21888.88903     23424.76683     26997.93657     30687.75473
1     19007.19129     18363.32494     21050.41377     23189.80135

   gdpPercap_2007
0     34435.36744
1     25185.00911
```

- Le colonne di un dataframe sono le variabili osservate e le righe sono le
  osservazioni.
- Pandas usa la backslash `\` per mostrare le righe avvolte quando l'output è troppo
  ampio per adattarsi allo schermo.
- L'uso di nomi descrittivi per i dataframe ci aiuta a distinguere tra più dataframe, in modo da evitare di sovrascrivere accidentalmente un dataframe o di leggere da quello
  sbagliato.

::::::::::::::::::::::::::::::::::::::::: callout

## File non trovato

Le nostre lezioni memorizzano i loro file di dati in una sottodirectory `data`, motivo
per cui il percorso del file è `data/gapminder_gdp_oceania.csv`. Se si dimentica di
includere `data/`, o se lo si include ma la propria copia del file si trova da qualche
altra parte, si otterrà un [runtime error](04-built-in.md) che termina con una riga come questa:

```error
FileNotFoundError: [Errno 2] No such file or directory: 'data/gapminder_gdp_oceania.csv'
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usare `index_col` per specificare che i valori di una colonna devono essere usati come intestazioni di riga.

- Le intestazioni delle righe sono numeri (0 e 1 in questo caso).
- Si vuole davvero indicizzare per paese.
- Per eseguire questa operazione, passare il nome della colonna a `read_csv` come
  parametro `index_col`.
- Il nome del dataframe `data_oceania_country` ci dice quale regione include i dati
  (`oceania`) e come sono indicizzati (`country`).

```python
data_oceania_country = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')
print(data_oceania_country)
```

```output
             gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
country
Australia       10039.59564     10949.64959     12217.22686     14526.12465
New Zealand     10556.57566     12247.39532     13175.67800     14463.91893

             gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
country
Australia       16788.62948     18334.19751     19477.00928     21888.88903
New Zealand     16046.03728     16233.71770     17632.41040     19007.19129

             gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
country
Australia       23424.76683     26997.93657     30687.75473     34435.36744
New Zealand     18363.32494     21050.41377     23189.80135     25185.00911
```

## Usare il metodo `DataFrame.info()` per saperne di più su un dataframe.

```python
data_oceania_country.info()
```

```output
<class 'pandas.core.frame.DataFrame'>
Index: 2 entries, Australia to New Zealand
Data columns (total 12 columns):
gdpPercap_1952    2 non-null float64
gdpPercap_1957    2 non-null float64
gdpPercap_1962    2 non-null float64
gdpPercap_1967    2 non-null float64
gdpPercap_1972    2 non-null float64
gdpPercap_1977    2 non-null float64
gdpPercap_1982    2 non-null float64
gdpPercap_1987    2 non-null float64
gdpPercap_1992    2 non-null float64
gdpPercap_1997    2 non-null float64
gdpPercap_2002    2 non-null float64
gdpPercap_2007    2 non-null float64
dtypes: float64(12)
memory usage: 208.0+ bytes
```

- Questo è un `DataFrame`
- Due righe denominate `'Australia'` e `'New Zealand'`
- Dodici colonne, ciascuna delle quali contiene due valori effettivi in virgola mobile a 64 bit.
  - Parleremo in seguito dei valori nulli, utilizzati per rappresentare le osservazioni
    mancanti.
- Utilizza 208 byte di memoria.

## La variabile `DataFrame.columns` memorizza informazioni sulle colonne del dataframe.

- Nota che questo è un dato,*non* un metodo. (non ha parentesi)
  - Come `math.pi`.
  - Quindi non usare `()` per cercare di chiamarlo.
- Si chiama *variabile membro*, o semplicemente *membro*.

```python
print(data_oceania_country.columns)
```

```output
Index(['gdpPercap_1952', 'gdpPercap_1957', 'gdpPercap_1962', 'gdpPercap_1967',
       'gdpPercap_1972', 'gdpPercap_1977', 'gdpPercap_1982', 'gdpPercap_1987',
       'gdpPercap_1992', 'gdpPercap_1997', 'gdpPercap_2002', 'gdpPercap_2007'],
      dtype='object')
```

## Usare `DataFrame.T` per trasporre un dataframe.

- A volte si desidera trattare le colonne come righe e viceversa.
- La trasposizione (scritta `.T`) non copia i dati, ma cambia solo la visione della tabella
- Come `columns`, è una variabile membro.

```python
print(data_oceania_country.T)
```

```output
country           Australia  New Zealand
gdpPercap_1952  10039.59564  10556.57566
gdpPercap_1957  10949.64959  12247.39532
gdpPercap_1962  12217.22686  13175.67800
gdpPercap_1967  14526.12465  14463.91893
gdpPercap_1972  16788.62948  16046.03728
gdpPercap_1977  18334.19751  16233.71770
gdpPercap_1982  19477.00928  17632.41040
gdpPercap_1987  21888.88903  19007.19129
gdpPercap_1992  23424.76683  18363.32494
gdpPercap_1997  26997.93657  21050.41377
gdpPercap_2002  30687.75473  23189.80135
gdpPercap_2007  34435.36744  25185.00911
```

## Usare `DataFrame.describe()` per ottenere statistiche di sintesi sui dati.

`DataFrame.describe()` ottiene le statistiche riassuntive solo delle colonne che hanno
dati numerici. Tutte le altre colonne vengono ignorate, a meno che non si utilizzi
l'argomento `include='all'`.

```python
print(data_oceania_country.describe())
```

```output
       gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
count        2.000000        2.000000        2.000000        2.000000
mean     10298.085650    11598.522455    12696.452430    14495.021790
std        365.560078      917.644806      677.727301       43.986086
min      10039.595640    10949.649590    12217.226860    14463.918930
25%      10168.840645    11274.086022    12456.839645    14479.470360
50%      10298.085650    11598.522455    12696.452430    14495.021790
75%      10427.330655    11922.958888    12936.065215    14510.573220
max      10556.575660    12247.395320    13175.678000    14526.124650

       gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
count         2.00000        2.000000        2.000000        2.000000
mean      16417.33338    17283.957605    18554.709840    20448.040160
std         525.09198     1485.263517     1304.328377     2037.668013
min       16046.03728    16233.717700    17632.410400    19007.191290
25%       16231.68533    16758.837652    18093.560120    19727.615725
50%       16417.33338    17283.957605    18554.709840    20448.040160
75%       16602.98143    17809.077557    19015.859560    21168.464595
max       16788.62948    18334.197510    19477.009280    21888.889030

       gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
count        2.000000        2.000000        2.000000        2.000000
mean     20894.045885    24024.175170    26938.778040    29810.188275
std       3578.979883     4205.533703     5301.853680     6540.991104
min      18363.324940    21050.413770    23189.801350    25185.009110
25%      19628.685413    22537.294470    25064.289695    27497.598692
50%      20894.045885    24024.175170    26938.778040    29810.188275
75%      22159.406358    25511.055870    28813.266385    32122.777857
max      23424.766830    26997.936570    30687.754730    34435.367440
```

- Non particolarmente utile con due soli record, ma molto utile quando ce ne sono
  migliaia.

::::::::::::::::::::::::::::::::::::::: challenge

## Lettura di altri dati

Leggere i dati contenuti in `gapminder_gdp_americas.csv` (che dovrebbe trovarsi nella
stessa directory di `gapminder_gdp_oceania.csv`) in una variabile chiamata
`data_americas` e visualizzarne le statistiche riassuntive.

::::::::::::::: solution

## Soluzione

Per leggere un CSV, si usa `pd.read_csv` e gli si passa il nome del file
`'data/gapminder_gdp_americas.csv'`. Passiamo ancora una volta il nome della colonna
`'country'` al parametro `index_col` per indicizzare per paese. Le statistiche di
riepilogo possono essere visualizzate con il metodo `DataFrame.describe()`.

```python
data_americas = pd.read_csv('data/gapminder_gdp_americas.csv', index_col='country')
data_americas.describe()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ispezione dei dati

Dopo aver letto i dati relativi alle Americhe, utilizzate `help(data_americas.head)` e
`help(data_americas.tail)` per scoprire cosa fanno `DataFrame.head` e `DataFrame.tail`.

1. Quale metodo visualizzerà le prime tre righe di questi dati?
2. Quale metodo visualizzerà le ultime tre colonne di questi dati?
   (Suggerimento: potrebbe essere necessario modificare la visualizzazione dei dati)

::::::::::::::: solution

## Soluzione

1. Possiamo controllare le prime cinque righe di `data_americas` eseguendo
   `data_americas.head()` che ci permette di visualizzare l'inizio del DataFrame. È
   possibile specificare il numero di righe che si desidera visualizzare specificando il parametro `n` nella chiamata a `data_americas.head()`. Per visualizzare le prime tre
   righe, eseguire:

  ```python
  data_americas.head(n=3)
  ```

  ```output
            continent  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
  country
  Argentina  Americas     5911.315053     6856.856212     7133.166023
  Bolivia    Americas     2677.326347     2127.686326     2180.972546
  Brazil     Americas     2108.944355     2487.365989     3336.585802

            gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
  country
  Argentina     8052.953021     9443.038526    10079.026740     8997.897412
  Bolivia       2586.886053     2980.331339     3548.097832     3156.510452
  Brazil        3429.864357     4985.711467     6660.118654     7030.835878

             gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
  country
  Argentina     9139.671389     9308.418710    10967.281950     8797.640716
  Bolivia       2753.691490     2961.699694     3326.143191     3413.262690
  Brazil        7807.095818     6950.283021     7957.980824     8131.212843

             gdpPercap_2007
  country
  Argentina    12779.379640
  Bolivia       3822.137084
  Brazil        9065.800825
  ```

2. Per controllare le ultime tre righe di `data_americas`, si usa il comando
   `americas.tail(n=3)`, analogo a `head()` usato sopra. Tuttavia, in questo caso
   vogliamo guardare le ultime tre colonne, quindi dobbiamo cambiare la nostra vista e
   usare `tail()`. Per farlo, creiamo un nuovo DataFrame in cui le righe e le colonne
   sono invertite:

  ```python
  americas_flipped = data_americas.T
  ```

Possiamo quindi visualizzare le ultime tre colonne di `americas` visualizzando le ultime tre righe di `americas_flipped`:

  ```python
  americas_flipped.tail(n=3)
  ```

  ```output
  country        Argentina  Bolivia   Brazil   Canada    Chile Colombia  \
  gdpPercap_1997   10967.3  3326.14  7957.98  28954.9  10118.1  6117.36
  gdpPercap_2002   8797.64  3413.26  8131.21    33329  10778.8  5755.26
  gdpPercap_2007   12779.4  3822.14   9065.8  36319.2  13171.6  7006.58

  country        Costa Rica     Cuba Dominican Republic  Ecuador    ...     \
  gdpPercap_1997    6677.05  5431.99             3614.1  7429.46    ...
  gdpPercap_2002    7723.45  6340.65            4563.81  5773.04    ...
  gdpPercap_2007    9645.06   8948.1            6025.37  6873.26    ...

  country          Mexico Nicaragua   Panama Paraguay     Peru Puerto Rico  \
  gdpPercap_1997   9767.3   2253.02  7113.69   4247.4  5838.35     16999.4
  gdpPercap_2002  10742.4   2474.55  7356.03  3783.67  5909.02     18855.6
  gdpPercap_2007  11977.6   2749.32  9809.19  4172.84  7408.91     19328.7

  country        Trinidad and Tobago United States  Uruguay Venezuela
  gdpPercap_1997             8792.57       35767.4  9230.24   10165.5
  gdpPercap_2002             11460.6       39097.1     7727   8605.05
  gdpPercap_2007             18008.5       42951.7  10611.5   11415.8
  ```

Questo mostra i dati che desideriamo, ma potremmo preferire la visualizzazione di tre
colonne invece che di tre righe, per cui possiamo invertirla:

  ```python
  americas_flipped.tail(n=3).T    
  ```

**Nota:** avremmo potuto eseguire quanto sopra in una sola riga di codice "concatenando"
i comandi:

  ```python
  data_americas.T.tail(n=3).T
  ```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lettura dei file in altre directory

I dati per il vostro progetto attuale sono memorizzati in un file chiamato
`microbes.csv`, che si trova in una cartella chiamata `field_data`. L'analisi viene
eseguita in un blocco note chiamato `analysis.ipynb` in una cartella sorella chiamata
`thesis`:

```output
your_home_directory
+-- field_data/
|   +-- microbes.csv
+-- thesis/
    +-- analysis.ipynb
```

Quale/i valore/i si deve passare a `read_csv` per leggere `microbes.csv` in
`analysis.ipynb`?

::::::::::::::: solution

## Soluzione

Dobbiamo specificare il percorso del file di interesse nella chiamata a `pd.read_csv`.
Dobbiamo prima 'saltare' dalla cartella `thesis` usando '../' e poi nella cartella
`field_data` usando 'field\_data/'. Quindi si può specificare il nome del file
`microbes.csv`. Il risultato è il seguente:

```python
data_microbes = pd.read_csv('../field_data/microbes.csv')
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Scrittura dei dati

Oltre alla funzione `read_csv` per leggere i dati da un file, Pandas fornisce una
funzione `to_csv` per scrivere i dataframe sui file. Applicando quanto appreso sulla
lettura dei file, scrivete uno dei vostri dataframe in un file chiamato`processed.csv`.
È possibile utilizzare `help` per ottenere informazioni su come utilizzare `to_csv`.

::::::::::::::: solution

## Soluzione

Per scrivere il DataFrame `data_americas` in un file chiamato `processed.csv`, eseguire
il seguente comando:

```python
data_americas.to_csv('processed.csv')
```

Per ottenere aiuto su `read_csv` o `to_csv`, si può eseguire, ad esempio:

```python
help(data_americas.to_csv)
help(pd.read_csv)
```

Si noti che `help(to_csv)` o `help(pd.to_csv)` generano un errore! Ciò è dovuto al fatto che `to_csv` non è una funzione globale di Pandas, ma una funzione membro di DataFrames. Ciò significa che può essere chiamata solo su un'istanza di un DataFrame, ad esempio `data_americas.to_csv` o `data_oceania.to_csv`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utilizzare la libreria Pandas per ottenere statistiche di base da tabelle.
- Utilizzare `index_col` per specificare che i valori di una colonna devono essere
  utilizzati come intestazioni di riga.
- Usare `DataFrame.info` per saperne di più su un dataframe.
- La variabile `DataFrame.columns` memorizza informazioni sulle colonne del dataframe.
- Utilizzare `DataFrame.T` per trasporre un dataframe.
- Utilizzare `DataFrame.describe` per ottenere statistiche di sintesi sui dati.

::::::::::::::::::::::::::::::::::::::::::::::::::



