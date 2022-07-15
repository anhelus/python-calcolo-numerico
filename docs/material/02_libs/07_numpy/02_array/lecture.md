# 7.2 - Gli array

Nella lezione precedente abbiamo introdotto il concetto gli array, ovvero la struttura dati "centrale" nell'ecosistema di NumPy. In questa lezione (e nelle successive) ne approfondiremo aspetti e caratteristiche principali.

## 7.2.1 - Array e liste

Di primo acchito, l'impressione che si può avere osservando gli array è che questi siano molto simili alle classiche liste. Tuttavia, come abbiamo già visto, esistono diverse differenze notevoli, riassumibili in linea di massima affermando che è preferibile usare un array quando si devono svolgere operazioni di tipo matematico su dati omogenei.

Gli array NumPy sono istanze della classe `ndarray`, crasi che sta per $n$-dimensional array. Mediante questa classe possiamo rappresentare strutture dati con un numero arbitrario di dimensioni, ovvero vettori, matrici e tensori.

Il primo passo per utilizzare un array è, come accennato in precedenza, crearlo. In tal senso, ci sono diversi metodi, ma ricordiamo di seguito quello più "semplice", che prevede l'uso del costruttore `array()` a cui passare una lista di elementi dello stesso tipo:

```py
>>> a = np.array([1, 2, 3, 4, 5, 6])
>>> a
array([1, 2, 3, 4, 5, 6])
```

Passando invece una lista i cui elementi sono a loro volta delle liste, potremo ottenere in uscita un array multidimensionale:

```py
>>> b = np.array([[1, 2, 3], [4, 5, 6]])
>>> b
array([[1, 2, 3],
       [4, 5, 6]])
```

Notiamo infine che gli array non sono necessariamente numerici. Possiamo, ad esempio, creare un array di stringhe:

```py
>>> c = np.array(["s1", "s2"])
>>> c
array(['s1', 's2'], dtype='<U2')
```

### 7.2.1.1 - Array eterogenei

In precedenza si è accennato al fatto che gli array, a differenza delle liste, debbano contenere dati omogenei. Cosa succederebbe quindi se provassimo a passare al metodo `array()` una lista composta da dati di tipo eterogeneo? Partiamo verificando cosa accade ad esempio usando un intero ed un float.

```py
>>> d = np.array([1, 1.])
>>> d
array([1., 1.])
```

Notiamo subito che è stata effettuata in maniera implicita ed automatica un'operazione di conversione di tipo, e tutti i valori passati sono stati convertiti in formato float.

Interessante è anche valutare cosa accade se proviamo a passare una lista contenente un numero ed una stringa:

```py
>>> e = np.array([1, "s3"])
>>> e
array(['1', 's3'], dtype='<U11')
```

Notiamo come anche in questo caso sia stata effettuata una conversione di tipo, passando stavolta da intero a stringa.

!!!note "Upcasting"
	La regola da tenere a mente è che NumPy (e, in generale, Python) seguono il principio dell'*upcasting*: in altre parole, quando deve essere fatta una conversione tra diversi tipi di dati, si fa in modo di scegliere il tipo a più alta precisione, minimizzando i rischi di perdita di informazioni.

## 7.2.2 - Il numero di elementi di un array

Gli array NumPy hanno dimensione prefissata, e sono quindi in grado di contenere un numero fisso di oggetti di un certo tipo. Per definire (o conoscere) questo valore si utilizza una proprietà chiamata `shape` che, a grandi linee, rappresenta la *forma* dell'array. La shape di un array è in pratica una tupla di numeri interi, ovviamente non negativi, ciascuno dei quali determina il numero di elementi per ciascuna delle dimensioni dell'array.

Creiamo ad esempio un array che rappresenti una matrice $2 \times 3$, ovvero a due righe e tre colonne:

```py
>>> a = np.array([[1, 2, 3], [4, 5, 6]])
>>> a
array([[1, 2, 3],
       [4, 5, 6]])
```

Vediamo che valore assume la proprietà `shape` di questo array:

```py
>>> a.shape
(2, 3)
```

Come ci aspettavamo, il nostro array ha cardinalità due sulla prima dimensione (ovvero il numero di righe) e tre sulla seconda (ovvero il numero di colonne).

## 7.2.3 - Altri metodi per creare un array

Oltre al metodo visto in precedenza, possiamo creare un array utilizzando direttamente il costruttore della classe `ndarray`:

```py
>>> a = np.ndarray([3, 3])       # oppure a = np.ndarray(shape=(3, 3))
>>> a
array([[0.00000000e+000, 0.00000000e+000, 0.00000000e+000],
       [0.00000000e+000, 0.00000000e+000, 3.02368175e-321],
       [6.69431255e+151, 1.68534231e+246, 6.69431467e+151]])
```

Notiamo che il costruttore accetta una lista contenente la shape dell'array, che in questo caso diverrà un $3 \times 3$.

!!!note "Nota"
    Notiamo come i numeri con cui viene "riempito" l'array sono al momento casuali.

Oltre a questa tecnica base, esistono diversi modi per creare array di un certo tipo. Vediamoli in breve.

### 7.2.3.1 - Array con valori zero ed unitari

Possiamo creare un array di dimensioni arbitrarie in cui tutti gli elementi sono pari ad 1. Per farlo, usiamo la funzione `ones()`:

```py
>>> u = np.ones(shape=(3, 3))
>>> u
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])
```

In modo simile, possiamo creare array di dimensioni arbitrarie in cui tutti gli elementi sono pari a zero mediante la funzione `zeros()`:

```py
>>> z = np.zeros(shape=(3, 3))
>>> z
array([[0., 0., 0.],
       [0., 0., 0.],
       [0., 0., 0.]])
```

### 7.2.3.2 - Array vuoti

Possiamo creare un array vuoto mediante la funzione `empty()`:

```py
>>> e = np.empty(shape=(3, 3))
>>> e
array([[0.00000000e+000, 0.00000000e+000, 0.00000000e+000],
       [0.00000000e+000, 0.00000000e+000, 1.67982320e-321],
       [5.96555652e-302, 1.14188703e-104, 9.91401238e-278]])
```

Questa funzione può risultare utile quando vogliamo preallocare spazio per un array.

!!!note "Nota"
    I più attenti avranno notato che, in realtà, l'array generato da `empty()` non è vuoto, ma contiene valori casuali. In tal senso, dà risultati equivalenti all'uso diretto del costruttore `ndarray()`.

### 7.2.3.4 - Matrice identità

Possiamo creare una matrice identità usando la funzione `eye()`:

```py
>>> i = np.eye(3)
>>> i
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])
```

!!!warning "Attenzione"
    In questo caso, notiamo come non si possa passare una tupla o una lista per indicare le dimensioni dell'array. Tuttavia, possiamo specificare sia il numero delle righe (con il primo parametro) che il numero delle colonne (con il secondo parametro).

### 7.2.3.5 - Matrici diagonali

La funzione `diag()` viene usata sia per *creare* una matrice diagonale a partire da un vettore (che, ovviamente, sarà poi la diagonale della matrice), sia per *estrarre* la diagonale di una matrice. Per capire questa dualità, immaginiamo per prima cosa di avere a disposizione un vettore riga a tre elementi, che vogliamo trasformare in modo tale che si comporti come la diagonale di una matrice.

```py
>>> x = np.array([5, 2, 3])
>>> x
array([5, 2, 3])
```

Potremo creare una matrice diagonale a partire da questo vettore passandolo come parametro alla funzione `diag()`:

```py
>>> d = np.diag(x)
>>> d
array([[5, 0, 0],
       [0, 2, 0],
       [0, 0, 3]])
```

Vediamo invece come affrontare il problema duale. Immaginiamo di avere quindi un array, e volerne estrarre la diagonale:

```py
>>> x = np.array([[5, 5, 5], [2, 1, 3], [4, 3, 6]])
>>> x
array([[5, 2, 2],
       [2, 1, 3],
       [4, 3, 6]])
```

Per farlo, dovremo anche questa volta usare la funzione `diag()`:

```py
>>> d = np.diag(x)
>>> d
array([5, 1, 6])
```

!!!tip "Suggerimento"
    Il fatto che la funzione `diag()` sia usata per operazioni duali può, a ragione, causare confusione. Basta però ricordare che passando un vettore si ottiene una matrice, mentre passando una matrice si ottiene un vettore, ed il gioco è fatto.

!!!warning "Attenzione"
    Ovviamente, la funzione `diag()` accetta solo input monodimensionali (vettori) e bidimensionali (matrici)!

### 7.2.3.6 - Matrici triangolari

Concludiamo questa breve carrellata mostrando due metodi in grado di estrarre la matrice triangolare, rispettivamente superiore ed inferiore.

Supponiamo di avere la matrice x definita in precedenza. Per estrarre la matrice triangolare superiore, dovremo usare la funzione `triu()`:

```py
>>> tu = np.triu(x)
>>> tu
array([[5, 2, 2],
       [0, 1, 3],
       [0, 0, 6]])
```

Per estrarre invece la matrice triangolare inferiore, dovremo usare la funzione `tril()`:

```py
>>> tl = np.tril(x)
>>> tl
array([[5, 0, 0],
       [2, 1, 0],
       [4, 3, 6]])
```

!!!tip "Suggerimento"
    In questo caso, le funzioni `tril()` e `triu()` possono tranquillamente essere applicate agli array n-dimensionali. Inoltre, non è richiesto le diverse dimensioni dell'array abbiano la stessa cardinalità.

## 7.2.4 - Accesso agli elementi di un array

Così come per le liste, il modo più immediato per accedere al valore di un elemento in un array è usare l'operatore `[]`, specificando contestualmente l'indice dell'elemento cui si vuole accedere. Ad esempio, per selezionare il primo elemento di un vettore:

```py
>>> a = np.array([1, 2, 3, 4])
>>> a[0]
1
```

Nel caso di array ad $n$ dimensioni, è necessario indicare l'indice per ciascuna delle dimensioni dell'array. Ad esempio, per un array bidimensionale potremmo selezionare l'elemento alla prima riga e prima colonna con una sintassi di questo tipo:

```py
>>> b = np.array([[1, 2], [3, 4]])
>>> b[0][0]
1
```

## 7.2.5 - Maschere booleane

Possiamo accedere ad un sottoinsieme di elementi dell'array mediante una "maschera", ovvero un altro array, di dimensioni uguali a quelle di partenza, al cui interno sono presenti esclusivamente dei valori booleani. Così facendo, estrarremo soltanto gli elementi la cui corrispondente posizione all'interno della maschera ha valore `True`. Ad esempio, possiamo selezionare tutti gli elementi appartenenti alla prima colonna dell'array `b`:

```py
>>> mask = np.array([[True, False], [True, False]])
>>> b[mask]
array([1, 3])
```

Ancora, possiamo scegliere tutti gli elementi che soddisfano una certa condizione logico/matematica:

```py
>>> mask = (b > 2)
>>> mask
array([[False, False],
       [ True,  True]])
>>> b[mask]
array([3, 4])
```

Interessante notare come la precedente notazione possa essere ulteriormente sintetizzata usando delle relazioni logiche:

```py
>>> b[b > 2]
array([3, 4])
```

Volendo, possiamo adattare la forma precedente all'uso di espressioni arbitrariamente complesse:

```py
>>> b[b%2 == 0]
array([2, 4])
>>> b[(b > 1) & (b < 4)]
array([2, 3])
```

## 7.2.6 - Slicing degli array

Così come le liste, anche gli array consentono le operazioni di slicing:

```py
>>> a = np.array([1, 2, 3, 4])
>>> a[0:2]
array([1, 2])
```

Per gli array multidimensionali, lo slicing si intende sulla $n$-ma dimensione dell'array. Questo concetto è facile da comprendere se si visualizza l'array ad $n$-dimensioni come un array di array:

```py
>>> b
array([[1, 2],
       [3, 4]])
>>> b[0:1]              # Lo slicing avviene sulla seconda dimensione
array([[1, 2]])
```

## 7.2.7 - La funzione `nonzero()`

Possiamo usare la funzione `nonzero()` per selezionare gli elementi e gli indici di un array il cui valore non sia pari a zero. Ad esempio:

```py
>>> x = np.array([[3, 0, 0], [0, 4, 0], [5, 6, 0]])
>>> x
array([[3, 0, 0],
       [0, 4, 0],
       [5, 6, 0]])
>>> np.nonzero(x)
(array([0, 1, 2, 2], dtype=int64), array([0, 1, 0, 1], dtype=int64))
```

La funzione `nonzero()` restituisce una tupla con gli indici per riga e colonna degli elementi diversi da zero. In particolare, la tupla risultante avrà un numero di elementi pari a ciascuna delle dimensioni dell'array `x` di ingresso, e l'$i$-mo vettore individuerà gli indici relativi alla $i$-ma dimensione. Ad esempio, in questo caso, il primo array rappresenta gli indici relativi alla prima dimensione dei valori non nulli (in questo caso, gli indici di riga), mentre il secondo gli indici relativi alla seconda dimensione (indici di colonna). Notiamo quindi che avremo i seguenti elementi diversi da zero:

| Indice di riga | Indice di colonna | Valore |
| -------------- | ----------------- | ------ |
| 0              | 0                 | 3      |
| 1              | 1                 | 4      |
| 2              | 0                 | 5      |
| 2              | 1                 | 6      |

!!!tip "Ottenere una lista di tuple"
	Possiamo ottenere una lista di tuple rappresentative delle coppie di indici per gli elementi non nulli sfruttando la funzione `zip`:
    > ```py
    >>> s = np.nonzero(tarry)
    >>> s
    (array([0, 1, 2, 2], dtype=int64), array([0, 1, 0, 1], dtype=int64))
    >>> coords = list(zip(s[0], s[1]))
    >>> coords
    [(0, 0), (1, 1), (2, 0), (2, 1)]
    ```

## 7.2.7 - Fancy indexing

Chiudiamo questa lezione parlando di una tecnica molto interessante chiamata *fancy indexing*, consistente nell'usare un array di indici per accedere a più elementi contemporaneamente. Ad esempio:

```py
>>> rand = np.random.RandomState(42)
>>> x = rand.randint(100, size=10)
>>> indexes = np.array([[1, 4],[5, 2]])
>>> x
array([51, 92, 14, 71, 60, 20, 82, 86, 74, 74])
>>> x[indexes]
array([[92, 60],
       [20, 14]])
```

Nel codice precedente, stiamo:

1. usando la funzione `randint()` per generare un array di numeri interi casuali compresi tra 0 e 100;
2. generando un array bidimensionale `indexes`;
3. restituendo, mediante il fancy indexing, un array con le dimensioni di `indexes` e gli elementi di `x` presi nelle posizioni indicate da `indexes`.

La potenza del fancy indexing sta proprio in questo: non solo siamo in grado di accedere facilmente a più elementi di un array mediante un'unica operazione, ma possiamo anche ridisporre questi elementi come più ci aggrada!
