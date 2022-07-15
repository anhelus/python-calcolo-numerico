# 7.1 Introduzione a NumPy

La libreria **NumPy**, nome derivante dalla crasi tra <em>Num</em>erical <em>Py</em>thon, è una tra le più utilizzate nelle applicazioni di calcolo scientifico in Python.

Nella pratica, possiamo pensare a NumPy come ad uno standard *de facto*: infatti, le classi ed i metodi messi a disposizione dalla libreria sono estensivamente utilizzate nella quasi totalità degli altri tool Python per le scienze matematiche, chimiche e fisiche, oltre che per l'ingegneria.

Partiamo nella nostra disamina dalla procedura di installazione della libreria.

## 7.1.1 Installare NumPy

!!!note "Installazione di una libreria"
    Al solito, ricordiamo che le diverse opzioni utilizzabili per installare una libreria sono descritte nel dettaglio nell'[appendice B](../../../appendix/02_libraries/lecture.md).

Per installare NumPy, ricorriamo all'utilizzo di `pip`, preferibilmente all'interno di un ambiente virtuale:

```sh
workon my-virtual-env
(my-virtual-env) pip install numpy
```

## 7.1.2 - Introduzione a NumPy

### 7.1.2.1 - Gli `ndarray`

Abbiamo visto in precedenza che per usare un package o un modulo Python all'interno dei nostri programmi dovremo per prima cosa importarlo:

```py
import numpy as np
```

Una volta importato NumPy, potremo passare ad utilizzare la struttura dati "principe" della libreria, ovvero l'*array*, analogo a quelli descritti dalla classica formulazione matematica.


Nello specifico, NumPy ci mette a disposizione gli `ndarray`, ovvero delle strutture dati in grado di rappresentare array ad $n$ dimensioni, contenenti dati di tipo *omogeneo*.

!!!tip "Nota"
    Anche `ndarray` è un'abbreviazione che sta per <em>n-d</em>imensional *array*.

Il metodo più semplice per creare un array è usare il costruttore `array` a cui viene passata una lista:

```py
>>> a = np.array([1, 2, 3])
```

### 7.1.2.2 - Array vs liste

Sono diverse le differenze che intercorrono tra un array ed una classica lista; le principali sono riassunte nella seguente tabella.

| Caratteristica | `ndarray`              | Lista                       |
| -------------- | ---------------------- | --------------------------- |
| Dimensione     | Fissa                  | Non fissa                   |
| Elementi       | Omogenei (stesso tipo) | Eterogenei (qualsiasi tipo) |
| Ambito         | Operazioni algebriche  | General-purpose             |

In pratica:

* un array ha dimensione fissa, a differenza della lista. Cambiarne la dimensione comporterà quindi la creazione di un nuovo array, e la cancellazione di quello originario;
* gli elementi di un array devono essere dello stesso tipo (tale limitazione non vale ovviamente per le liste);
* gli array sono pensati specificamente per le operazioni algebriche, laddove le liste sono pensate per degli scopi generici.

## 7.1.3 - NumPy e le operazioni algebriche

Abbiamo detto che gli array NumPy sono progettati specificamente per le operazioni algebriche. Ovviamente, ciò assume una notevole rilevanza ai nostri fini. Per capirlo, facciamo un esemplice esempio, nel quale moltiplichiamo tra loro due vettori riga *elemento-per-elemento*.

### 7.1.3.1 - Approccio con liste

Per effettuare l'operazione appena descritta potremmo usare un ciclo `for` o una list comprehension:

```py
# ciclo for
c = []
for i in range(len(a)):
    c.append(a[i]*b[i])

# list comprehension
c = [a[i] * b[i] for i in range(len(a))]
```

Il risultato dell'operazione sarà in entrambi i casi *corretto*. Tuttavia, i cicli sono computazionalmente *costosi*: ciò significa che, specialmente all'aumentare del numero di elementi contenuti nei vettori, sarà necessario pagare un costo crescente.

Questo potrebbe essere in qualche modo arginato dal ricorso ad un linguaggio più efficiente, come ad esempio il C; tuttavia, provando ad estendere il calcolo a due dimensioni, il codice diverrà:

```py
for i in range(len(a)):
    for j in range(len(b)):
        c.append(a[i][j]*b[i][j]
```

Il numero di cicli annidati aumenterà ovviamente in maniera direttamente proporzionale alla dimensionalità degli array coinvolti. Ciò implica che per un array ad $m$ dimensioni avremo altrettanti cicli annidati, con tutto ciò che ne consegue in termini di complessità di codice.

Ed è proprio in questa situazione che NumPy ci viene in aiuto. Infatti, per moltiplicare due array *di qualsiasi dimensionalità* ci basta usare la seguente istruzione:

```py
c = a * b
```

Evidentemente, una sintassi di questo tipo risulta essere molto più concisa e semplice rispetto all'uso dei cicli annidati, ed è inoltre molto simile a quella che possiamo trovare sulle formule "reali" usate nei libri di testo.

L'uso di questa sintassi si esplicita in due concetti fondamentali sui quali risulta essere basato NumPy:

* la *vettorizzazione* del codice, ovvero la possibilità di scrivere istruzioni matriciali senza usare esplicitamente dei cicli;
* il *broadcasting*, che riguarda la possibilità di usare una sintassi comune ed indipendente dalla dimensionalità degli array coinvolti nelle operazioni.
