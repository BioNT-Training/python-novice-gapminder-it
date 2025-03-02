---
title: Riferimento
---


## Riferimento

## [Esecuzione e chiusura](episodes/01-run-quit.md)

- I file Python hanno l'estensione `.py`.
- Può essere scritto in un file di testo o in un [Jupyter Notebook][jupyter].
  - I quaderni Jupyter hanno l'estensione `.ipynb`
  - I taccuini Jupyter possono essere aperti da
    [Anaconda](https://docs.continuum.io/anaconda/install) o dalla riga di comando
    digitando `$ jupyter notebook`
    - Markdown e HTML sono ammessi nelle celle markdown per documentare il codice.

## [Variabili e assegnazione](episodes/02-variables.md)

- Le variabili sono memorizzate con `=`.
  - Le stringhe sono definite tra virgolette `'...'`.
  - Gli interi e i numeri in virgola mobile sono definiti senza virgolette.
- Le variabili possono contenere lettere, cifre e trattini bassi `_`.
  - Non può iniziare con una cifra.
  - Le variabili che iniziano con caratteri di sottolineatura devono essere evitate.
- Usare `print(...)` per visualizzare i valori come testo.
- Può utilizzare l'indicizzazione delle stringhe.
  - L'indicizzazione inizia da 0.
  - La posizione è indicata tra parentesi quadre `[position]` dopo il nome della
    variabile.
  - Prende una fetta usando `[start:stop]`. Questo crea una copia di una parte della
    stringa originale.
    - `start` è l'indice del primo elemento.
    - `stop` è l'indice dell'elemento successivo all'ultimo elemento desiderato.
- Usare `len(...)` per trovare la lunghezza di una variabile o di una stringa.

## [Tipi di dati e conversione dei tipi](episodes/03-types-conversion.md)

- Ogni valore ha un tipo. Questo controlla ciò che può essere fatto con esso.
  - `int` rappresenta un numero intero
  - `float` rappresenta un numero in virgola mobile.
  - `str` rappresenta una stringa.
- Per determinare il tipo di variabile, utilizzare la funzione integrata `type(...)`,
  includendo il nome della variabile tra le parentesi.
- Modifica delle stringhe:
  - Usare `+` per concatenare le stringhe.
  - Usare `*` per ripetere una stringa.
  - I numeri e le stringhe non possono essere aggiunti ad altri.
    - Convertire una stringa in un numero intero: `int(...)`.
    - Converte un numero intero in stringa: `str(...)`.

## [Funzioni integrate e aiuto](episodes/04-built-in.md)

- Per aggiungere un commento, anteporre `#` alla cosa che non si desidera venga
  eseguita.
- Funzioni incorporate comunemente utilizzate:
  - `min()` trova il valore più piccolo.
  - `max()` trova il valore più grande.
  - `round()` arrotonda un numero in virgola mobile.
  - `help()` visualizza la documentazione della funzione tra parentesi.
    - Altri modi per ottenere aiuto sono tenere premuto `shift` e premere `tab` in
      Jupyter Notebooks.

## [Librerie](episodes/06-libraries.md)

- Importazione di una libreria:
  - Usare `import ...` per caricare una libreria.
  - Fare riferimento a questa libreria utilizzando `module_name.thing_name`.
    - `.` indica "parte di".
- Per importare un elemento specifico da una libreria: `from ... import ...`
- Per importare una libreria usando un alias: `import ... as ...`
- Importazione della libreria matematica: `import math`
  - Esempio di riferimento a un elemento con il nome del modulo: `math.cos(math.pi)`.
- Importazione della libreria di plottaggio come alias: `import matplotlib as mpl`

## [Lettura di dati tabulari in DataFrames](episodes/07-reading-tabular.md)

- Utilizzare la libreria pandas per eseguire statistiche su dati tabellari. Caricare con
  `import pandas as pd`.
  - Per leggere un csv: `pd.read_csv()`, includendo il nome del percorso tra le
    parentesi.
    - Per specificare che i valori di una colonna devono essere usati come intestazioni
      di riga: `pd.read_csv('path', index_col='column name')`, dove il percorso e il
      nome della colonna devono essere sostituiti con i valori pertinenti.
- Per ottenere ulteriori informazioni su un DataFrame, usare `DataFrame.info`,
  sostituendo `DataFrame` con il nome della variabile del DataFrame.
- Usare `DataFrame.columns` per visualizzare i nomi delle colonne.
- Usare `DataFrame.T` per trasporre un DataFrame.
- Usare `DataFrame.describe` per ottenere statistiche riassuntive sui dati.

## [Pandas DataFrames](episodes/08-data-frames.md)

- Seleziona i dati utilizzando `[i,j]`
  - Per selezionare in base alla posizione della voce: `DataFrame.iloc[..., ...]`
    - Questo include tutto tranne l'indice finale.
  - Per selezionare in base all'etichetta della voce: `DataFrame.loc[..., ...]`
    - Può selezionare più righe o colonne elencando le etichette.
    - Questo è comprensivo di entrambe le estremità.
  - Usare `:` per selezionare tutte le righe o le colonne.
- Si possono anche selezionare i dati in base ai valori usando `True` e `False`. Si
  tratta di una maschera booleana.
  - `mask = subset > 10000`
  - Possiamo quindi usarlo per selezionare i valori.
- Per usare un'operazione select-apply-combine si usa `data.apply(lambda x: x >
  x.mean())` dove `mean()` può essere qualsiasi operazione che l'utente desidera
  applicare a x.

## [Plotting](episodes/09-plotting.md)

- La libreria di plottaggio più utilizzata è `matplotlib`.
  - Di solito importato con `import matplotlib.pyplot as plt`.
  - Per tracciare un grafico si usa il comando `plt.plot(time, position)`.
  - Per creare una legenda usare `plt.legend(['label1', 'label2'], loc='upper left')`
    - Si possono anche definire etichette all'interno delle istruzioni del grafico
      usando `plt.plot(time, position, label='label')`. Per far apparire la legenda,
      usare `plt.legend()`
  - Per etichettare gli assi x e y si usano `plt.xlabel('label')` e
    `plt.ylabel('label')`.
- I DataFrame di Pandas possono essere usati per tracciare utilizzando
  `DataFrame.plot()`. Tutte le operazioni che possono essere utilizzate su un DataFrame
  possono essere applicate durante il plottaggio.
  - Per tracciare un grafico a barre `data.plot(kind='bar')`

```python
import matplotlib.puplot as plot
plt.plot(time, position, label='label')
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.legend()
```

## [Elenchi](episodi/11-elenchi.md)

- Definiti all'interno di `[...]` e separati da `,`.
  - Un elenco vuoto può essere creato utilizzando `[]`.
- Può usare `len(...)` per determinare quanti valori ci sono in un elenco.
- Può indicizzare proprio come fatto nelle lezioni precedenti.
  - L'indicizzazione può essere utilizzata per riassegnare i valori `list_name[0] =
    newvalue`.
- Per aggiungere un elemento a un elenco, usare `list_name.append()`, con l'elemento da
  aggiungere tra le parentesi.
- Per combinare due elenchi usare `list_name_1.extend(list_name_2)`.
- Per rimuovere un elemento da un elenco, usare `del list_name[index]`.

## [For Loops](episodes/12-for-loops.md)

- Iniziare un ciclo for con `for number in [1, 2, 3]:`, con le seguenti righe indentate.
  - `[1, 2, 3]` è considerato un insieme.
  - `number` è la variabile del ciclo.
  - L'azione che segue la raccolta è il corpo.
- Per iterare su una sequenza di numeri usare `range(start, end)`

```python
for number in range(0,5):
    print(number)
```

## [Condizionali](episodi/13-condizionali.md)

- Definita in modo simile a un ciclo, utilizzando `if variable conditional value:`.
  - Ad esempio, `if variable > 5:`.
- Utilizzare `elif:` per ulteriori test.
- Usare `else:` per quando l'istruzione if non è vera.
- Si possono combinare più condizionali usando `and` o `or`.
- Spesso usato in combinazione con i cicli for.
- Condizioni che possono essere utilizzate:
  - `==` uguale a.
  - `>=` maggiore o uguale a.
  - `<=` minore o uguale a.
  - `>` maggiore di.
  - `<` meno di.

```python
for m in [3, 6, 7, 2, 8]:
    if m > 5:
        print(m, 'is large')
    elif m == 5:
        print(m, 'is 5')
    else:
        print(m, 'is small')
```

## [Looping su insiemi di dati](episodes/14-looping-data-sets.md)

- Usa un ciclo for: `for filename in [file1, file2]:`
- Per trovare un insieme di file utilizzando un modello, utilizzare `glob.glob`
  - Deve essere importato prima usando `import glob`.
  - `*` indica "corrisponde a zero o più caratteri"
  - `?` indica "corrisponde esattamente a un carattere"
    - Per esempio: `glob.glob(*.txt)` troverà tutti i file che finiscono con `.txt`
      nella directory corrente.
- Combinate questi elementi scrivendo un ciclo utilizzando: `for filename in
  glob.glob(*.txt):`

```python
for filename in glob.glob(*.txt):
  data = pd.read_csv(filename)
```

## [Funzioni di scrittura](episodes/16-writing-functions.md)

- Definire una funzione utilizzando `def function_name(parameters):`. Sostituire
  `parameters` con le variabili da utilizzare quando la funzione viene eseguita.
- Eseguito utilizzando `function_name(parameters)`.
- Per restituire un risultato al chiamante, utilizzare `return ...` nella funzione.

```python
def add_numbers(a, b):
    result = a + b
    return result

add_numbers(1, 4)
```

## [Ambito delle variabili](episodes/17-scope.md)

- Una variabile locale è definita in una funzione e può essere vista e utilizzata solo
  all'interno di quella funzione.
- Una variabile globale è definita al di fuori di una funzione e può essere vista o
  utilizzata ovunque dopo la definizione.

## [Stile di programmazione](episodi/18-style.md)

- Documentate il vostro codice.
- Utilizzare nomi di variabili chiari e significativi.
- Seguire [la guida di stile PEP8](https://www.python.org/dev/peps/pep-0008) quando si
  imposta il codice.
- Utilizzare le asserzioni per verificare la presenza di errori interni.
- Utilizzare le docstringhe per fornire aiuto.

## Glossario

Argomenti : Valori passati alle funzioni.

Array : Un contenitore che contiene elementi dello stesso tipo.

Booleano : Un oggetto composto da `True` e `False`.

DataFrame : Il modo in cui Pandas rappresenta una tabella; una raccolta di serie.

Elemento : Un elemento di un elenco o di una matrice. Per una stringa, questi sono i
singoli caratteri.

Funzione : Un blocco di codice che può essere richiamato e riutilizzato altrove.

Variabile globale : Una variabile definita al di fuori di una funzione che può essere
utilizzata ovunque.

Indice : La posizione di un dato elemento.

Jupyter Notebook : Ambiente di codifica interattivo che consente una combinazione di
codice e markdown.

Libreria : Una raccolta di file contenenti funzioni utilizzate da altri programmi.

Variabile locale : Una variabile definita all'interno di una funzione che può essere
utilizzata solo all'interno di quella funzione.

Maschera : Un oggetto booleano usato per selezionare i dati da un altro oggetto.

Metodo : Un'azione legata a un particolare oggetto. Viene richiamata utilizzando
`object.method`.

Moduli : I file di una libreria che contengono funzioni utilizzate da altri programmi.

Parametri : Variabili utilizzate durante l'esecuzione di una funzione.

Serie : Una struttura dati Pandas per rappresentare una colonna.

Substringa : Una parte di una stringa.

Variabili : Nomi per i valori.





