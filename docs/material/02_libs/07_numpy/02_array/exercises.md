# E7.2 - Gli array

## Esercizio E7.2.1

Scriviamo una funzione che restituisca il prodotto riga per colonna di due vettori `v1` e `v2`. Usiamo una list comprehension, e verifichiamo che la lunghezza dei due vettori sia coerente. Valutiamo inoltre il tempo necessario all'esecuzione. Il metodo dovrà funzionare indipendentemente dall’ordine in cui sono passati i parametri.

Provare ad effettuare la stessa operazione in NumPy.

### Soluzione S7.2.1

Ecco una possibile soluzione:

```py
from time import time
import numpy as np

def riga_per_colonna(v1, v2):
	tic = time()
	if v1.shape[0] == 1:
		if v2.shape[1] == 1 and v1.shape[1] == v2.shape[0]:
			prod = sum([v1[0][i] * v2[i] for i in range(v2.shape[0])])
	elif v2.shape[0] == 1:
		if v1.shape[1] == 1 and v2.shape[1] == v1.shape[0]:
			prod = sum([v1[i] * v2[0][i] for i in range(v1.shape[0])])
	else:
		return 'Le dimensioni non sono coerenti!'
	toc = time()
	return prod, toc - tic

v1 = np.array([[1,2,3,4]])
v2 = np.array([[1],[2],[3],[4]])

res = riga_per_colonna(v1, v2)
res = riga_per_colonna(v2, v1)
res = riga_per_colonna(np.array([[1]]), v2)
```

L'equivalente operazione in NumPy è data da:

<!--
teoricamente
```python
res = np.dot(v1, v2) # oppure np.multiply(v1, v2)
```
-->

```py
res = np.dot(v1, v2)
```

## Esercizio E7.2.2

Scriviamo una funzione `crea_array(dim_1, dim_2, val_min, val_max)` che crei array di dimensioni arbitrarie `dim_1` $\times$ `dim_2` fatti di numeri interi casuali compresi tra `val_min` e `val_max`. Di default, la funzione dovrà creare dei vettori riga.

Provare ad effettuare la stessa operazione in NumPy.

### Soluzione S7.2.2

Ecco una possibile soluzione:

```py
import numpy as np
from random import randint

def crea_array(dim_1, dim_2=1, val_min=0, val_max=100):
	rows = [[randint(val_min, val_max) for i in range(dim_2)] for j in range(dim_1)]
	return np.array(rows)

a_1 = crea_array(4, 1)
a_2 = crea_array(2, 2)
```

Ovviamente, per NumPy ci basterà usare il metodo `randint`:

```py
from numpy import random

a_1 = random.randint(0, 100, (4, 1))
a_2 = random.randint(0, 100, (2, 2))
```
