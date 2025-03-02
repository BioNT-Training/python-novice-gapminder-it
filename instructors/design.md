---
title: Progettazione della lezione
---


::::::::::::::::::::::::::::::::::::::::: callout

## Aiuto Cercasi

**Compiliamo gli esercizi [qui sotto] (#stage-3-learning-plan) per rendere più concreto
il programma della lezione. I contributi (sia sotto forma di richieste di pull con
esercizi compilati, sia di commenti su esercizi specifici, ordinamento e tempi) sono
molto apprezzati.**


::::::::::::::::::::::::::::::::::::::::::::::::::

## Processo utilizzato

> I consigli di Michael Pollan se insegnasse programmazione in R o Python:
> 
> 1. Scrivere il codice.
> 2. Non troppo.
> 3. Principalmente tracciati.
> 
> — [Michael Koontz](https://twitter.com/_mikoontz/status/758021742078025728) {:
> .quotation}
> 

Questa lezione è stata sviluppata utilizzando una variante ridotta del processo
"Understanding by Design". Le sezioni principali sono:

1. Assunzioni sul pubblico, sul tempo, ecc. (La bozza attuale include anche alcune
   conclusioni e decisioni in questa sezione - che dovrebbero essere riformulate)

2. Risultati desiderati: obiettivi generali, valutazioni sommative a livello di mezza
   giornata, ciò che gli studenti saranno in grado di fare, ciò che gli studenti
   sapranno.

3. Piano di apprendimento: ogni episodio ha un titolo che riassume ciò che verrà
   trattato, poi stima il tempo da dedicare all'insegnamento e agli esercizi, mentre gli
   esercizi sono indicati come punti elenco.

## Fase 1: Presupposti

- pubblico
  - Studenti laureati in discipline numeriche dalla cosmologia all'archeologia
  - Chi ha manipolato i dati in fogli di calcolo e con strumenti interattivi come SAS
  - Ma non ho programmato oltre il CPD (copy-paste-despair)
- Vincoli
  - Un giorno intero 09:00-16:30
    - 06:15 ora di lezione
    - 0:45 pranzo
    - 0:30 totale per due pause caffè
  - Gli studenti utilizzano installazioni native sulle proprie macchine
    - Può utilizzare macchine virtuali o risorse cloud a discrezione dell'istruttore
    - Ma deve mantenere l'installazione locale nativa come opzione
  - Nessuna dipendenza da altri moduli Carpentry
    - In particolare, non richiede la conoscenza della shell o del controllo di versione
  - Usare il Quaderno Jupyter
    - Strumento autentico utilizzato da molti istruttori
    - non esiste un'alternativa
    - e significa che anche chi ha già visto un po' di Python probabilmente imparerà
      qualcosa
- Esempio motivante
  - Creazione di grafici 2D adatti all'inserimento in pubblicazioni
  - Si rivolge quasi a tutti
  - Rende la lezione utilizzabile da entrambe le Carpenterie
    - e significa che anche chi ha già visto un po' di Python probabilmente imparerà
      qualcosa
- Dati
  - Usare i dati di gapminder per tutto il tempo
  - Ma suddividere in più file per continente
    - Per rendere più ordinata la visualizzazione dell'output degli esempi (ad esempio,
      usare Australia/Nuova Zelanda, che è solo di due righe)
    - e consentire esempi che mostrino l'uso di insiemi di dati multipli
- Concentrarsi su Pandas invece che su NumPy
  - Rende la lezione utilizzabile sia da Data Carpentry che da Software Carpentry
  - È probabile che i novizi vogliano analizzare i dati
  - E persone con qualche esperienza precedente:
    - accetterà l'analisi dei dati come compito autentico,
    - ed è improbabile che abbiano incontrato Pandas, quindi potranno comunque trarre
      qualcosa di utile dalla lezione
- Le sfide saranno per lo più *non* "scrivere questo codice da zero"
  - Volete un sacco di esercizi brevi che possano essere completati in modo affidabile
    nel tempo stabilito
  - Quindi utilizzare MCQ, riempimento di spazi vuoti, problemi di Parsons, "modifica di
    questo codice", ecc.

## Fase 2: Risultati desiderati

### Domande

Come faccio a...

- ... leggere dati tabellari?
- ... tracciare un singolo vettore di valori?
- ... creare un grafico di una serie temporale?
- ... creare un grafico per ciascuno dei diversi set di dati?
- ... ottenere dati extra da un singolo set di dati per il plottaggio?
- ... scrivere programmi che posso leggere e riutilizzare in futuro?

### Competenze

Posso...

- ... scrivere brevi script utilizzando loop e condizionali.
- ... scrivere funzioni con un numero fisso di parametri che restituiscono un unico
  risultato.
- ... importare librerie usando alias e fare riferimento ai contenuti di tali librerie.
- ... fare semplici estrazioni e formattazioni di dati usando Pandas.

### Concetti

So...

- ...che un programma è un'apparecchiatura di laboratorio che implementa un'analisi
  - Deve essere convalidato/calibrato prima/durante l'uso
  - Rende l'analisi riproducibile, rivedibile e condivisibile
- ... che i programmi sono scritti per le persone, non per i computer
  - Nomi di variabili significativi
  - Modularità per la leggibilità e per il riutilizzo
  - Nessuna duplicazione
  - Scopo e uso del documento
- ... che non c'è magia: i programmi che usano non sono diversi in linea di principio da
  quelli che costruiscono
- ... come assegnare valori a variabili
- ... cosa sono gli interi, i float, le stringhe, gli array NumPy e i dataframe di
  Pandas
- ... come tracciare l'esecuzione di un ciclo `for`
- ...come tracciare l'esecuzione delle istruzioni `if`/`else`
- ... come creare e indicizzare elenchi
- ... come creare e indicizzare array NumPy
- ... come creare e indicizzare i dataframe Pandas
- ...come creare grafici di serie temporali
- ... la differenza tra definire e chiamare una funzione
- ... dove trovare la documentazione sulle librerie standard
- ... come scoprire cos'altro offre Python scientifico

## Fase 3: Piano di apprendimento

### Valutazione sommativa

- Midpoint: creare un grafico di serie temporali per ogni file in una directory.
- Finale: estrarre i dati da un dataframe di Pandas e creare un grafico comparativo di
  serie temporali su più righe.

### [Esecuzione e chiusura interattiva](../episodes/01-run-quit.md) (9:00)

- Insegnamento: 15 min (per problemi di impostazione)
  - Avviare Jupyter Notebook, creare nuovi notebook e uscire dal Notebook.
  - Creare celle Markdown in un blocco note.
  - Creare ed eseguire celle Python in un blocco note.
- Sfide: 0 min (considerati nel tempo di insegnamento - nessun esercizio separato)
  - Creazione di elenchi in Markdown
  - Cosa viene visualizzato quando più espressioni vengono inserite in una singola
    cella?
  - Cambiare una cella esistente da codice a Markdown
  - Rendering di equazioni in stile LaTeX

### [Variabili e assegnazione](../episodi/02-variabili.md) (9:15)

- Insegnamento: 10 min
  - Scrivere programmi che assegnano valori scalari alle variabili ed eseguono calcoli
    con tali valori.
  - Tracciare correttamente i cambiamenti di valore nei programmi che utilizzano
    l'assegnazione scalare.
- Sfide: 10 min
  - Traccia dell'esecuzione del codice che scambia due valori utilizzando una variabile
    intermedia.
  - Prevedere i valori finali delle variabili dopo diverse assegnazioni.
  - Cosa succede se si cerca di indicizzare un numero?
  - Qual è il nome migliore per una variabile, `m`, `min` o `minutes`?
  - Cosa producono le seguenti espressioni di slice?

### [Tipi di dati e conversione dei tipi](../episodi/03-conversione-tipi.md) (09:35)

- Insegnamento: 10 min
  - Spiegare le principali differenze tra numeri interi e numeri in virgola mobile.
  - Spiegare le principali differenze tra numeri e stringhe di caratteri.
  - Utilizzare le funzioni integrate per convertire tra numeri interi, numeri in virgola
    mobile e stringhe.
- Sfide: 10 min
  - Che tipo di valore è 3,4?
  - Che tipo di valore è 3,25 + 4?
  - Che tipo di valore usereste per rappresentare:
    - Numero di giorni dall'inizio dell'anno.
    - Tempo trascorso dall'inizio dell'anno.
    - Ecc.
  - Come si possono usare `//` (divisione di interi) e `%` (modulo)?
  - Cosa fa `int("3.4")`?
  - Dati questi valori float, int e stringa, quali espressioni stamperanno un risultato
    particolare?
  - Cosa vi aspettate che produca `1+2j + 3`?

### [Funzioni integrate e guida](../episodi/04-built-in.md) (09:55)

- Insegnamento: 15 min
  - Spiegare lo scopo delle funzioni.
  - Chiamare correttamente le funzioni integrate di Python.
  - Annidare correttamente le chiamate alle funzioni integrate.
  - Utilizzare la guida per visualizzare la documentazione delle funzioni integrate.
  - Descrivere correttamente le situazioni in cui si verificano SyntaxError e NameError.
- Sfide: 10 min
  - Spiegate l'ordine delle operazioni nella seguente espressione complessa.
  - Cosa produrrà ogni combinazione annidata di chiamate `min` e `max`?
  - Perché `max` e `min` non restituiscono `None` quando non vengono dati argomenti?
  - Dato ciò che abbiamo visto finora, quale espressione indice otterrà l'ultimo
    carattere di una stringa?

### [Caffè](../episodi/05-caffè.md): 15 min (10:20)

### [Librerie](../episodi/06-librerie.md) (10:35)

- Insegnamento: 10 min
  - Spiegare cosa sono le librerie software e perché i programmatori le creano e le
    usano.
  - Scrivere programmi che importano e utilizzano librerie dalla libreria standard di
    Python.
  - Trovare e leggere la documentazione delle librerie standard in modo interattivo
    (nell'interprete) e online.
- Sfide: 10 min
  - Quale funzione della libreria matematica standard si può usare per calcolare una
    radice quadrata?
  - Quale libreria usereste per selezionare un valore casuale dai dati?
  - Se `help(math)` produce un errore, cosa avete dimenticato di fare?
  - Riempite gli spazi vuoti nel codice sottostante in modo che la dichiarazione di
    importazione e il programma vengano eseguiti.

### [Lettura di dati tabellari](../episodi/07-lettura-tabellari.md) (10:55)

- Insegnamento: 10 min
  - Importare la libreria Pandas.
  - Utilizzare Pandas per caricare un semplice set di dati CSV.
  - Ottenere alcune informazioni di base su un DataFrame di Pandas.
- Sfide: 10 min
  - Leggere i dati delle Americhe e visualizzare le statistiche di riepilogo.
  - Cosa fanno `.head` e `.tail`?
  - Quali stringhe passare a `read_csv` per leggere file da altre directory?
  - Come si possono *scrivere* dati CSV?

### [DataFrames](../episodes/08-data-frames.md) (11:15)

- Insegnamento: 15 min
  - Selezionare singoli valori da un dataframe Pandas.
  - Selezionare intere righe o intere colonne da un dataframe.
  - Selezionare un sottoinsieme di righe e colonne da un dataframe con una sola
    operazione.
  - Selezionare un sottoinsieme di un dataframe in base a un singolo criterio booleano.
- Sfide: 15 min
  - Scrivete un'espressione per trovare il PIL pro capite della Serbia nel 2007.
  - Quale regola governa ciò che è (o non è) incluso nelle fette numeriche e nominate in
    Pandas?
  - Cosa fa ogni riga del seguente breve programma?
  - Cosa fanno `idxmin` e `idxmax`?
  - Scrivere espressioni per ottenere il PIL pro capite per tutti i paesi nel 1982, per
    tutti i paesi *dopo* il 1985, ecc.
  - Dato il modo in cui i suoi confini sono cambiati dal 1900, cosa fareste se vi
    chiedessero di creare una tabella del PIL pro capite della Polonia per il ventesimo
    secolo?

### [Plotting](../episodes/09-plotting.md) (11:45)

- Insegnamento: 15 min
  - Creare un grafico di serie temporali che mostri un singolo set di dati.
  - Creare un grafico a dispersione che mostri la relazione tra due serie di dati.
- Esercitazione: 15 min
  - Riempite gli spazi vuoti per tracciare il PIL minimo pro capite nel tempo per i
    paesi europei.
  - Modificare l'esempio per creare un grafico a dispersione del PIL pro capite nei
    paesi asiatici.
  - Spiegate cosa fa ogni argomento di `plot` nel seguente esempio.

### [Pranzo](../episodi/10-pranzo.md) (12:15): 45 min

### [Liste](../episodi/11-liste.md) (13:00)

- Insegnamento: 10 min
  - Spiegare perché i programmi hanno bisogno di collezioni di valori.
  - Scrivere programmi che creano elenchi piatti, li indicizzano, li tagliano e li
    modificano attraverso assegnazioni e chiamate di metodi.
- Sfide: 10 min
  - Riempite gli spazi vuoti in modo che il programma produca l'output mostrato.
  - Quanto sono grandi le seguenti fette?
  - Cosa stampano le espressioni di indice negativo?
  - Cosa fa uno "stride" in una slice?
  - Come trattano gli slices i limiti fuori range?
  - Quali sono le differenze tra l'ordinamento in questi due modi?
  - Qual è la differenza tra `new = old` e `new = old[:]`?

### [Loops](../episodes/12-for-loops.md) (13:20)

- Insegnamento: 10 min
  - Spiegare a cosa servono normalmente i cicli for.
  - Tracciare l'esecuzione di un semplice ciclo (non annidato) e indicare correttamente
    i valori delle variabili in ogni iterazione.
  - Scrivere cicli for che utilizzano lo schema Accumulator per aggregare i valori.
- Sfide: 15 min
  - Un errore di indentazione è un errore di sintassi o un errore di runtime?
  - Tracciare le righe di questo programma in quale ordine vengono eseguite.
  - Riempite gli spazi vuoti di questo programma in modo da invertire una stringa.
  - Riempite gli spazi vuoti di questa serie di esempi per esercitarvi ad accumulare
    valori.
  - Riordinate e rientrate queste righe per calcolare la somma cumulativa dei valori
    dell'elenco.

### [Condizionali](13-condizionali) (15:00)

- Insegnamento: 10 min
  - Scrivere correttamente programmi che utilizzano istruzioni if e else e semplici
    espressioni booleane (senza operatori logici).
  - Tracciare l'esecuzione di condizionali non annidati e di condizionali all'interno di
    loop.
- Sfide: 15 min
  - Traccia l'esecuzione di questa dichiarazione condizionale.
  - riempite gli spazi vuoti in modo che questa funzione sostituisca i valori negativi
    con gli zeri.
  - Modificate questo programma in modo che elabori solo i file con meno di 50 record.
  - Modificate questo programma in modo che trovi sempre i valori più grandi e più
    piccoli di una lista, indipendentemente dai valori della lista stessa.

### [Looping su insiemi di dati](14-looping-data-sets) (13:45)

- Insegnamento: 5 min
  - Essere in grado di leggere e scrivere espressioni di globbing che corrispondono a
    insiemi di file.
  - Utilizzare glob per creare elenchi di file.
  - Scrivere cicli for per eseguire operazioni sui file dati i loro nomi in un elenco.
- Sfide: 10 min
  - Quali nomi di file non corrispondono a questa espressione glob?
  - Modificate questo programma in modo che stampi il numero di record nel file più
    corto.
  - Scrivere un programma che legga e tracci tutti i set di dati regionali.

### [Caffè](15-caffè) (14:45): 15 min

### [Funzioni di scrittura](16-funzioni di scrittura) (14:00)

- Insegnamento: 10 min
  - Spiegare e identificare la differenza tra definizione di funzione e chiamata di
    funzione.
  - Scrivete una funzione che accetta un piccolo numero fisso di argomenti e produce un
    unico risultato.
- Sfide: 15 min
  - Questo codice definisce e chiama una funzione: cosa stampa quando viene eseguita?
  - Spiegate perché questo breve programma stampa le cose nell'ordine in cui le stampa.
  - Riempite gli spazi vuoti per creare una funzione che trovi il valore minimo in un
    file di dati.
  - Riempite gli spazi vuoti per creare una funzione che trovi il primo valore negativo
    in un elenco. Cosa fa la vostra funzione se l'elenco è vuoto?
  - Perché a volte è utile passare gli argomenti dando un nome ai parametri
    corrispondenti?
  - Riempite gli spazi vuoti e trasformate questo breve pezzo di codice in una funzione.

### [Ambito variabile](17-ambito) (14:25)

- Insegnamento: 10 min
  - Identificare le variabili locali e globali.
  - Identificare i parametri come variabili locali.
  - Leggere un traceback e determinare il numero di file, funzione e riga in cui si è
    verificato l'errore.
- Sfide: 10 min
  - Tracciate le modifiche ai valori di questo programma, facendo attenzione a
    distinguere i valori locali da quelli globali.

### [Stile di programmazione](18-style) (15:25)

- Insegnamento: 15 min
  - Come posso rendere i miei programmi più leggibili?
  - Come la maggior parte dei programmatori formatta il proprio codice?
  - Come possono i programmi controllare il proprio funzionamento?
- Sfide: 15 min
  - Quali righe di questo codice saranno disponibili come guida in linea?
  - Trasformare i commenti di questo programma in docstring.
  - Riscrivete questo breve programma per renderlo più leggibile.

### [Wrap-Up](19-wrap) (15:55)

- Insegnamento: 20 min
  - Nominare e localizzare i siti scientifici della comunità Python per software,
    workshop e assistenza.
- Sfide: 0 min
  - Nessuno.

### [Feedback](20-feedback) (16:15)

- Insegnamento: 0 min
- Sfide: 15 min
  - Raccolta di feedback

### Fine (16:30)



