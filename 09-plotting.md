---
title: Tracciare
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Crea un grafico di serie temporali che mostra una singola serie di dati.
- Crea un grafico a dispersione che mostra la relazione tra due serie di dati.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso tracciare i miei dati?
- Come posso salvare il mio grafico per la pubblicazione?

::::::::::::::::::::::::::::::::::::::::::::::::::

## [`matplotlib`](https://matplotlib.org/) è la libreria di grafici scientifici più utilizzata in Python.

- Comunemente si usa una sottolibreria chiamata
  [`matplotlib.pyplot`](https://matplotlib.org/stable/tutorials/introductory/pyplot.html).
- Per impostazione predefinita, Jupyter Notebook esegue il rendering dei grafici.

```python
import matplotlib.pyplot as plt
```

- I grafici semplici si creano (abbastanza) facilmente

```python
time = [0, 1, 2, 3]
position = [0, 100, 200, 300]

plt.plot(time, position)
plt.xlabel('Time (hr)')
plt.ylabel('Position (km)')
```

![](fig/9_simple_position_time_plot.svg){alt='Un grafico a linee che mostra il tempo
(ore) rispetto alla posizione (km), utilizzando i valori forniti nel blocco di codice
precedente. Per impostazione predefinita, la linea tracciata è blu su sfondo bianco e
gli assi sono stati scalati automaticamente per adattarsi all'intervallo dei dati di
input.'}

::::::::::::::::::::::::::::::::::::::::: callout

## Visualizza tutte le figure aperte

Nel nostro esempio di Jupyter Notebook, l'esecuzione della cella dovrebbe generare la
figura direttamente sotto il codice. La figura è anche inclusa nel documento del notebook per una visualizzazione futura. Tuttavia, altri ambienti Python, come una sessione Python interattiva avviata da un terminale o uno script Python eseguito dalla riga di comando, richiedono un comando aggiuntivo per visualizzare la figura.

Indica a `matplotlib` di mostrare una figura:

```python
plt.show()
```

Questo comando può essere usato anche all'interno di un blocco note, ad esempio per
visualizzare più figure se diverse sono state create da una singola cella.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Traccia i dati direttamente da un [`Pandas dataframe`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html).

- È anche possibile tracciare [Pandas
  dataframes](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).
- Prima di tracciare, convertiamo le intestazioni delle colonne da un tipo di dati
  `string` a `integer`, poiché rappresentano valori numerici, usando
  [str.replace()](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace.html)
  per rimuovere il prefisso `gpdPercap_` e poi
  [astype(int)](https://pandas.pydata.org/docs/reference/api/pandas.Series.astype.html)
  per convertire la serie di valori stringa (`['1952', '1957', ..., '2007']`) in una
  serie di interi: `[1925, 1957, ..., 2007]`.

```python
import pandas as pd

data = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')

# Estrae l’anno dagli ultimi 4 caratteri di ciascun nome di colonna.
# I nomi delle colonne attuali sono nella forma 'gdpPercap_(anno)',
# quindi vogliamo mantenere solo la parte (anno) per rendere più chiaro il grafico PIL vs anni.
# Usiamo il metodo replace(), che rimuove dalla stringa i caratteri specificati come argomento.
# Questo metodo agisce su stringhe, quindi utilizziamo replace() attraverso le funzioni vettorializzate per stringhe di Pandas (Series.str).

years = data.columns.str.replace('gdpPercap_', '')

# Converte i valori degli anni in interi e salva i risultati di nuovo nel DataFrame.

data.columns = years.astype(int)

data.loc['Australia'].plot()
```

![](fig/9_gdp_australia.svg){alt='Grafico del PIL per l'Australia'}

## Seleziona e trasforma i dati, quindi li traccia.

- Per impostazione predefinita,
  [`DataFrame.plot`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html#pandas.DataFrame.plot)
  esegue il grafico con le righe come asse X.
- È possibile trasporre i dati per tracciare serie multiple.

```python
data.T.plot()
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_australia_nz.svg){alt='Grafico del PIL per Australia e Nuova Zelanda'}

## Sono disponibili molti stili di grafico.

- Ad esempio, si può creare un grafico a barre utilizzando uno stile più sofisticato.

```python
plt.style.use('ggplot')
data.T.plot(kind='bar')
plt.ylabel('GDP per capita')
```

![](fig/9_gdp_bar.svg){alt='Grafico a barre del PIL per l'Australia'}

## I dati possono essere tracciati anche chiamando direttamente la funzione `matplotlib` `plot`.

- Il comando è `plt.plot(x, y)`
- Il colore e il formato dei marcatori possono essere specificati come argomento
  opzionale aggiuntivo, ad esempio `b-` è una linea blu, `g--` è una linea verde
  tratteggiata.

## Ottenere i dati sull'Australia dal dataframe

```python
years = data.columns
gdp_australia = data.loc['Australia']

plt.plot(years, gdp_australia, 'g--')
```

![](fig/9_gdp_australia_formatted.svg){alt='Grafico formattato del PIL per l'Australia'}

## Può tracciare molti insiemi di dati contemporaneamente.

```python
# Selezionare i dati relativi a due Paesi
gdp_australia = data.loc['Australia']
gdp_nz = data.loc['New Zealand']

# Graficali con due diversi colori.
plt.plot(years, gdp_australia, 'b-', label='Australia')
plt.plot(years, gdp_nz, 'g-', label='New Zealand')

# Creare una legenda.
plt.legend(loc='upper left')
plt.xlabel('Year')
plt.ylabel('GDP per capita ($)')
```

::::::::::::::::::::::::::::::::::::::::: callout

## Aggiunta di una legenda

Spesso quando si tracciano più insiemi di dati sulla stessa figura è auspicabile avere
una legenda che descriva i dati.

Questo può essere fatto in `matplotlib` in due fasi:

- Fornisce un'etichetta per ogni serie di dati nella figura:

```python
plt.plot(years, gdp_australia, label='Australia')
plt.plot(years, gdp_nz, label='New Zealand')
```

- Indica a `matplotlib` di creare la legenda.

```python
plt.legend()
```

Per impostazione predefinita, matplotlib tenta di posizionare la legenda in una
posizione centrale. Se si preferisce specificare una posizione, è possibile farlo con
l'argomento `loc=`, ad esempio per posizionare la legenda nell'angolo superiore sinistro del grafico, specificare `loc='upper left'`

::::::::::::::::::::::::::::::::::::::::::::::::::

![](fig/9_gdp_australia_nz_formatted.svg){alt='Grafico formattato del PIL per Australia
e Nuova Zelanda'}

- Traccia un grafico a dispersione che mette in relazione il PIL di Australia e Nuova
  Zelanda
- Utilizzare `plt.scatter` o `DataFrame.plot.scatter`

```python
plt.scatter(gdp_australia, gdp_nz)
```

![](fig/9_gdp_correlation_plt.svg){alt='Correlazione del PIL con plt.scatter'}

```python
data.T.plot.scatter(x = 'Australia', y = 'New Zealand')
```

![](fig/9_gdp_correlation_data.svg){alt='Correlazione del PIL usando
data.T.plot.scatter'}

::::::::::::::::::::::::::::::::::::::: challenge

## Minimi e massimi

Compilate gli spazi vuoti qui sotto per tracciare il PIL minimo pro capite nel tempo per tutti i paesi europei. Modificatelo di nuovo per tracciare il PIL pro capite massimo nel tempo per l'Europa.

```python
data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
data_europe.____.plot(label='min')
data_europe.____
plt.legend(loc='best')
plt.xticks(rotation=90)
```

::::::::::::::: solution

## Soluzione

```python
data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
data_europe.min().plot(label='min')
data_europe.max().plot(label='max')
plt.legend(loc='best')
plt.xticks(rotation=90)
```

![](fig/9_minima_maxima_soluzione.png){alt='Minima Massima Soluzione'}



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Correlazioni

Modificate l'esempio nelle note per creare un grafico a dispersione che mostri la
relazione tra il PIL pro capite minimo e massimo dei paesi asiatici per ogni anno
dell'insieme di dati. Quale relazione vedete (se esiste)?

::::::::::::::: solution

## Soluzione

```python
data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col='country')
data_asia.describe().T.plot(kind='scatter', x='min', y='max')
```

![](fig/9_correlazioni_soluzione1.svg){alt='Correlazioni Soluzione 1'}

Non si notano particolari correlazioni tra i valori minimi e massimi del PIL anno per
anno. Sembra che le fortune dei paesi asiatici non salgano e non scendano insieme.


:::::::::::::::::::::::::

Si può notare che la variabilità del massimo è molto più alta di quella del minimo.
Osservate gli indici di massimo e di massimo:

```python
data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col='country')
data_asia.max().plot()
print(data_asia.idxmax())
print(data_asia.idxmin())
```

::::::::::::::: solution

## Soluzione

![](fig/9_correlations_solution2.png){alt='Correlazioni Soluzione 2'}

Sembra che la variabilità di questo valore sia dovuta a un forte calo dopo il 1972.
Forse è in gioco la geopolitica? Data la predominanza dei paesi produttori di petrolio,
forse l'indice del Brent potrebbe essere un confronto interessante? Mentre il Myanmar ha costantemente il PIL più basso, la nazione con il PIL più alto ha subito variazioni più marcate.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Altre correlazioni

Questo breve programma crea un grafico che mostra la correlazione tra il PIL e
l'aspettativa di vita per il 2007, normalizzando il marker in base alla popolazione:

```python
data_all = pd.read_csv('data/gapminder_all.csv', index_col='country')
data_all.plot(kind='scatter', x='gdpPercap_2007', y='lifeExp_2007',
              s=data_all['pop_2007']/1e6)
```

Utilizzando la guida in linea e altre risorse, spiegate cosa fa ogni argomento di
`plot`.

::::::::::::::: solution

## Soluzione

![](fig/9_more_correlations_solution.svg){alt='Soluzione per più correlazioni'}

Un buon punto di partenza è la documentazione della funzione plot -
help(data\_all.plot).

kind - Come già visto, determina il tipo di grafico da disegnare.

x e y - Nome di una colonna o indice che determina quali dati saranno posizionati sugli
assi x e y del grafico

s - I dettagli sono disponibili nella documentazione di plt.scatter. Un singolo numero o un valore per ogni punto di dati. Determina la dimensione dei punti tracciati.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Salvataggio del grafico in un file

Se siete soddisfatti del grafico che vedete, potreste volerlo salvare in un file, magari per includerlo in una pubblicazione. Esiste una funzione nel modulo matplotlib.pyplot che permette di farlo:
[savefig](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.savefig.html).
Chiamando questa funzione, ad esempio con

```python
plt.savefig('my_figure.png')
```

salva la figura corrente nel file `my_figure.png`. Il formato del file viene
automaticamente dedotto dall'estensione del nome del file (altri formati sono pdf, ps,
eps e svg).

Si noti che le funzioni in `plt` fanno riferimento a una variabile globale di figura e
dopo che una figura è stata visualizzata sullo schermo (ad esempio con `plt.show`)
matplotlib farà in modo che questa variabile faccia riferimento a una nuova figura
vuota. Pertanto, assicurarsi di chiamare `plt.savefig` prima che il grafico venga
visualizzato sullo schermo, altrimenti si potrebbe trovare un file con un grafico vuoto.

Quando si usano i dataframe, i dati vengono spesso generati e tracciati sullo schermo in un'unica riga. Oltre a usare `plt.savefig`, si può salvare un riferimento alla figura corrente in una variabile locale (con `plt.gcf`) e chiamare il metodo della classe  `savefig` da quella variabile per salvare la figura su file.

```python
data.plot(kind='bar')
fig = plt.gcf() # get current figure
fig.savefig('my_figure.png')
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Rendere accessibili i grafici

Ogni volta che si generano grafici da inserire in un documento o in una presentazione,
ci sono alcune cose da fare per assicurarsi che tutti possano capire i grafici.

- Assicuratevi sempre che il testo sia abbastanza visibile da essere letto. Usate il
  parametro `fontsize` in `xlabel`, `ylabel`, `title` e `legend` e [`tick_params` con
  `labelsize`](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.tick_params.html) per aumentare la dimensione del testo dei numeri sugli assi.
- Allo stesso modo, è necessario che gli elementi del grafico siano facili da vedere.
  Usate `s` per aumentare le dimensioni dei marcatori del grafico di dispersione e
  `linewidth` per aumentare le dimensioni delle linee del grafico.
- L'uso del colore (e di nient'altro) per distinguere i diversi elementi del grafico
  renderà i grafici illeggibili a chiunque sia daltonico o abbia una stampante da
  ufficio in bianco e nero. Per le linee, il parametro `linestyle` consente di
  utilizzare diversi tipi di linee. Per i diagrammi di dispersione, il parametro
  `marker` consente di modificare la forma dei punti. Se non si è sicuri dei colori, si
  può usare [Coblis](https://www.color-blindness.com/coblis-color-blindness-simulator/)
  o [Color Oracle](https://colororacle.org/) per simulare l'aspetto dei grafici per le
  persone affette da daltonismo.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- [`matplotlib`](https://matplotlib.org/) è la libreria di grafici scientifici più
  utilizzata in Python.
- Grafica i dati direttamente da un dataframe Pandas.
- Selezionare e trasformare i dati, quindi graficarli.
- Sono disponibili molti stili di grafico: per ulteriori opzioni, consultare la [Python
  Graph Gallery](https://python-graph-gallery.com/matplotlib/).
- Si possono graficare molti insiemi di dati insieme.

::::::::::::::::::::::::::::::::::::::::::::::::::



