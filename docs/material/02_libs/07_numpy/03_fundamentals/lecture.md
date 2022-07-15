# 7.3 - Operazioni fondamentali sugli array

## 7.3.1 - Operazioni algebriche di base

NumPy ci offre la possibilità di effettuare diversi tipi di operazioni algebriche di base sugli array. Ad esempio, è possibile sommare due array:

```py
>>> a = np.array([1, 2])
>>> b = np.array([3, 4])
>>> a + b
array([4, 6])
```

Possiamo ovviamente anche fare le altre operazioni fondamentali:

```py
>>> a - b
array([-2, -2])
>>> a * b
array([3, 8])
>>> a / b
array([0.33333333, 0.5])
>>> b / a
array([3., 2.])
```

!!!note "Moltiplicazione e divisione"
	Per comprendere appieno il comportamento degli operatori * e /, dovremo parlare del broadcasting. Lo faremo in una delle prossime lezioni.

## 7.3.2 - La funzione `sum()`

La funzione `sum(axis=None)` ci permette di sommare tutti gli elementi di un array lungo l'asse specificato.

Ad esempio, per sommare tutti gli elementi di un vettore:

```py
>>> a = np.array([1, 2, 3, 4])
>>> a.sum()
10
```

In caso di array multidimensionale, dovremo specificare, come già detto, l'asse. Ad esempio, per sommare gli elementi per colonna, dovremo passare il parametro `0`:

```py
>>> b = np.array([[1, 2], [3, 4]])
>>> b.sum(axis=0)
array([4, 6])
```

Per sommare gli elementi per riga, invece, dovremo passare il parametro `1`:

```py
>>> b.sum(axis=1)
array([3, 7])
```

## 7.3.3 - La funzione `dot()`

La funzione `dot()` ci permette di effettuare l'operazione di moltiplicazione matriciale standard:

```py
>>> a = np.array([[1, 2]])
>>> b = np.array([[3], [4]])
>>> a.dot(b)
array([11])
>>> b.dot(a)
array([[3, 6],
       [4, 8]])
```

## 7.3.4 - La funzione `sort()`

Mediante la funzione `sort()` è possibile ordinare gli elementi di un array. Ad esempio:

```py
>>> arr = np.array([2, 1, 5, 3, 7, 4, 6, 8])
>>> np.sort(arr)
array([1, 2, 3, 4, 5, 6, 7, 8])
```

L'ordine avviene maniera *ascendente* (ovvero dall'elemento più piccolo al più grande). In caso di array $n$-dimensionale, possiamo anche specificare l'asse lungo il quale avviene l'ordinamento, specificando il parametro axis. Ad esempio:

```py
>>> mat = np.array([[2, 3, 1], [4, 2, 6], [7, 5, 1]])
>>> mat
array([[2, 3, 1],
       [4, 2, 6],
       [7, 5, 1]])
```

Per ordinare lungo le colonne:

```py
>>> np.sort(mat, axis=0)
array([[2, 2, 1],
       [4, 3, 1],
       [7, 5, 6]])
```

Mentre per ordinare lungo le righe:

```py
>>> np.sort(mat, axis=1)
array([[1, 2, 3],
       [2, 4, 6],
       [1, 5, 7]])
```

Possiamo anche specificare diversi algoritmi di ordinamento mediante l'argomento `kind`, che ci permette di scegliere tra il quick sort, il merge sort e l'heap sort.

!!!note "Nota"
    Esistono anche altre funzioni per l'ordinamento di un array, come [`argsort()`](https://numpy.org/doc/stable/reference/generated/numpy.argsort.html#numpy.argsort), [`lexsort()`](https://numpy.org/doc/stable/reference/generated/numpy.lexsort.html#numpy.lexsort), [`searchsorted()`](https://numpy.org/doc/stable/reference/generated/numpy.searchsorted.html#numpy.searchsorted) e [`partition()`](https://numpy.org/doc/stable/reference/generated/numpy.partition.html#numpy.partition).

## 7.3.5 - Concatenare due array

Possiamo concatenare due array usando la funzione `concatenate()`:

```py
>>> a = np.array([1, 2, 3, 4])
>>> b = np.array([5, 6, 7, 8])
>>> np.concatenate((a, b))
array([1, 2, 3, 4, 5, 6, 7, 8])
```

Si può anche in questo caso usare il parametro `axis` per specificare l'asse lungo quale concatenare due diversi array:

```py
>>> x = np.array([[1, 2], [3, 4]])
>>> y = np.array([[5, 6], [7, 8]])
>>> np.concatenate((x, y), axis=0)
array([[1, 2],
       [3, 4],
       [5, 6],
       [7, 8]])
>>> np.concatenate((x, y), axis=1)
array([[1, 2, 5, 6],
       [3, 4, 7, 8]])
```

Ovviamente, le dimensioni degli array devono essere *coerenti* affinché vengano concatenati. Ad esempio, con questo array:

```py
>>> z = np.array([[9, 10]])
```

la concatenazione per righe è ammissibile:

```py
>>> np.concatenate((x, z), axis=0)
array([[ 1,  2],
       [ 3,  4],
       [ 9, 10]])
```

mentre la concatenazione per colonne non è possibile:

```py
>>> np.concatenate((x, z), axis=1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<__array_function__ internals>", line 5, in concatenate
ValueError: all the input array dimensions for the concatenation axis must match exactly, but along dimension 0, the array at index 0 has size 2 and the array at index 1 has size 1
```

## 7.3.6 - Rimozione ed inserimento di elementi in un array

### 7.3.6.1 - La funzione `delete()`

La funzione `delete(arr, obj, axis=None)` ci permette di rimuovere uno o più elementi di un array specificandone gli indici. La funzione accetta i seguenti parametri:

* `arr`: l'array sul quale vogliamo effettuare l'operazione di rimozione;
* `obj`: gli indici degli elementi da rimuovere;
* `axis`: l'asse su cui vogliamo operare.

Ad esempio, immaginiamo di voler rimuovere il primo elemento di un vettore:

```py
>>> arr = np.array([1, 2, 3, 4])
>>> np.delete(arr, 0)
array([2, 3, 4])
```

La funzione può essere anche applicata su più indici usando una sequenza:

```py
>>> np.delete(arr, range(2))
array([3, 4])
```

Possiamo anche usare lo slicing:

```py
>>> idx = range(4)
>>> np.delete(arr, idx[0:2])
array([3, 4])
```

!!!tip "Suggerimento"
    La precedente notazione può essere rimpiazzata dalla funzione `slice(start, stop, step)`, che crea un oggetto di classe `slice` sugli indici che vanno da `start` a `stop` con passo `step`. Questo può essere usato per scopi analoghi ai precedenti; ad esempio:
    > ```py
      >>> np.delete(a, slice(0, 2, 1))
      array([3, 4])
      ```

#### 7.3.6.1.1 - Array multidimensionali e `delete()`

La funzione `delete()` può essere usata anche su array multidimensionali. In questo caso, è opportuno specificare l'asse su cui operare.

Ad esempio, se vogliamo rimuovere la prima riga dal seguente array, dobbiamo dare il valore `0` al parametro `axis`:

```py
>>> mat = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
>>> np.delete(mat, 0, 0)
array([[4, 5, 6],
       [7, 8, 9]])
```

Invece, se vogliamo rimuovere la prima colonna, dobbiamo passare il valore `1`:

```py
>>> np.delete(mat, 0, 1)
array([[2, 3],
       [5, 6],
       [8, 9]])
```

Se non specificassimo alcun valore per il parametro `axis`, otterremmo questo risultato:

```py
>>> np.delete(mat, 0)
array([2, 3, 4, 5, 6, 7, 8, 9])
```

In altre parole, non specificando un valore per `axis`, rimuoveremmo il primo elemento dell'array "vettorizzato".

!!!tip "Rimozione mediante maschere booleane"
	Spesso è preferibile usare, al posto della notazione precedente, una maschera booleana:
    > ```py
      >>> mask = np.array([[True, False, True], [False, False, True], [False, True, True]])
      >>> mtrx[mask]
      array([1, 3, 6, 8, 9])
      ```

### 7.3.6.2 - La funzione `insert()`

La funzione `insert(arr, obj, values, axis=None)` permette di inserire un elemento all'interno di un array. I parametri accettati dalla funzione sono:

* `arr`: l'array sul quale vogliamo effettuare l'operazione di inserzione;
* `obj`: gli indici su cui inserire i nuovi valori;
* `values`: i valori da inserire agli indici specificati da `obj`;
* `axis`: l'asse su cui vogliamo operare.

Ad esempio, per inserire una nuova riga nella matrice precedente, dovremo specificare l'indice di riga (`3`), gli elementi della riga da inserire (`[10, 11, 12]`) e l'asse (`0`):

```py
>>> np.insert(mat, 3, [10, 11, 12], 0)
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
```

Cambiando l'asse in `1`, si effettua l'inserzione sulle colonne:

```py
>>> np.insert(mat, 3, [10, 11, 12], 1)
array([[ 1,  2,  3, 10],
       [ 4,  5,  6, 11],
       [ 7,  8,  9, 12]])
```

Non specificando alcun asse, infine, si inserisce l'elemento specificato nella matrice vettorizzata:

```py
>>> np.insert(mat, 9, 10)
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])
```

### 7.3.6.3 - La funzione `append()`

La funzione `append(arr, values, axis=None)` permette di inserire in coda ad un array i valori specificati. I parametri accettati dalla funzione sono:

* `arr`: l'array sul quale vogliamo effettuare l'operazione di inserzione;
* `values`: i valori da inserire in coda all'array;
* `axis`: l'asse su cui vogliamo operare.

Al solito, non specificando l'asse effettuiamo la concatenazione sulla matrice vettorizzata:

```py
>>> np.append(mat, [[10, 11, 12]])
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12])
```

Se specifichiamo il valore 0 sul parametro `axis`, effettuiamo la concatenazione per righe:

```py
>>> np.append(mat, [[10, 11, 12]], axis=0)
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
```

Se specifichiamo il valore 1 sul parametro `axis`, invece, effettuiamo la concatenazione per colonne:

```py
>>> np.append(mat, [[10], [11], [12]], axis=1)
array([[ 1,  2,  3, 10],
       [ 4,  5,  6, 11],
       [ 7,  8,  9, 12]])
```

!!!warning "Attenzione"
    Nell'ultima istruzione, abbiamo usato un vettore *colonna*, mentre nella penultima un vettore *riga*.

## 7.3.7 - Dimensioni e forma di un array

Esistono diverse proprietà di un array che ne descrivono dimensioni e forma.

Tornando alla nostra matrice `mat`, possiamo conoscere il numero di assi mediante l'attributo `ndarray.ndim`:

```py
>>> mat.ndim
2
```

Il numero di elementi è invece definito dall'attributo `ndarray.size`:

```py
>>> mat.size
9
```

L'attributo `ndarray.shape` restituisce invece una tupla di interi che indica il numero di elementi per ciascuno degli assi dell'array:

```py
>>> mat.shape
(3, 3)
```

## 7.3.8 - Modificare le dimensioni di un array

Possiamo modificare le dimensioni di un array mediante la funzione `reshape(arr, new_shape)`. I parametri passati alla funzione sono:

* `arr`: l'array di cui modificare le dimensioni;
* `new_shape`: le nuove dimensioni dell'array.

Se volessimo modificare le dimensioni di una matrice da $4 \times 4$ a $2 \times 8$, potremmo usare la funzione `reshape()` come segue:

```py
>>> mat = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]])
>>> np.reshape(mat, (2, 8))
array([[ 1,  2,  3,  4,  5,  6,  7,  8],
       [ 9, 10, 11, 12, 13, 14, 15, 16]])
```

!!!tip "Suggerimento"
    Una forma alternativa è la seguente:
    > ```py
      >>> mat.reshape((2, 8))
      array([[ 1,  2,  3,  4,  5,  6,  7,  8],
             [ 9, 10, 11, 12, 13, 14, 15, 16]])
      ```
    Ciò significa che la funzione `reshape()` è sia disponibile nella libreria NumPy, sia come metodo sugli oggetti di classe `ndarray`.

!!!warning "Attenzione"
    Le nuove dimensioni dell'array devono essere coerenti con quelle dell'array di partenza!

## 7.3.9 - Flattening di un array

Abbiamo già visto in precedenza la *vettorizzazione* di un array, effettuata in automatico in alcune situazioni (come ad esempio la chiamata di `delete()` o `insert()` senza specificare il parametro `axis`). Tuttavia, possiamo usare la funzione `flatten()` per effettuare manualmente questa operazione:

```py
>>> mat.flatten()
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16])
```

!!!tip "La funzione `ravel()`"
	Un altro modo per vettorizzare un array è utilizzare la funzione `ravel()`, che restituisce un risultato analogo alla `flatten()`, a meno di una importante differenza: infatti, laddove `flatten()` restituisce una copia dell'array vettorizzato, `ravel()` mantiene un riferimento all'array originario.
