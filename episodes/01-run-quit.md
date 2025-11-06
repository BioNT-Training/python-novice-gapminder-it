---
title: Esecuzione e chiusura
teaching: 15
exercises: 0
---


::::::::::::::::::::::::::::::::::::::: objectives

- Avviare JupyterLab.
- Creare un nuovo script Python.
- Creare un Jupyter notebook.
- Arrestare il server di JupyterLab.
- Comprendere la differenza tra uno script Python e un Jupyter notebook.
- Creare celle Markdown in un notebook.
- Creare ed eseguire celle Python in un notebook.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Come posso eseguire i programmi Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

Per eseguire Python, per il resto di questo workshop useremo i [Jupyter
Notebooks][jupyter] tramite [JupyterLab][jupyterlab]. I notebook Jupyter sono molto diffusi nella scienza dei dati e nella visualizzazione e rappresentano una comoda soluzione per eseguire codice Python in modo interattivo, in cui è possibile visualizzare e condividere facilmente i risultati del proprio codice.
Esistono altri modi per modificare, gestire ed eseguire il codice. Gli sviluppatori di software spesso usano un ambiente di sviluppo integrato (IDE) come
[PyCharm](https://www.jetbrains.com/pycharm/) o [Visual Studio
Code](https://code.visualstudio.com/), oppure editor di testo come Vim o Emacs, per creare e modificare i loro programmi Python. Dopo aver modificato e salvato i programmi, è possibile eseguirli all’interno dell’IDE stesso o direttamente dalla riga di comando. I notebook Jupyter, invece, consentono di eseguire e visualizzare immediatamente i risultati del codice all’interno del notebook.

JupyterLab ha diverse funzioni utili:

- È possibile digitare, modificare, copiare e incollare facilmente blocchi di codice.
- L’autocompletamento consente di accedere rapidamente a nomi di oggetti/metodi e di scoprirne di più.
- Permette di annotare il codice con collegamenti, testo di dimensioni diverse, elenchi puntati ecc., per renderlo più accessibile a voi e ai vostri collaboratori.
- Consente di visualizzare le figure accanto al codice che le produce, per raccontare una storia completa dell’analisi.

Ogni notebook contiene una o più celle che possono contenere codice, testo o immagini.

## Iniziare con JupyterLab

JupyterLab è un server di applicazioni con interfaccia web del [Project
Jupyter][jupyter]he consente di lavorare con documenti e attività (notebook Jupyter, editor di testo, terminali e componenti personalizzati) in modo flessibile, integrato ed estensibile. JupyterLab richiede un browser ragionevolmente aggiornato (idealmente una versione corrente di Chrome, Safari o Firefox); Internet Explorer 9 e precedenti non sono *supportati*.

JupyterLab è incluso nella distribuzione Anaconda Python. Se non avete ancora installato Anaconda, consultate [le istruzioni di installazione](../learners/setup.md) per le istruzioni di installazione.

questa lezione eseguiremo JupyterLab in locale sui nostri computer, quindi non sarà necessaria una connessione a Internet oltre a quella iniziale per scaricare e installare Anaconda e JupyterLab.

- Avviare il server JupyterLab sul proprio computer.
- Usare un browser per aprire uno speciale URL localhost che si connette al server JupyterLab.
- Il server JupyterLab esegue il lavoro e il browser web visualizza il risultato.
- Digitare il codice nel browser e vedere i risultati dopo che il server JupyterLab ha terminato l’esecuzione del codice.

::::::::::::::::::::::::::::::::::::::::: callout

## JupyterLab? E i taccuini Jupyter?

JupyterLab è la [prossima tappa dell'evoluzione del Jupyter
Notebook](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html#overview).
Se avete già lavorato con i notebook Jupyter, sapete cosa aspettarvi da JupyterLab.

GGli utenti esperti interessati a un confronto più dettagliato tra le interfacce di JupyterLab e dei notebook Jupyter possono consultare la [documentazione
dell'interfaccia utente di JupyterLab][jupyterlab-ui].


::::::::::::::::::::::::::::::::::::::::::::::::::

## Avvio di JupyterLab

È possibile avviare il server JupyterLab dalla riga di comando o tramite un’applicazione chiamata Anaconda Navigator (inclusa nella distribuzione Anaconda Python).

### macOS - Riga di comando

Per avviare il server JupyterLab è necessario accedere alla riga di comando tramite Terminale. Due modi per aprirlo su Mac:

1. Nella cartella Applicazioni, aprire Utility e fare doppio clic su Terminale.
2. Premere <kbd>Comando</kbd> + <kbd>barra spaziatrice</kbd> pper aprire Spotlight, digitare Terminal e premere
   <kbd>Invio</kbd> o fare doppio clic sul risultato.

Dopo aver avviato Terminale, eseguite:

```bash
$ jupyter lab
```

### Utenti Windows - Riga di comando

Per avviare il server JupyterLab è necessario accedere all’Anaconda Prompt.

Premere <kbd>Tasto logo di Windows</kbd> e cercare `Anaconda Prompt`, e aprirlo. Poi eseguire:

```bash
$ jupyter lab
```

### Anaconda Navigator

Per avviare JupyterLab da Anaconda Navigator occorre prima
[avviare Anaconda Navigator (cliccare per istruzioni dettagliate su macOS, Windows e
Linux)](https://docs.anaconda.com/free/navigator/getting-started/#navigator-starting-navigator).
È possibile cercarlo con Spotlight su macOS (<kbd>Command</kbd> + <kbd>barra spaziatrice</kbd>), con la ricerca di Windows (tasto logo), oppure aprendo un terminale ed eseguendo
`anaconda-navigator`.

Dopo l’avvio di Anaconda Navigator, fare clic su Launch sotto JupyterLab (potrebbe essere necessario scorrere).

Ecco una schermata di una pagina di Anaconda Navigator simile a quella che dovrebbe
aprirsi su macOS o Windows.

<p align='center'>
  <img alt="Anaconda Navigator landing page" src="fig/0_anaconda_navigator_landing_page.png" width="750"/>
</p>

Ecco una schermata di una pagina di destinazione di JupyterLab che dovrebbe essere
simile a quella che si apre nel browser web predefinito dopo aver avviato il server
JupyterLab su macOS o Windows.

<p align='center'>
  <img alt="JupyterLab landing page" src="fig/0_jupyterlab_landing_page.png" width="750"/>
</p>

## L'interfaccia di JupyterLab

JupyterLab ha molte caratteristiche tipiche degli IDE tradizionali, ma è focalizzato su blocchi flessibili per il calcolo interattivo ed esplorativo.

L'interfaccia di [JupyterLab][jupyterlab-ui] omprende la Barra dei menu, una barra laterale sinistra comprimibile e l’area di lavoro principale con le schede di documenti e attività.

### Barra dei menu

La barra dei menu, in alto, espone azioni e scorciatoie. I menu predefiniti includono:

- **File:** operazioni su file e directory come *Nuovo*, *Apri*, *Chiudi*, *Salva*,
  ecc. Il menu *File* comprende anche l'azione *Shut Down* utilizzata per spegnere il
  server JupyterLab.
- **Modifica:** Azioni relative alla modifica di documenti e altre attività come *Undo*,
  *Cut*, *Copy*, *Paste*, ecc.
- **Visualizza:** Azioni che modificano l'aspetto di JupyterLab.
- **Esegui:** Azioni per l'esecuzione di codice in diverse attività come i notebooks
  e le console di codice (discusse più avanti).
- **Kernel:** Azioni per la gestione dei kernel. I kernel in Jupyter saranno spiegati in
  dettaglio più avanti.
- **Tabs:** Un elenco dei documenti e delle attività aperte nell'area di lavoro
  principale.
- **Impostazioni:** Le impostazioni comuni di JupyterLab possono essere configurate
  utilizzando questo menu. Nel menu a discesa è presente anche un'opzione *Advanced
  Settings Editor* che fornisce un controllo più preciso delle impostazioni e delle
  opzioni di configurazione di JupyterLab.
- **Help:** Un elenco di link di aiuto a JupyterLab e al kernel.

::::::::::::::::::::::::::::::::::::::::: callout

## Kernel

La [documentazione](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html)  di JupyterLab definisce i kernel come «processi separati avviati dal server che eseguono il codice in diversi linguaggi ed ambienti». Aprire un notebook avvia un kernel (un processo) che eseguirà il codice. In questa lezione useremo il kernel IPython per eseguire interattivamente codice Python 3.

L'uso di altri [kernel per altri linguaggi di programmazione](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels) di Jupyter ci permetterebbe di scrivere
ed eseguire codice in altri linguaggi di programmazione nella stessa interfaccia di
JupyterLab, come R, Java, Julia, Ruby, JavaScript, Fortran, ecc.

::::::::::::::::::::::::::::::::::::::::::::::::::

Di seguito è riportata una schermata della barra dei menu predefinita.

<p align='center'>   <img alt="JupyterLab Menu Bar" src="fig/0_jupyterlab_menu_bar.png" width="750"/>
</p>

### Barra laterale sinistra

La barra laterale sinistra contiene una serie di schede di uso comune, come il browser
dei file (che mostra il contenuto della directory in cui è stato lanciato il server
JupyterLab), l'elenco dei kernel e dei terminali in esecuzione, la tavolozza dei comandi
e l'elenco delle schede aperte nell'area di lavoro principale. Di seguito è riportata
un'immagine della barra laterale sinistra predefinita.

<p align='center'>   <img alt="JupyterLab Left Side Bar" src="fig/0_jupyterlab_left_side_bar.png" width="250"/>
</p>

La barra laterale sinistra può essere chiusa o espansa selezionando "Mostra barra
laterale sinistra" nel menu Visualizza o facendo clic sulla scheda della barra laterale
attiva.

### Area di lavoro principale

L'area di lavoro principale di JupyterLab consente di organizzare i documenti (notebook,
file di testo, ecc.) e le altre attività (terminali, console di codice, ecc.) in
pannelli di schede che possono essere ridimensionati o suddivisi. Di seguito è riportata
una schermata dell'area di lavoro principale predefinita.

Se non vedete la scheda Launcher, fate clic sul segno più blu sotto i menu "File" e
"Modifica" e apparirà.

<p align='center'>   <img alt="JupyterLab Main Work Area" src="fig/0_jupyterlab_main_work_area.png" width="750"/>
</p>

Trascinate una scheda al centro di un pannello di schede per spostare la scheda nel
pannello. Suddividere un pannello di schede trascinando una scheda a sinistra, a destra,
in alto o in basso del pannello. L'area di lavoro ha una sola attività corrente. La
scheda dell'attività corrente è contrassegnata da un bordo superiore colorato (blu per
impostazione predefinita).

## Creazione di uno script Python

- Per iniziare a scrivere un nuovo programma Python, fate clic sull'icona *Text File*
  sotto l'intestazione *Other* nel Launcher dell'area di lavoro principale.
  - È anche possibile creare un nuovo file di testo semplice selezionando *New -> Text File* dal menu *File* nella barra dei menu.
- Per convertire questo file di testo in un programma Python, selezionate l'azione
  *Save File As* dal menu *File* nella barra dei menu e date al nuovo file di
  testo un nome che termini con l'estensione `.py`.
  - L'estensione `.py` fa capire a tutti (compreso il sistema operativo) che questo file
    di testo è un programma Python.
  - Questa è una convenzione, non un requisito.

## Creazione di un quaderno Jupyter

Per aprire un nuovo notebook fare clic sull'icona Python 3 sotto l'intestazione
*Notebook* nel Launcher dell'area di lavoro principale. È anche possibile
creare un nuovo blocco note selezionando *New -> Notebook* dal menu *File* nella
barra dei menu.

Note aggiuntive sui Jupyter notebook.

- I file del notebook hanno l'estensione `.ipynb` per distinguerli dai programmi
  Python in testo semplice.
- I notebook possono essere esportati come script Python che possono essere eseguiti
  dalla riga di comando.

Di seguito è riportata una schermata di un Jupyter notebook in esecuzione all'interno di
JupyterLab. Se siete interessati a maggiori dettagli, consultate la [documentazione
ufficiale del notebook][jupyterlab-notebook-docs].

<p align='center'>   <img alt="Example Jupyter Notebook" src="fig/0_jupyterlab_notebook_screenshot.png" width="750"/>
</p>

::::::::::::::::::::::::::::::::::::::::: callout

## Come è memorizzato

- Il file del notebook è memorizzato in un formato chiamato JSON.
- Proprio come una pagina web, ciò che viene salvato è diverso da ciò che si vede nel
  browser.
- Ma questo formato consente a Jupyter di combinare codice sorgente, testo e immagini in
  un unico file.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Disporre i documenti in pannelli di schede

Nell'area di lavoro principale di JupyterLab è possibile organizzare i documenti in
pannelli di schede. Ecco un esempio tratto dalla [documentazione ufficiale][jupyterlab].

<p align='center'>   <img alt="Multi-panel JupyterLab" src="fig/0_multipanel_jupyterlab_screenshot.png" width="750"/>
</p>

Per prima cosa, create un file di testo, una console Python e una finestra di terminale e disponeteli in tre pannelli. Poi create un notebook, una finestra di terminale e un file di testo e disponeteli in tre pannelli. Infine, create la vostra combinazione di pannelli e schede. Quale combinazione ritenete più utile per il vostro flusso di lavoro?

::::::::::::::: solution

## Soluzione

Dopo aver creato le schede necessarie, trascinate una scheda al centro di un pannello per spostarla; quindi suddividete un pannello trascinando una scheda a sinistra, a destra, in alto o in basso.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Codice vs. Testo

Jupyter mescola codice e testo in diversi tipi di blocchi, chiamati celle. Spesso usiamo
il termine "codice" per indicare "il codice sorgente di un software scritto in un
linguaggio come Python". Una "cella di codice" in un blocco note è una cella che
contiene software; una "cella di testo" è una cella che contiene normale testo scritta
per gli esseri umani.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Il notebook ha le modalità Comando e Modifica.

- Premendo alternatamente <kbd>Esc</kbd> e <kbd>Ritorno</kbd>, iil bordo della cella cambia (grigio ↔ blu).
- Queste sono le modalità **Comando** (grigio) e **Modifica** (blu) del blocco note.
- La modalità comando (bordo grigio) consente di modificare le funzioni a livello di blocco note,
  mentre la modalità Modifica modifica il contenuto delle celle (bordo blu).
- In modalità Comando (esc/grigio),
  - Il tasto <kbd>b</kbd> crea una nuova cella sotto la cella attualmente selezionata.
  - il tasto <kbd>a</kbd> ne crea uno sopra.
  - Il tasto <kbd>x</kbd> cancella la cella corrente.
  - Il tasto <kbd>z</kbd> annulla l'ultima operazione della cella (che può essere una
    cancellazione, una creazione, ecc.).
- Tutte le azioni possono essere eseguite utilizzando i menu, ma ci sono molte
  scorciatoie da tastiera per velocizzare le operazioni.

::::::::::::::::::::::::::::::::::::::: challenge

## Comando Vs. Modifica
Nella pagina del notebook siete in modalità Comando o Modifica?
Passate da una modalità all’altra. Usate le scorciatoie per creare una nuova cella, eliminarla e annullare l’ultima operazione.

::::::::::::::: solution

## Soluzione

La modalità Comando ha un bordo grigio e la modalità Modifica ha un bordo blu. Usate
<kbd>Esc</kbd> e <kbd>Retro</kbd> per passare da una modalità all'altra. Dovete essere
in modalità Comando (premete <kbd>Esc</kbd> se la cella è blu). Digitare <kbd>b</kbd> o
<kbd>a</kbd>. È necessario essere in modalità Comando (premere <kbd>Esc</kbd> se la
cella è blu). Digitare <kbd>x</kbd>. È necessario essere in modalità Comando (premere
<kbd>Esc</kbd> se la cella è blu). Digitare <kbd>z</kbd>.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Utilizzare la tastiera e il mouse per selezionare e modificare le celle.

- Premendo il tasto <kbd>Invio</kbd> il bordo diventa blu e si attiva la modalità
  Modifica, che consente di digitare all'interno della cella.
- Poiché vogliamo essere in grado di scrivere molte righe di codice in una singola
  cella, premendo il tasto <kbd>Invio</kbd> in modalità Modifica (blu) si sposta il
  cursore sulla riga successiva della cella, proprio come in un editor di testo.
- Abbiamo bisogno di un altro modo per dire al blocco note che vogliamo eseguire ciò che
  è contenuto nella cella.
- Premendo insieme <kbd>Shift</kbd>\+<kbd>Ritorno</kbd> si eseguirà il contenuto della
  cella.
- Notate che i tasti <kbd>Return</kbd> e <kbd>Shift</kbd> sulla destra della tastiera
  sono uno accanto all'altro.

### Il blocco note trasformerà Markdown in una documentazione ben stampata.

- I notebook possono renderizzare file [Markdown][markdown].
  - Un semplice formato di testo per scrivere elenchi, collegamenti e altri
    elementi che potrebbero essere inseriti in una pagina Web.
  - Equivalentemente, un sottoinsieme di HTML che assomiglia a quello che si invia in
    una e-mail vecchio stile.
- Trasformate la cella corrente in una cella Markdown accedendo alla modalità Comando
  (<kbd>Esc</kbd>/grigio) e premendo il tasto <kbd>M</kbd>.
- `In [ ]:` scomparirà per indicare che non è più una cella di codice e si potrà
  scrivere in Markdown.
- Trasformate la cella corrente in una cella Codice accedendo alla modalità Comando
  (<kbd>Esc</kbd>/grigio) e premendo il tasto <kbd>y</kbd>.

### Markdown fa la maggior parte di ciò che fa l'HTML.

Tabella di esempio: sintassi Markdown e output renderizzato.

+---------------------------------------+------------------------------------------------+
| Markdown code                         | Rendered output                                |
+=======================================+================================================+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| *   Use asterisks                     | -   Use asterisks                              |
| *   to create                         | -   to create                                  |
| *   bullet lists.                     | -   bullet lists.                              |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| 1.   Use numbers                      | 1.   Use numbers                               |
| 1.   to create                        | 2.   to create                                 |
| 1.   bullet lists.                    | 3.   numbered lists.                           |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| *  You can use indents                | - You can use indents                          |
|   *  To create sublists               |   - To create sublists                         |
|   *  of the same type                 |   - of the same type                           |
| *  Or sublists                        | - Or sublists                                  |
|   1. Of different                     |   1. Of different                              |
|   1. types                            |   2. types                                     |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| # A Level-1 Heading                   | ## A Level-1 Heading                           |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| ## A Level-2 Heading (etc.)           | ### A Level-2 Heading (etc.)                   |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| Line breaks                           | Line breaks                                    |
| don't matter.                         | don't matter.                                  |
|                                       |                                                |
| But blank lines                       | But blank lines                                |
| create new paragraphs.                | create new paragraphs.                         |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+
+---------------------------------------+------------------------------------------------+
| ```                                   | <p></p>                                        |
| [Links](http://software-carpentry.org)| [Links](https://software-carpentry.org)        |
| are created with `[...](...)`.        | are created with `[...](...)`.                 |
| Or use [named links][data-carp].      | Or use [named links][data_carpentry].          |
|                                       |                                                |
| [data-carp]: http://datacarpentry.org |                                                |
| ```                                   |                                                |
+---------------------------------------+------------------------------------------------+

::::::::::::::::::::::::::::::::::::::: challenge

## Creare elenchi in Markdown

Create un elenco annidato in una cella Markdown che assomigli a:

1. Ottenere finanziamenti.
2. Fare il lavoro.
  - Esperimento di progettazione.
  - Raccogliere i dati.
  - Analizzare.
3. Scrivere.
4. Pubblica.

::::::::::::::: solution

## Soluzione

Questa sfida integra sia l'elenco numerato che l'elenco puntato. Si noti che l'elenco
puntato è rientrato di 2 spazi in modo da essere in linea con gli elementi dell'elenco
numerato.

```
1.  Ottenere finanziamenti.
2.  Fare il lavoro.
    *   Esperimento di progettazione.
    *   Raccogliere i dati.
    *   Analizzare.
3.  Scrivere.
4.  Pubblica.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Più matematica

Cosa viene visualizzato quando viene eseguita una cella Python in un blocco note che
contiene diversi calcoli? Ad esempio, cosa succede quando viene eseguita questa cella?

```python
7 * 3
2 + 1
```

::::::::::::::: solution

## Soluzione

Python restituisce l'output dell'ultimo calcolo.

```python
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Cambia una cella esistente da Codice a Markdown

Cosa succede se si scrive Python in una cella di codice e poi si passa a una cella di
Markdown? Ad esempio, inserite quanto segue in una cella di codice:

```python
x = 6 * 7 + 12
print(x)
```

e poi eseguirlo con <kbd>Shift</kbd>\+<kbd>Return</kbd> per essere sicuri che funzioni
come cella di codice. Ora tornate alla cella e usate <kbd>Esc</kbd> e poi <kbd>m</kbd>
per passare la cella a Markdown ed "eseguirla" con <kbd>Shift</kbd>\+<kbd>Return</kbd>.
Cosa è successo e come potrebbe essere utile?

::::::::::::::: solution

## Soluzione

Il codice Python viene trattato come testo Markdown. Le righe appaiono come se facessero
parte di un unico paragrafo contiguo. Questo potrebbe essere utile per attivare e
disattivare temporaneamente le celle nei quaderni che vengono utilizzati per più scopi.

```python
x = 6 * 7 + 12 print(x)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Equazioni

Il Markdown standard (come quello che stiamo usando per queste note) nnon renderizza le equazioni, ma il notebook sì. Creare una nuova cella Markdown e inserire quanto segue:

```
$\sum_{i=1}^{N} 2^{-i} \approx 1$
```

(probabilmente è più facile copiare e incollare). Cosa mostra? Cosa pensate che facciano
il trattino basso, `_`, il circonflesso, `^`, e il segno del dollaro, `$`?

::::::::::::::: solution

## Soluzione

Il notebook mostra l'equazione come verrebbe renderizzata con sintassi LaTeX.
Il segno del dollaro, `$`, è usato per indicare a Markdown che il testo intermedio è
un'equazione LaTeX. Se non si ha familiarità con LaTeX, il trattino basso, `_`, è usato
per i pedici e il circonflesso, `^`, per gli apici. Una coppia di parentesi graffe, `{`
e `}`, viene usata per raggruppare il testo in modo che l'istruzione `i=1` diventi il
pedice e `N` l'apice. Allo stesso modo, `-i` è tra parentesi graffe per rendere l'intera
istruzione l'apice di `2`. `\sum` e `\approx` sono comandi LaTeX per i simboli "somma
su" e "approssima".



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Chiusura di JupyterLab

- Dalla barra dei menu selezionare il menu "File" e poi scegliere "Shut Down" in fondo
  al menu a discesa. Verrà richiesto di confermare l’arresto del server JupyterLab(non dimenticate di salvare il vostro lavoro!). Fare clic su "Shut Down" per chiudere il server JupyterLab.
- Per riavviare il server JupyterLab è necessario eseguire nuovamente il seguente comando da una shell.

```
$ jupyter lab
```

::::::::::::::::::::::::::::::::::::::: challenge

## Chiusura di JupyterLab

Esercitatevi a chiudere e riavviare il server JupyterLab.


::::::::::::::::::::::::::::::::::::::::::::::::::



[jupyterlab]: https://jupyterlab.readthedocs.io/en/stable/
[jupyterlab-ui]: https://jupyterlab.readthedocs.io/en/stable/user/interface.html
[jupyterlab-notebook-docs]:
https://jupyterlab.readthedocs.io/en/stable/user/notebook.html
[markdown]: https://en.wikipedia.org/wiki/Markdown
[data_carpentry]: https://datacarpentry.org


:::::::::::::::::::::::::::::::::::::::: keypoints

- Gli script Python sono file di testo semplice.
- Usare il Jupyter Notebook per modificare ed eseguire Python.
- Il notebook ha le modalità Comando e Modifica.
- Usare tastiera e mouse per selezionare e modificare le celle.
- Il notebook renderizza Markdown in documentazione.
- Markdown copre gran parte delle funzionalità di HTML.

::::::::::::::::::::::::::::::::::::::::::::::::::



