---
title: Pandas Telai di dati
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Selezionare singoli valori da un dataframe Pandas.
- Selezionare intere righe o intere colonne da un dataframe.
- Selezionare un sottoinsieme di righe e colonne da un dataframe con una sola
  operazione.
- Selezionare un sottoinsieme di un dataframe in base a un singolo criterio booleano.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso fare un'analisi statistica di dati tabellari?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Nota sui DataFrames/Series di Pandas

Un [DataFrame][pandas-dataframe] è un insieme di [Series][pandas-series]; il DataFrame è il modo in cui Pandas rappresenta una tabella e Series è la struttura dati che Pandas
usa per rappresentare una colonna.

Pandas è costruito sulla base della libreria [Numpy][numpy], il che in pratica significa che la maggior parte dei metodi definiti per gli array Numpy si applicano alle serie/dataframe di Pandas.

Ciò che rende Pandas così interessante è la potente interfaccia per accedere ai singoli
record della tabella, la corretta gestione dei valori mancanti e le operazioni di
database relazionale tra DataFrames.

## Selezione di valori

Per accedere a un valore nella posizione `[i,j]` di un DataFrame, abbiamo due opzioni, a seconda del significato di `i` in uso. Ricordiamo che un DataFrame fornisce un *indice* per identificare le righe della tabella; una riga, quindi, ha una *posizione*
all'interno della tabella e una *etichetta*, che identifica in modo univoco la sua
*entrata* nel DataFrame.

## Usare `DataFrame.iloc[..., ...]` per selezionare i valori in base alla loro posizione (di ingresso)

- Può specificare la posizione tramite un indice numerico, analogamente alla versione 2D della selezione dei caratteri nelle stringhe.

```python
import pandas as pd
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.iloc[0, 0])
```

```output
1601.056136
```

## Usare `DataFrame.loc[..., ...]` per selezionare i valori in base alla loro etichetta (di ingresso).

- Può specificare la posizione per nome di riga e/o colonna.

```python
print(data.loc["Albania", "gdpPercap_1952"])
```

```output
1601.056136
```

## Usare `:` da solo per indicare tutte le colonne o tutte le righe.

- Proprio come la notazione di taglio usuale di Python.

```python
print(data.loc["Albania", :])
```

```output
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
```

- Si otterrebbe lo stesso risultato stampando `data.loc["Albania"]` (senza un secondo
  indice).

```python
print(data.loc[:, "gdpPercap_1952"])
```

```output
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
```

- Si otterrebbe lo stesso risultato stampando `data["gdpPercap_1952"]`
- Lo stesso risultato si otterrebbe anche stampando `data.gdpPercap_1952` (non consigliato,perché facilmente confondibile con la notazione `.` per i metodi)

## Seleziona più colonne o righe usando `DataFrame.loc` e una slice con nome.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
```

Nel codice riportato sopra, scopriamo che **l’operazione di slicing con loc è inclusiva a entrambe le estremit**à, a differenza di quella con iloc, in cui vengono selezionati tutti gli elementi fino all’indice finale escluso.

## Il risultato dello slicing può essere usato in altre operazioni.

- Di solito non si stampa solo una slice.
- Tutti gli operatori statistici che lavorano su interi DataFrame funzionano allo stesso modo anche sulle slice.
- Ad esempio, possiamo calcolare il valore massimo di una slice.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
```

```output
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
```

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
```

```output
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
```

## Usa i confronti per selezionare i dati in base al valore.

- Il confronto viene applicato elemento per elemento.
- Restituisce un dataframe di forma simile di `True` e `False`.

```python
# Usiamo solo una parte dei dati per ottenere un risultato leggibile.
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Quali valori sono maggiori di 10000 ?
print('\nWhere are values large?\n', subset > 10000)
```

```output
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
```

## Selezionare valori o celle vuote (NaN) tramite una maschera booleana.

- Un insieme di valori booleani disposto in una tabella viene talvolta chiamato *maschera (mask)*, per via del modo in cui può essere utilizzato.

```python
mask = subset > 10000
print(subset[mask])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
```

- Restituisce il valore quando la maschera è True e NaN (Not a Number) quando è False.
- Questo è utile perché i valori NaN vengono ignorati da operazioni come max, min, media, ecc.

```python
print(subset[subset > 10000].describe())
```

```output
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
```

## Raggruppa per: split-apply-combine

::::::::::::::::::::::::::::::::::::: instructor

Gli studenti hanno spesso difficoltà in questo caso, molti non lavorano con i dati e
concetti finanziari e quindi trovano i concetti dell'esempio difficili da comprendere.
Il problema più grande, tuttavia, è la linea che genera il wealth_score: questo
passaggio deve essere spiegato a fondo:
* Utilizza una conversione implicita tra valori booleani e float che non è stata
  trattata finora nel corso.
* L'argomento asse=1 deve essere spiegato chiaramente.

:::::::::::::::::::::::::::::::::::::::::::::::::

I metodi di vettorizzazione e le operazioni di raggruppamento di Pandas sono
caratteristiche che offrono agli utenti molta flessibilità nell'analisi dei dati.

Per esempio, supponiamo di voler avere una visione più chiara di come i paesi europei si dividono in base al loro PIL.

1. Possiamo dare un'occhiata dividendo i paesi in due gruppi durante gli anni presi in
   esame, quelli che hanno presentato un PIL *più alto* della media europea e quelli con un PIL *più basso*.
2. Stimiamo quindi un *punteggio di ricchezza* basato sui valori storici (dal 1962 al
   2007), dove teniamo conto di quante volte un paese ha partecipato ai gruppi di PIL
   *più bassi* o *più alti*

```python
mask_higher = data > data.mean()
wealth_score = mask_higher.aggregate('sum', axis=1) / len(data.columns)
print(wealth_score)
```

```output
country
Albania                   0.000000
Austria                   1.000000
Belgium                   1.000000
Bosnia and Herzegovina    0.000000
Bulgaria                  0.000000
Croatia                   0.000000
Czech Republic            0.500000
Denmark                   1.000000
Finland                   1.000000
France                    1.000000
Germany                   1.000000
Greece                    0.333333
Hungary                   0.000000
Iceland                   1.000000
Ireland                   0.333333
Italy                     0.500000
Montenegro                0.000000
Netherlands               1.000000
Norway                    1.000000
Poland                    0.000000
Portugal                  0.000000
Romania                   0.000000
Serbia                    0.000000
Slovak Republic           0.000000
Slovenia                  0.333333
Spain                     0.333333
Sweden                    1.000000
Switzerland               1.000000
Turkey                    0.000000
United Kingdom            1.000000
dtype: float64
```

Infine, per ogni gruppo nella tabella `wealth_score`, sommiamo il contributo
(finanziario) per tutti gli anni presi in esame utilizzando metodi concatenati:

```python
print(data.groupby(wealth_score).sum())
```

```output
          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
0.000000    36916.854200    46110.918793    56850.065437    71324.848786   
0.333333    16790.046878    20942.456800    25744.935321    33567.667670   
0.500000    11807.544405    14505.000150    18380.449470    21421.846200   
1.000000   104317.277560   127332.008735   149989.154201   178000.350040   

          gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
0.000000    88569.346898   104459.358438   113553.768507   119649.599409   
0.333333    45277.839976    53860.456750    59679.634020    64436.912960   
0.500000    25377.727380    29056.145370    31914.712050    35517.678220   
1.000000   215162.343140   241143.412730   263388.781960   296825.131210   

          gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007  
0.000000    92380.047256   103772.937598   118590.929863   149577.357928  
0.333333    67918.093220    80876.051580   102086.795210   122803.729520  
0.500000    36310.666080    40723.538700    45564.308390    51403.028210  
1.000000   315238.235970   346930.926170   385109.939210   427850.333420
```

::::::::::::::::::::::::::::::::::::::: challenge

## Selezione di valori individuali

Si supponga che Pandas sia stato importato nel notebook e che siano stati caricati i
dati del PIL di Gapminder per l'Europa:

```python
import pandas as pd

data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
```

Scrivere un'espressione per trovare il PIL pro capite della Serbia nel 2007.

::::::::::::::: solution

## Soluzione

La selezione può essere effettuata utilizzando le etichette sia per la riga ("Serbia")
sia per la colonna ("gdpPercap\_2007"):

```python
print(data_europe.loc['Serbia', 'gdpPercap_2007'])
```

L'output è

```output
9786.534714
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Estensione dell'affettatura

1. Le due istruzioni seguenti producono lo stesso risultato?
2. In base a questo, quale regola regola regola l'inclusione (o meno) nelle fette
   numeriche e nelle fette denominate in Pandas?

```python
print(data_europe.iloc[0:2, 0:2])
print(data_europe.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
```

::::::::::::::: solution

## Soluzione

No, non producono lo stesso output! L'output della prima è:

```output
        gdpPercap_1952  gdpPercap_1957
country                                
Albania     1601.056136     1942.284244
Austria     6137.076492     8842.598030
```

La seconda istruzione dà:

```output
        gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
country                                                
Albania     1601.056136     1942.284244     2312.888958
Austria     6137.076492     8842.598030    10750.721110
Belgium     8343.105127     9714.960623    10991.206760
```

È evidente che la seconda istruzione produce una colonna e una riga in più rispetto alla prima.  
Quale conclusione possiamo trarre? Vediamo che una slice numerica, 0:2, *omette*
l'indice finale (cioè l'indice 2) nell'intervallo fornito, mentre una slice denominata,
'gdpPercap\1952':'gdpPercap\1962', *include* l'elemento finale.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ricostruzione dei dati

Spiegate cosa fa ogni riga del seguente breve programma: cosa c'è in `first`, `second`,
ecc

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
second = first[first['continent'] == 'Americas']
third = second.drop('Puerto Rico')
fourth = third.drop('continent', axis = 1)
fourth.to_csv('result.csv')
```

::::::::::::::: solution

## Soluzione

Esaminiamo questo pezzo di codice riga per riga.

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
```

Questa riga carica il dataset contenente i dati sul PIL di tutti i paesi in un dataframe chiamato `first`. Il parametro `index_col='country'` seleziona quale colonna utilizzare come etichetta di riga nel dataframe.

```python
second = first[first['continent'] == 'Americas']
```

Questa riga effettua una selezione: vengono estratte solo le righe di `first` per le
quali la colonna 'continente' corrisponde a 'Americhe'. Si noti come l'espressione
booleana all'interno delle parentesi, `first['continent'] == 'Americas'`, venga
utilizzata per selezionare solo le righe in cui l'espressione è vera. Provate a stampare questa espressione! È possibile stampare anche i singoli elementi Vero/Falso?
(suggerimento: prima assegnate l'espressione a una variabile)

```python
third = second.drop('Puerto Rico')
```

Come suggerisce la sintassi, questa riga elimina la riga da `second` in cui l'etichetta
è "Porto Rico". Il dataframe risultante `third` ha una riga in meno rispetto al
dataframe originale `second`.

```python
fourth = third.drop('continent', axis = 1)
```

Anche in questo caso applichiamo la funzione drop, ma in questo caso non eliminiamo una
riga ma un'intera colonna. Per farlo, è necessario specificare anche il parametro `axis` (vogliamo eliminare la seconda colonna che ha indice 1).

```python
fourth.to_csv('result.csv')
```

Il passo finale è scrivere i dati su cui abbiamo lavorato in un file csv. Pandas
semplifica questa operazione con la funzione `to_csv()`. L'unico argomento richiesto
alla funzione è il nome del file. Si noti che il file verrà scritto nella directory da
cui è stata avviata la sessione Jupyter o Python.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Selezione degli indici

Spiegate in termini semplici cosa fanno `idxmin` e `idxmax` nel breve programma qui
sotto. Quando utilizzereste questi metodi?

```python
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.idxmin())
print(data.idxmax())
```

::::::::::::::: solution

## Soluzione

Per ogni colonna in `data`, `idxmin` restituirà il valore dell'indice corrispondente al
minimo di ogni colonna; `idxmax` farà lo stesso per il valore massimo di ogni colonna.

È possibile utilizzare queste funzioni quando si desidera ottenere l'indice di riga del
valore minimo/massimo e non il valore minimo/massimo effettivo.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Esercitarsi con la selezione

Si supponga che Pandas sia stato importato e che siano stati caricati i dati del PIL di
Gapminder per l'Europa. Scrivete un'espressione per selezionare ciascuno dei seguenti
elementi:

1. PIL pro capite per tutti i paesi nel 1982.
2. PIL pro capite per la Danimarca per tutti gli anni.
3. PIL pro capite per tutti i paesi per gli anni *dopo* il 1985.
4. PIL pro capite di ciascun Paese nel 2007 come multiplo del PIL pro capite di quel
   Paese nel 1952.

::::::::::::::: solution

## Soluzione

1:

```python
data['gdpPercap_1982']
```

2:

```python
data.loc['Denmark',:]
```

3:

```python
data.loc[:,'gdpPercap_1985':]
```

Pandas è abbastanza intelligente da riconoscere il numero alla fine dell'etichetta della colonna e non dà errore, anche se non esiste alcuna colonna denominata `gdpPercap_1985`. Questo è utile se in seguito vengono aggiunte nuove colonne al file CSV.

4:

```python
data['gdpPercap_2007']/data['gdpPercap_1952']
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Molti modi di accesso

Esistono almeno due modi per accedere a un valore o a una slice di un DataFrame: per
nome o per indice. Tuttavia, ve ne sono molti altri. Ad esempio, si può accedere a una
singola colonna o riga come oggetto `DataFrame` o `Series`.

Suggerite diversi modi di eseguire le seguenti operazioni su un DataFrame:

1. Accesso a una singola colonna
2. Accesso a una singola riga
3. Accesso a un singolo elemento del DataFrame
4. Accesso a diverse colonne
5. Accesso a diverse righe
6. accesso a un sottoinsieme di righe e colonne specifiche
7. Accesso a un sottoinsieme di intervalli di righe e di colonne

::::::::::::::: solution

## Soluzione

1\. Accedere a una singola colonna:

```python
# by name
data["col_name"]   # as a Series
data[["col_name"]] # as a DataFrame

# by name using .loc
data.T.loc["col_name"]  # as a Series
data.T.loc[["col_name"]].T  # as a DataFrame

# Dot notation (Series)
data.col_name

# by index (iloc)
data.iloc[:, col_index]   # as a Series
data.iloc[:, [col_index]] # as a DataFrame

# using a mask
data.T[data.T.index == "col_name"].T
```

2\. Accedere a una singola riga:

```python
# by name using .loc
data.loc["row_name"] # as a Series
data.loc[["row_name"]] # as a DataFrame

# by name
data.T["row_name"] # as a Series
data.T[["row_name"]].T # as a DataFrame

# by index
data.iloc[row_index]   # as a Series
data.iloc[[row_index]]   # as a DataFrame

# using mask
data[data.index == "row_name"]
```

3\. Accedere a un singolo elemento del DataFrame:

```python
# by column/row names
data["column_name"]["row_name"]         # as a Series

data[["col_name"]].loc["row_name"]  # as a Series
data[["col_name"]].loc[["row_name"]]  # as a DataFrame

data.loc["row_name"]["col_name"]  # as a value
data.loc[["row_name"]]["col_name"]  # as a Series
data.loc[["row_name"]][["col_name"]]  # as a DataFrame

data.loc["row_name", "col_name"]  # as a value
data.loc[["row_name"], "col_name"]  # as a Series. Preserves index. Column name is moved to `.name`.
data.loc["row_name", ["col_name"]]  # as a Series. Index is moved to `.name.` Sets index to column name.
data.loc[["row_name"], ["col_name"]]  # as a DataFrame (preserves original index and column name)

# by column/row names: Dot notation
data.col_name.row_name

# by column/row indices
data.iloc[row_index, col_index] # as a value
data.iloc[[row_index], col_index] # as a Series. Preserves index. Column name is moved to `.name`
data.iloc[row_index, [col_index]] # as a Series. Index is moved to `.name.` Sets index to column name.
data.iloc[[row_index], [col_index]] # as a DataFrame (preserves original index and column name)

# column name + row index
data["col_name"][row_index]
data.col_name[row_index]
data["col_name"].iloc[row_index]

# column index + row name
data.iloc[:, [col_index]].loc["row_name"]  # as a Series
data.iloc[:, [col_index]].loc[["row_name"]]  # as a DataFrame

# using masks
data[data.index == "row_name"].T[data.T.index == "col_name"].T
```

4\. Accesso a diverse colonne:

```python
# by name
data[["col1", "col2", "col3"]]
data.loc[:, ["col1", "col2", "col3"]]

# by index
data.iloc[:, [col1_index, col2_index, col3_index]]
```

5\. Accesso a diverse righe

```python
# by name
data.loc[["row1", "row2", "row3"]]

# by index
data.iloc[[row1_index, row2_index, row3_index]]
```

6\. Accedere a un sottoinsieme di righe e colonne specifiche

```python
# by names
data.loc[["row1", "row2", "row3"], ["col1", "col2", "col3"]]

# by indices
data.iloc[[row1_index, row2_index, row3_index], [col1_index, col2_index, col3_index]]

# column names + row indices
data[["col1", "col2", "col3"]].iloc[[row1_index, row2_index, row3_index]]

# column indices + row names
data.iloc[:, [col1_index, col2_index, col3_index]].loc[["row1", "row2", "row3"]]
```

7\. Accedere a un sottoinsieme di intervalli di righe e colonne

```python
# by name
data.loc["row1":"row2", "col1":"col2"]

# by index
data.iloc[row1_index:row2_index, col1_index:col2_index]

# column names + row indices
data.loc[:, "col1_name":"col2_name"].iloc[row1_index:row2_index]

# column indices + row names
data.iloc[:, col1_index:col2_index].loc["row1":"row2"]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Esplorazione dei metodi disponibili utilizzando la funzione `dir()`

Python include una funzione `dir()` che può essere utilizzata per visualizzare tutti i
metodi (funzioni) disponibili integrati in un oggetto dati. Nell'episodio 4 abbiamo
utilizzato alcuni metodi con una stringa. Ma possiamo vedere che ne sono disponibili
molti altri utilizzando la funzione `dir()`:

```python
my_string = 'Hello world!'   # creation of a string object 
dir(my_string)
```

Questo comando restituisce:

```python
['__add__',
...
'__subclasshook__',
'capitalize',
'casefold',
'center',
...
'upper',
'zfill']
```

È possibile utilizzare `help()` o <kbd>Shift</kbd>\+<kbd>Tab</kbd> per ottenere maggiori informazioni sulle funzioni di questi metodi.

Si supponga che Pandas sia stato importato e che i dati del PIL di Gapminder per
l'Europa siano stati caricati come `data`. Quindi, utilizzare `dir()` per trovare la
funzione che stampa la mediana del PIL pro-capite di tutti i paesi europei per ogni anno
in cui sono disponibili le informazioni.

::::::::::::::: solution

## Soluzione

Tra le tante scelte, `dir()` elenca la funzione `median()` come una possibilità. Quindi,

```python
data.median()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Interpretazione

I confini della Polonia sono stabili dal 1945, ma sono cambiati più volte negli anni
precedenti. Come si gestirebbe questa situazione se si dovesse creare una tabella del
PIL pro capite della Polonia per l'intero ventesimo secolo?


::::::::::::::::::::::::::::::::::::::::::::::::::

[pandas-dataframe]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html
[pandas-series]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html
[numpy]: https://www.numpy.org/


:::::::::::::::::::::::::::::::::::::::: keypoints

- Usare `DataFrame.iloc[..., ...]` per selezionare i valori in base alla posizione degli interi.
- Usare `:` da solo per indicare tutte le colonne o tutte le righe.
- Selezionare più colonne o righe utilizzando `DataFrame.loc` e una slice denominata.
- Il risultato dell'affettatura può essere utilizzato in altre operazioni.
- Utilizzare i confronti per selezionare i dati in base al valore.
- Selezionare valori o NaN utilizzando una maschera booleana.

::::::::::::::::::::::::::::::::::::::::::::::::::



