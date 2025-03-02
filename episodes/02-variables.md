---
title: Variabili e assegnazioni
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Scrivere programmi che assegnano valori scalari alle variabili ed eseguono calcoli con
  tali valori.
- Tracciare correttamente i cambiamenti di valore nei programmi che utilizzano
  l'assegnazione scalare.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come si possono memorizzare i dati nei programmi?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Usare le variabili per memorizzare i valori.

- **Variabili** sono nomi di valori.

- Nomi di variabili

  - può **solo** contenere lettere, cifre e il trattino basso `_` (tipicamente usato per
    separare le parole in nomi di variabili lunghi)
  - non può iniziare con una cifra
  - sono **sensibili alle maiuscole** (età, Age e AGE sono tre variabili diverse)

- Anche il nome deve essere significativo, in modo che l'utente o un altro programmatore
  sappia di cosa si tratta

- I nomi delle variabili che iniziano con trattini bassi, come `__alistairs_real_age`,
  hanno un significato speciale, quindi non lo faremo finché non avremo capito la
  convenzione.

- In Python il simbolo `=` assegna il valore a destra al nome a sinistra.

- La variabile viene creata quando le viene assegnato un valore.

- Qui Python assegna un'età alla variabile `age` e un nome tra virgolette alla variabile
  `first_name`.

  ```python
  age = 42
  first_name = 'Ahmed'
  ```

## Usare `print` per visualizzare i valori.

- Python ha una funzione integrata chiamata `print` che stampa le cose come testo.
- Chiamate la funzione (cioè dite a Python di eseguirla) usando il suo nome.
- Fornire i valori alla funzione (cioè le cose da stampare) tra parentesi.
- Per aggiungere una stringa alla stampa, avvolgerla in apici singoli o doppi.
- I valori passati alla funzione sono chiamati **argomenti**

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

- `print` inserisce automaticamente un singolo spazio tra gli elementi per separarli.
- e si avvolge su una nuova riga alla fine.

## Le variabili devono essere create prima di essere utilizzate.

- Se una variabile non esiste ancora o se il nome è stato scritto male, Python segnala
  un errore. (A differenza di alcuni linguaggi, che "indovinano" un valore predefinito)

```python
print(last_name)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
```

- L'ultima riga di un messaggio di errore è di solito la più informativa.
- I messaggi di errore saranno esaminati in dettaglio [più avanti]
  (17-scope.md#reading-error-messages).

::::::::::::::::::::::::::::::::::::::::: callout

## Le variabili persistono tra una cella e l'altra

Siate consapevoli che in un quaderno Jupyter è importante l'*ordine* di esecuzione delle
celle, non l'ordine in cui appaiono. Python ricorda *tutto* il codice eseguito in
precedenza, comprese le variabili definite, indipendentemente dall'ordine nel blocco
note. Pertanto, se si definiscono variabili più in basso nel blocco note e poi si
(ri)eseguono celle più in alto, quelle definite più in basso saranno ancora presenti. Ad
esempio, si creino due celle con il seguente contenuto, in quest'ordine:

```python
print(myval)
```

```python
myval = 1
```

Se lo si esegue in ordine, la prima cella darà un errore. Tuttavia, se si esegue la
prima cella *dopo* la seconda cella, verrà stampato `1`. Per evitare confusione, può
essere utile usare l'opzione `Kernel` -> `Restart & Run All` che cancella l'interprete
ed esegue tutto da zero, dall'inizio alla fine.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Le variabili possono essere usate nei calcoli.

- Possiamo usare le variabili nei calcoli come se fossero valori.
  - Ricordate che abbiamo assegnato il valore `42` a `age` qualche riga fa.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Usare un indice per ottenere un singolo carattere da una stringa.

- I caratteri (singole lettere, numeri e così via) in una stringa sono ordinati. Ad
  esempio, la stringa `'AB'` non è uguale a `'BA'`. A causa di questo ordinamento,
  possiamo trattare la stringa come un elenco di caratteri.
- A ogni posizione nella stringa (prima, seconda, ecc.) viene assegnato un numero.
  Questo numero è chiamato **indice** o talvolta pedice.
- Gli indici sono numerati a partire da 0.
- utilizzare l'indice della posizione tra parentesi quadre per ottenere il carattere in
  quella posizione.

![Una riga di codice Python, print(nome_atomo[0]), dimostra che usando l'indice zero si
ottiene solo la lettera iniziale, in questo caso 'h' per
l'elio.](fig/2_indexing.svg){alt="Spiegare l'indicizzazione stampando sottoinsiemi della
stringa"}

```python
atom_name = 'helium'
print(atom_name[0])
```

```output
h
```

## Usare una slice per ottenere una sottostringa.

- Una parte di una stringa è chiamata **sottostringa**. Una sottostringa può essere
  breve come un singolo carattere.
- Un elemento di un elenco è chiamato elemento. Ogni volta che trattiamo una stringa
  come se fosse un elenco, gli elementi della stringa sono i suoi singoli caratteri.
- Una slice è una parte di una stringa (o, più in generale, una parte di qualsiasi cosa
  simile a un elenco).
- Prendiamo una slice con la notazione `[start:stop]`, dove `start` è l'indice intero
  del primo elemento che vogliamo e `stop` è l'indice intero dell'elemento *appena*
  successivo all'ultimo elemento che vogliamo.
- La differenza tra `stop` e `start` è la lunghezza della slice.
- L'esecuzione di una slice non modifica il contenuto della stringa originale. Al
  contrario, l'acquisizione di una fetta restituisce una copia di una parte della
  stringa originale.

```python
atom_name = 'sodium'
print(atom_name[0:3])
```

```output
sod
```

## Usare la funzione integrata `len` per trovare la lunghezza di una stringa.

```python
print(len('helium'))
```

```output
6
```

- Le funzioni annidate vengono valutate dall'interno verso l'esterno, come in
  matematica.

## Python è sensibile alle maiuscole e alle minuscole.

- Python pensa che le lettere maiuscole e minuscole siano diverse, quindi `Name` e
  `name` sono variabili diverse.
- Esistono convenzioni per l'uso di lettere maiuscole all'inizio dei nomi delle
  variabili, quindi per ora useremo lettere minuscole.

## Utilizzare nomi di variabili significativi.

- A Python non interessa come si chiamano le variabili, purché rispettino le regole
  (caratteri alfanumerici e trattino basso).

```python
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
```

- Utilizzare nomi di variabili significativi per aiutare gli altri a capire cosa fa il
  programma.
- L'"altra persona" più importante è il vostro io futuro.

::::::::::::::::::::::::::::::::::::::: challenge

## Scambio di valori

Riempire la tabella che mostra i valori delle variabili di questo programma *dopo*
l'esecuzione di ogni istruzione.

```python
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    #              #              #               #
y = 3.0    #              #              #               #
swap = x   #              #              #               #
x = y      #              #              #               #
y = swap   #              #              #               #
```

::::::::::::::: solution

## Soluzione

```output
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    # 1.0          # not defined  # not defined   #
y = 3.0    # 1.0          # 3.0          # not defined   #
swap = x   # 1.0          # 3.0          # 1.0           #
x = y      # 3.0          # 3.0          # 1.0           #
y = swap   # 3.0          # 1.0          # 1.0           #
```

Queste tre righe scambiano i valori in `x` e `y` usando la variabile `swap` come memoria
temporanea. Si tratta di un idioma di programmazione piuttosto comune.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Previsione dei valori

Qual è il valore finale di `position` nel programma qui sotto? (Provate a prevedere il
valore senza eseguire il programma, poi verificate la vostra previsione)

```python
initial = 'left'
position = initial
initial = 'right'
```

::::::::::::::: solution

## Soluzione

```python
print(position)
```

```output
left
```

Alla variabile `initial` viene assegnato il valore `'left'`. Nella seconda riga, anche
la variabile `position` riceve il valore di stringa `'left'`. Nella terza riga, alla
variabile `initial` viene assegnato il valore `'right'`, ma la variabile `position`
mantiene il suo valore di stringa `'left'`.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Sfida

Se si assegna `a = 123`, cosa succede se si cerca di ottenere la seconda cifra di `a`
tramite `a[1]`?

::::::::::::::: solution

## Soluzione

I numeri non sono stringhe o sequenze e Python solleva un errore se si cerca di eseguire
un'operazione di indice su un numero. Nella [prossima lezione sui tipi e sulla
conversione dei tipi] (03-types-conversion.md) impareremo di più sui tipi e su come
convertire i diversi tipi. Se si desidera l'ennesima cifra di un numero, è possibile
convertirla in una stringa utilizzando la funzione incorporata `str` e quindi eseguire
un'operazione di indice su tale stringa.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

```python
a = str(123)
print(a[1])
```

```output
2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Scelta di un nome

Qual è il nome migliore per una variabile, `m`, `min` o `minutes`? Suggerimento: pensate
a quale codice preferireste ereditare da qualcuno che sta per lasciare il laboratorio:

1. `ts = m * 60 + s`
2. `tot_sec = min * 60 + sec`
3. `total_seconds = minutes * 60 + seconds`

::::::::::::::: solution

## Soluzione

`minutes` è meglio perché `min` potrebbe significare qualcosa come "minimo" (e in realtà
è una funzione integrata in Python che tratteremo più avanti).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Pratica di affettatura

Cosa stampa il seguente programma?

```python
atom_name = 'carbon'
print('atom_name[1:3] is:', atom_name[1:3])
```

::::::::::::::: solution

## Soluzione

```output
atom_name[1:3] is: ar
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Concetti di affettatura

Data la seguente stringa:

```python
species_name = "Acacia buxifolia"
```

Cosa restituiscono queste espressioni?

1. `species_name[2:8]`
2. `species_name[11:]` (senza un valore dopo i due punti)
3. `species_name[:4]` (senza un valore prima dei due punti)
4. `species_name[:]` (solo i due punti)
5. `species_name[11:-3]`
6. `species_name[-5:-3]`
7. Cosa succede quando si sceglie un valore `stop` che non rientra nell'intervallo?
   (cioè, provate con `species_name[0:20]` o `species_name[:103]`)

::::::::::::::: solution

## Soluzioni

1. `species_name[2:8]` restituisce la sottostringa `'acia b'`
2. `species_name[11:]` restituisce la sottostringa `'folia'`, dalla posizione 11 fino
   alla fine
3. `species_name[:4]` restituisce la sottostringa `'Acac'`, dall'inizio fino alla
   posizione 4 esclusa
4. `species_name[:]` restituisce l'intera stringa `'Acacia buxifolia'`
5. `species_name[11:-3]` restituisce la sottostringa `'fo'`, dall'undicesima posizione
   alla terzultima
6. `species_name[-5:-3]` restituisce anche la sottostringa `'fo'`, dalla quintultima
   posizione alla terzultima
7. Se una parte della slice è fuori dall'intervallo, l'operazione non fallisce.
   `species_name[0:20]` dà lo stesso risultato di `species_name[0:]` e
   `species_name[:103]` dà lo stesso risultato di `species_name[:]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Utilizzare le variabili per memorizzare i valori.
- Usare `print` per visualizzare i valori.
- Le variabili persistono tra le celle.
- Le variabili devono essere create prima di essere utilizzate.
- Le variabili possono essere utilizzate nei calcoli.
- Usare un indice per ottenere un singolo carattere da una stringa.
- Usare una slice per ottenere una sottostringa.
- Usare la funzione integrata `len` per trovare la lunghezza di una stringa.
- Python è sensibile alle maiuscole e alle minuscole.
- Utilizzare nomi di variabili significativi.

::::::::::::::::::::::::::::::::::::::::::::::::::



