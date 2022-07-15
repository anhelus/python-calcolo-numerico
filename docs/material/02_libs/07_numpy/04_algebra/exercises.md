# E7.4 - Operazioni algebriche in NumPy

## Esercizio E7.4.1

Verificare che il prodotto tra una matrice invertibile e la sua inversa sia la matrice identità.

### Soluzione S7.4.1

Ecco una possibile soluzione.

```py
import numpy as np

mat = np.array([[5, 0, 1], [0, 2, 2], [0, 0, 3]])
mat_inv = np.linalg.inv(mat)
np.eye(3) == mat.dot(mat_inv)
```

## Esercizio E7.4.2

Scriviamo la funzione `calcola_determinante(mat)` che permetta di calcolare il determinante di una matrice $2 \times 2$ **senza usare l'apposita funzione NumPy**.

### Soluzione S7.4.2

Ecco una possibile soluzione:

```py
def calcola_determinante(mat):
    if len(mat.shape) == 2 and mat.shape[0] == mat.shape[1] and mat.shape[0] == 2:
        return mat[0][0] * mat[1][1] - mat[0][1] * mat[1][0]
    raise ValueError('La matrice non ha le dimensioni attese.')
```

## Esercizio E7.4.3

Scriviamo la funzione `inverti_se_invertibile(mat)` che, data una matrice bidimensionale, restituisca l'inversa soltanto se `mat` è bidimensionale, quadrata, e il determinante sia diverso da zero. Usare esclusivamente le istruzioni `if`.

### Soluzione S7.4.3

Ecco una possibile soluzione:

```py
def inverti_se_invertibile(mat):
    if len(mat.shape) == 2 \
        and mat.shape[0] == mat.shape[1] \
        and linalg.det(mat) != 0:
        return linalg.inv(mat)
    raise ValueError('La matrice passata non è invertibile.')
```
